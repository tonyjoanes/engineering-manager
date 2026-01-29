# Platform Engineering for Azure Shops

A guide to building internal developer platforms using Azure-native tools and best practices.

## Your Current Stack

**Infrastructure as Code:**
- Bicep (Azure native)
- Terraform (starting to adopt)
- PowerShell (automation)

**CI/CD:**
- Azure DevOps (Azure Pipelines)
- YAML pipelines

**Cloud Platform:**
- Microsoft Azure

**This guide:** Azure-first recommendations while keeping flexibility for best-of-breed tools.

## Azure Platform Engineering Components

### 1. Infrastructure as Code

#### Bicep (Recommended for Azure-Native)

**Why Bicep:**
- Native Azure support (always up-to-date with latest services)
- Type safety and IntelliSense
- Simpler than ARM templates
- No state file management
- Modules for reusability
- Integration with Azure DevOps

**Platform approach with Bicep:**

**Create reusable modules:**
```
platform-modules/
├── web-app/
│   ├── main.bicep
│   ├── parameters.json
│   └── README.md
├── sql-database/
│   ├── main.bicep
│   └── README.md
├── storage-account/
├── app-service-plan/
└── virtual-network/
```

**Module structure (web-app example):**
```bicep
// platform-modules/web-app/main.bicep
@description('Name of the web app')
param webAppName string

@description('Location for resources')
param location string = resourceGroup().location

@description('Environment (dev, staging, prod)')
@allowed(['dev', 'staging', 'prod'])
param environment string

@description('App Service Plan SKU')
param sku string = 'B1'

// Naming convention enforced
var appServicePlanName = 'asp-${webAppName}-${environment}'
var appInsightsName = 'ai-${webAppName}-${environment}'

// Best practices baked in
resource appServicePlan 'Microsoft.Web/serverfarms@2022-03-01' = {
  name: appServicePlanName
  location: location
  sku: {
    name: sku
  }
  properties: {
    reserved: true // Linux
  }
  tags: {
    environment: environment
    managedBy: 'platform-team'
  }
}

resource webApp 'Microsoft.Web/sites@2022-03-01' = {
  name: webAppName
  location: location
  properties: {
    serverFarmId: appServicePlan.id
    httpsOnly: true // Security by default
    siteConfig: {
      alwaysOn: true
      minTlsVersion: '1.2'
      ftpsState: 'Disabled'
      // Application Insights auto-configured
      appSettings: [
        {
          name: 'APPINSIGHTS_INSTRUMENTATIONKEY'
          value: appInsights.properties.InstrumentationKey
        }
      ]
    }
  }
  tags: {
    environment: environment
    managedBy: 'platform-team'
  }
}

// Monitoring included by default
resource appInsights 'Microsoft.Insights/components@2020-02-02' = {
  name: appInsightsName
  location: location
  kind: 'web'
  properties: {
    Application_Type: 'web'
  }
}

output webAppUrl string = 'https://${webApp.properties.defaultHostName}'
output appInsightsKey string = appInsights.properties.InstrumentationKey
```

**Service template for teams:**
```bicep
// team-service.bicep
param serviceName string
param environment string

module webApp '../platform-modules/web-app/main.bicep' = {
  name: '${serviceName}-webapp'
  params: {
    webAppName: serviceName
    environment: environment
    sku: environment == 'prod' ? 'P1v2' : 'B1'
  }
}

module database '../platform-modules/sql-database/main.bicep' = {
  name: '${serviceName}-db'
  params: {
    databaseName: serviceName
    environment: environment
  }
}
```

**Self-service usage:**
```bash
# Teams can deploy with simple command
az deployment group create \
  --resource-group rg-myservice-prod \
  --template-file team-service.bicep \
  --parameters serviceName=myapi environment=prod
```

**Benefits:**
- Security and compliance built-in
- Monitoring automatically configured
- Naming conventions enforced
- Best practices baked in
- Simple for teams to use

#### Terraform (Recommended for Multi-Cloud or Specific Use Cases)

**When to use Terraform instead of Bicep:**
- Multi-cloud scenarios
- Non-Azure resources (GitHub, Datadog, etc.)
- Existing Terraform expertise
- Complex state management needs
- Provider ecosystem (over 3000 providers)

**Azure + Terraform architecture:**
```
terraform/
├── modules/
│   ├── azure-web-app/
│   ├── azure-sql/
│   └── github-repo/          # Can manage non-Azure
├── environments/
│   ├── dev/
│   ├── staging/
│   └── prod/
└── shared/
    └── backend.tf             # Azure Storage for state
```

**State in Azure Storage:**
```hcl
# backend.tf
terraform {
  backend "azurerm" {
    resource_group_name  = "rg-terraform-state"
    storage_account_name = "tfstateplatform"
    container_name       = "tfstate"
    key                  = "prod.terraform.tfstate"
  }
}
```

**Hybrid approach:**
```
Use Bicep for: Pure Azure infrastructure
Use Terraform for:
- Multi-cloud resources
- GitHub/GitLab management
- Third-party SaaS (Datadog, PagerDuty)
- When Bicep doesn't support resource yet
```

#### PowerShell (Recommended for Automation & Operations)

**Great for:**
- Operational tasks
- Azure AD/Entra ID management
- Complex logic and conditionals
- Bulk operations
- Reports and audits

**Platform automation examples:**

**User provisioning:**
```powershell
# New-DeveloperEnvironment.ps1
param(
    [Parameter(Mandatory=$true)]
    [string]$DeveloperEmail,

    [Parameter(Mandatory=$true)]
    [string]$ServiceName
)

# Create resource group
$rgName = "rg-$ServiceName-dev-$(Get-Random -Maximum 9999)"
New-AzResourceGroup -Name $rgName -Location "eastus"

# Assign developer permissions
$user = Get-AzADUser -UserPrincipalName $DeveloperEmail
New-AzRoleAssignment `
    -ObjectId $user.Id `
    -RoleDefinitionName "Contributor" `
    -ResourceGroupName $rgName

# Deploy from Bicep template
New-AzResourceGroupDeployment `
    -ResourceGroupName $rgName `
    -TemplateFile "./templates/dev-environment.bicep" `
    -serviceName $ServiceName

Write-Host "Environment created: $rgName"
Write-Host "Developer $DeveloperEmail has Contributor access"
```

**Cost reporting:**
```powershell
# Get-CostByTeam.ps1
$tags = @("team", "environment", "costcenter")

Get-AzResourceGroup | ForEach-Object {
    $consumption = Get-AzConsumptionUsageDetail `
        -ResourceGroup $_.ResourceGroupName `
        -StartDate (Get-Date).AddDays(-30) `
        -EndDate (Get-Date)

    [PSCustomObject]@{
        ResourceGroup = $_.ResourceGroupName
        Team = $_.Tags["team"]
        Environment = $_.Tags["environment"]
        Cost = ($consumption | Measure-Object -Property PretaxCost -Sum).Sum
    }
} | Export-Csv -Path "monthly-costs.csv"
```

### 2. CI/CD Platform (Azure DevOps)

#### Azure Pipelines

**Golden path pipeline template:**

**Template (azure-pipelines-template.yml):**
```yaml
# Platform team maintains this template
parameters:
  - name: serviceName
    type: string
  - name: buildConfiguration
    type: string
    default: 'Release'
  - name: runTests
    type: boolean
    default: true

stages:
  # Build stage
  - stage: Build
    jobs:
      - job: BuildAndTest
        pool:
          vmImage: 'ubuntu-latest'
        steps:
          # Restore dependencies
          - task: DotNetCoreCLI@2
            displayName: 'Restore packages'
            inputs:
              command: restore

          # Build
          - task: DotNetCoreCLI@2
            displayName: 'Build solution'
            inputs:
              command: build
              arguments: '--configuration ${{ parameters.buildConfiguration }}'

          # Run tests (if enabled)
          - ${{ if eq(parameters.runTests, true) }}:
            - task: DotNetCoreCLI@2
              displayName: 'Run tests'
              inputs:
                command: test
                arguments: '--configuration ${{ parameters.buildConfiguration }} --collect:"XPlat Code Coverage"'

            # Publish test results
            - task: PublishTestResults@2
              inputs:
                testResultsFormat: 'VSTest'
                testResultsFiles: '**/*.trx'

          # Security scanning (built into platform)
          - task: WhiteSource@21
            displayName: 'Security scan'
            inputs:
              cwd: '$(System.DefaultWorkingDirectory)'

          # Publish artifact
          - task: DotNetCoreCLI@2
            displayName: 'Publish application'
            inputs:
              command: publish
              publishWebProjects: true
              arguments: '--configuration ${{ parameters.buildConfiguration }} --output $(Build.ArtifactStagingDirectory)'

          - task: PublishBuildArtifacts@1
            inputs:
              pathToPublish: '$(Build.ArtifactStagingDirectory)'
              artifactName: 'drop'

  # Deploy to Dev (automatic)
  - stage: DeployDev
    dependsOn: Build
    jobs:
      - deployment: DeployToDev
        environment: 'dev'
        strategy:
          runOnce:
            deploy:
              steps:
                - template: deploy-steps.yml
                  parameters:
                    environment: 'dev'
                    serviceName: ${{ parameters.serviceName }}

  # Deploy to Staging (manual approval)
  - stage: DeployStaging
    dependsOn: DeployDev
    jobs:
      - deployment: DeployToStaging
        environment: 'staging'
        strategy:
          runOnce:
            deploy:
              steps:
                - template: deploy-steps.yml
                  parameters:
                    environment: 'staging'
                    serviceName: ${{ parameters.serviceName }}

  # Deploy to Prod (manual approval + gates)
  - stage: DeployProd
    dependsOn: DeployStaging
    jobs:
      - deployment: DeployToProd
        environment: 'production'
        strategy:
          runOnce:
            deploy:
              steps:
                - template: deploy-steps.yml
                  parameters:
                    environment: 'prod'
                    serviceName: ${{ parameters.serviceName }}
```

**Deployment steps (deploy-steps.yml):**
```yaml
parameters:
  - name: environment
    type: string
  - name: serviceName
    type: string

steps:
  # Download artifact
  - download: current
    artifact: drop

  # Deploy infrastructure with Bicep
  - task: AzureCLI@2
    displayName: 'Deploy infrastructure'
    inputs:
      azureSubscription: 'Platform-ServiceConnection-${{ parameters.environment }}'
      scriptType: 'bash'
      scriptLocation: 'inlineScript'
      inlineScript: |
        az deployment group create \
          --resource-group rg-${{ parameters.serviceName }}-${{ parameters.environment }} \
          --template-file ./infra/main.bicep \
          --parameters environment=${{ parameters.environment }}

  # Deploy application
  - task: AzureWebApp@1
    displayName: 'Deploy to Azure Web App'
    inputs:
      azureSubscription: 'Platform-ServiceConnection-${{ parameters.environment }}'
      appType: 'webAppLinux'
      appName: '${{ parameters.serviceName }}-${{ parameters.environment }}'
      package: '$(Pipeline.Workspace)/drop/**/*.zip'

  # Run smoke tests
  - task: PowerShell@2
    displayName: 'Smoke tests'
    inputs:
      targetType: 'inline'
      script: |
        $url = "https://${{ parameters.serviceName }}-${{ parameters.environment }}.azurewebsites.net/health"
        $response = Invoke-WebRequest -Uri $url -UseBasicParsing
        if ($response.StatusCode -ne 200) {
          throw "Health check failed"
        }
```

**Team usage (simple):**
```yaml
# Team's azure-pipelines.yml
trigger:
  - main

# Use platform template
extends:
  template: azure-pipelines-template.yml@platform-templates
  parameters:
    serviceName: 'my-api'
    runTests: true
```

**Benefits:**
- Platform team maintains best practices
- Security scanning automatic
- Consistent across all services
- Teams get started in minutes
- Approval gates configured
- Infrastructure and code deployed together

#### Azure DevOps Service Connections

**Platform team pre-configures:**
```
Service Connections (per environment):
├── Platform-ServiceConnection-dev
├── Platform-ServiceConnection-staging
└── Platform-ServiceConnection-prod

Each with:
- Service Principal with least privilege
- Scoped to environment resource groups
- Automatic secret rotation
- Approval gates configured
```

**Teams reference, don't create:**
```yaml
# Teams use pre-configured connections
azureSubscription: 'Platform-ServiceConnection-prod'
# No managing credentials!
```

### 3. Developer Portal (Azure-Integrated Options)

#### Option 1: Spotify Backstage (with Azure Plugins)

**Why Backstage for Azure:**
- Open source, flexible
- Azure plugins available
- Service catalog
- Template scaffolding
- TechDocs integration

**Azure-specific plugins:**
```yaml
# app-config.yaml
backend:
  database:
    client: pg
    connection:
      host: ${POSTGRES_HOST}  # Azure Database for PostgreSQL

integrations:
  azure:
    - host: dev.azure.com
      credentials:
        - organizations:
            - your-org
          personalAccessToken: ${AZURE_TOKEN}

catalog:
  providers:
    azureDevOps:
      organization: your-org
      project: '*'

    azureResourceGraph:
      tenantId: ${AZURE_TENANT_ID}
      clientId: ${AZURE_CLIENT_ID}
      clientSecret: ${AZURE_CLIENT_SECRET}
```

**Service templates in Backstage:**
```yaml
# template.yaml
apiVersion: scaffolder.backstage.io/v1beta3
kind: Template
metadata:
  name: azure-webapp-template
  title: Azure Web App
  description: Create a new Azure Web App with best practices
spec:
  owner: platform-team
  type: service

  parameters:
    - title: Service Information
      required:
        - name
        - owner
      properties:
        name:
          title: Service Name
          type: string
        owner:
          title: Owner Team
          type: string
          ui:field: OwnerPicker
        environment:
          title: Environment
          type: string
          enum: ['dev', 'staging', 'prod']

  steps:
    - id: fetch-base
      name: Fetch Base
      action: fetch:template
      input:
        url: ./template-content
        values:
          name: ${{ parameters.name }}
          owner: ${{ parameters.owner }}

    - id: create-repo
      name: Create Azure DevOps Repo
      action: azure:repo:create
      input:
        organization: your-org
        project: your-project
        repoName: ${{ parameters.name }}

    - id: create-pipeline
      name: Create Pipeline
      action: azure:pipeline:create
      input:
        organization: your-org
        project: your-project
        pipelineYaml: azure-pipelines.yml

    - id: deploy-infra
      name: Deploy Infrastructure
      action: azure:bicep:deploy
      input:
        template: ./infra/main.bicep
        resourceGroup: rg-${{ parameters.name }}-${{ parameters.environment }}
```

#### Option 2: Azure Portal Extensions (Lightweight)

**For simpler needs:**
- Custom Azure Portal extensions
- Azure Resource Graph queries
- PowerShell-based portals
- Static site with Azure Functions backend

**Simple portal example:**
```typescript
// Azure Function backend
export async function createService(
  serviceName: string,
  environment: string
): Promise<void> {
  // Execute Bicep deployment
  await exec(`
    az deployment group create \
      --resource-group rg-${serviceName}-${environment} \
      --template-file ./templates/service.bicep \
      --parameters serviceName=${serviceName}
  `);

  // Create ADO repo
  await createAzureDevOpsRepo(serviceName);

  // Create pipeline from template
  await createPipeline(serviceName);

  // Assign permissions
  await assignPermissions(serviceName, environment);
}
```

### 4. Observability (Azure Native)

#### Azure Monitor (Comprehensive)

**Platform configuration:**

**Log Analytics Workspace (centralized):**
```bicep
resource logAnalytics 'Microsoft.OperationalInsights/workspaces@2021-06-01' = {
  name: 'log-platform-prod'
  location: location
  properties: {
    sku: {
      name: 'PerGB2018'
    }
    retentionInDays: 90
  }
}

// Auto-configure for all resources
resource diagnosticSettings 'Microsoft.Insights/diagnosticSettings@2021-05-01-preview' = {
  name: 'platform-diagnostics'
  scope: webApp
  properties: {
    workspaceId: logAnalytics.id
    logs: [
      {
        category: 'AppServiceHTTPLogs'
        enabled: true
      }
      {
        category: 'AppServiceConsoleLogs'
        enabled: true
      }
    ]
    metrics: [
      {
        category: 'AllMetrics'
        enabled: true
      }
    ]
  }
}
```

**Application Insights (automatic):**
- Built into web app module
- Connection string in app settings
- Distributed tracing enabled
- Performance monitoring

**Kusto queries for teams:**
```kql
// Example: Error rate by service
AppRequests
| where TimeGenerated > ago(1h)
| summarize
    Total = count(),
    Errors = countif(Success == false)
    by AppRoleName
| extend ErrorRate = (Errors * 100.0) / Total
| order by ErrorRate desc
```

**Azure Workbooks (dashboards):**
```json
{
  "version": "Notebook/1.0",
  "items": [
    {
      "type": 3,
      "content": {
        "version": "KqlItem/1.0",
        "query": "AppRequests | summarize count() by bin(TimeGenerated, 5m)",
        "visualization": "timechart"
      }
    }
  ]
}
```

#### Alerts (Platform-Managed)

**Common alerts pre-configured:**
```bicep
// High error rate alert
resource errorRateAlert 'Microsoft.Insights/metricAlerts@2018-03-01' = {
  name: 'alert-high-error-rate-${serviceName}'
  location: 'global'
  properties: {
    severity: 2
    enabled: true
    evaluationFrequency: 'PT5M'
    windowSize: 'PT5M'
    criteria: {
      'odata.type': 'Microsoft.Azure.Monitor.SingleResourceMultipleMetricCriteria'
      allOf: [
        {
          name: 'ErrorRate'
          metricName: 'Requests/Failed'
          operator: 'GreaterThan'
          threshold: 5  // 5% error rate
          timeAggregation: 'Average'
        }
      ]
    }
    actions: [
      {
        actionGroupId: platformActionGroup.id
      }
    ]
  }
}
```

### 5. Development Environments

#### Azure Dev Box (Preview)

**Cloud-based development environments:**
- Pre-configured with tools
- Consistent across team
- Scales up/down
- Access from anywhere

**Platform setup:**
```bicep
resource devCenter 'Microsoft.DevCenter/devcenters@2023-04-01' = {
  name: 'devcenter-platform'
  location: location

  identity: {
    type: 'SystemAssigned'
  }
}

resource devBoxDefinition 'Microsoft.DevCenter/devcenters/devboxdefinitions@2023-04-01' = {
  parent: devCenter
  name: 'dotnet-developer'
  properties: {
    imageReference: {
      id: '/subscriptions/.../images/vs2022-dotnet-azure'
    }
    sku: {
      name: 'general_i_8c32gb256ssd_v2'
    }
    hibernateSupport: 'Enabled'
  }
}
```

**Developers self-service provision via portal or CLI**

#### Alternative: Local + Azure Resources

**Dev environment with Azure:**
```yaml
# docker-compose.yml (local services)
version: '3.8'
services:
  app:
    build: .
    environment:
      - AZURE_SQL_CONNECTION=${AZURE_SQL_CONNECTION}
      - AZURE_STORAGE_CONNECTION=${AZURE_STORAGE_CONNECTION}
      - APPINSIGHTS_KEY=${APPINSIGHTS_KEY}
    # Local development, cloud resources
```

**PowerShell to setup dev resources:**
```powershell
# Setup-DevEnvironment.ps1
param([string]$DeveloperName)

$resourceGroup = "rg-dev-$DeveloperName"

# Create dev resource group
New-AzResourceGroup -Name $resourceGroup -Location "eastus"

# Deploy dev resources from template
New-AzResourceGroupDeployment `
    -ResourceGroupName $resourceGroup `
    -TemplateFile "./dev-environment.bicep" `
    -developerName $DeveloperName

# Output connection strings
$storage = Get-AzStorageAccount -ResourceGroupName $resourceGroup
Write-Host "AZURE_STORAGE_CONNECTION=$($storage.Context.ConnectionString)"
```

### 6. Secret Management

#### Azure Key Vault (Recommended)

**Platform approach:**

**Key Vault per environment:**
```bicep
resource keyVault 'Microsoft.KeyVault/vaults@2023-02-01' = {
  name: 'kv-${serviceName}-${environment}'
  location: location
  properties: {
    sku: {
      family: 'A'
      name: 'standard'
    }
    tenantId: subscription().tenantId

    // RBAC-based access (not access policies)
    enableRbacAuthorization: true

    // Security best practices
    enableSoftDelete: true
    softDeleteRetentionInDays: 90
    enablePurgeProtection: true

    networkAcls: {
      defaultAction: 'Deny'
      bypass: 'AzureServices'
      virtualNetworkRules: [
        {
          id: vnet.properties.subnets[0].id
        }
      ]
    }
  }
}

// App identity can read secrets
resource secretReader 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
  scope: keyVault
  name: guid(keyVault.id, webApp.id, 'Key Vault Secrets User')
  properties: {
    roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', '4633458b-17de-408a-b874-0445c86b69e6') // Key Vault Secrets User
    principalId: webApp.identity.principalId
  }
}
```

**Application usage (automatic with Managed Identity):**
```csharp
// .NET code - no secrets in code!
var keyVaultUrl = "https://kv-myservice-prod.vault.azure.net/";
var client = new SecretClient(
    new Uri(keyVaultUrl),
    new DefaultAzureCredential()  // Uses Managed Identity
);

var secret = await client.GetSecretAsync("database-password");
```

**Pipeline secret access:**
```yaml
# Azure Pipelines
steps:
  - task: AzureKeyVault@2
    inputs:
      azureSubscription: 'Platform-ServiceConnection-prod'
      KeyVaultName: 'kv-myservice-prod'
      SecretsFilter: '*'

  # Secrets available as variables
  - script: |
      echo "Deploying with database password from Key Vault"
      # $(database-password) is available
```

## Azure-Specific Platform Patterns

### Pattern 1: Landing Zones

**Azure Landing Zone architecture:**
```
Management Groups:
├── Platform
│   ├── Management (Log Analytics, etc.)
│   ├── Identity (Azure AD, etc.)
│   └── Connectivity (Hub VNet, Firewall)
└── Landing Zones
    ├── Corp (internal apps)
    └── Online (internet-facing apps)
        ├── Development
        ├── Staging
        └── Production
```

**Bicep modules for landing zones:**
```bicep
// Hub VNet (platform team manages)
module hubNetwork './modules/hub-network.bicep' = {
  name: 'hubNetwork'
  params: {
    vnetName: 'vnet-hub-prod'
    addressPrefix: '10.0.0.0/16'
  }
}

// Spoke VNet for team (self-service)
module spokeNetwork './modules/spoke-network.bicep' = {
  name: 'teamSpokeNetwork'
  params: {
    vnetName: 'vnet-team-prod'
    addressPrefix: '10.1.0.0/16'
    hubVnetId: hubNetwork.outputs.vnetId
  }
}
```

### Pattern 2: Policy as Code

**Azure Policy for guardrails:**
```bicep
// Enforce tagging
resource tagPolicy 'Microsoft.Authorization/policyDefinitions@2021-06-01' = {
  name: 'require-tags'
  properties: {
    policyType: 'Custom'
    mode: 'Indexed'
    policyRule: {
      if: {
        anyOf: [
          {
            field: 'tags[environment]'
            exists: false
          }
          {
            field: 'tags[owner]'
            exists: false
          }
        ]
      }
      then: {
        effect: 'deny'
      }
    }
  }
}

// Assign to subscription
resource policyAssignment 'Microsoft.Authorization/policyAssignments@2021-06-01' = {
  name: 'enforce-tags'
  properties: {
    policyDefinitionId: tagPolicy.id
    displayName: 'Require environment and owner tags'
  }
}
```

**Common policies:**
- Require specific Azure regions
- Enforce naming conventions
- Require encryption
- Deny public IP addresses
- Require diagnostic settings
- Cost limits per resource group

### Pattern 3: Subscription Vending

**Automated subscription provisioning:**
```powershell
# New-TeamSubscription.ps1
param(
    [string]$TeamName,
    [string]$Environment
)

# Create new subscription (Enterprise Agreement)
$subscription = New-AzSubscription `
    -Name "sub-$TeamName-$Environment" `
    -OfferType "MS-AZR-0017P" `
    -EnrollmentAccountObjectId $enrollmentAccountId

# Move to appropriate management group
New-AzManagementGroupSubscription `
    -GroupName "mg-landingzones-$Environment" `
    -SubscriptionId $subscription.SubscriptionId

# Assign RBAC
New-AzRoleAssignment `
    -ObjectId $teamGroupId `
    -RoleDefinitionName "Contributor" `
    -Scope "/subscriptions/$($subscription.SubscriptionId)"

# Deploy landing zone resources
New-AzDeployment `
    -Location "eastus" `
    -TemplateFile "./landing-zone.bicep" `
    -subscriptionId $subscription.SubscriptionId
```

## Tool Recommendations for Azure Shops

### Core Stack (Keep)

✅ **Azure DevOps** - Your CI/CD platform
- Native Azure integration
- YAML pipelines
- Artifact management
- Test plans
- Work item tracking

✅ **Bicep** - Primary IaC for Azure resources
- Latest Azure features
- Type safety
- Native support
- No state management

✅ **PowerShell** - Automation and operations
- Azure management
- Complex logic
- Bulk operations
- Scripting tasks

### Selectively Adopt

🔄 **Terraform** - For specific scenarios
- Multi-cloud
- Non-Azure providers (GitHub, Datadog, etc.)
- When Bicep doesn't support something yet
- Team preference/expertise

### Consider Adding

**Developer Portal:**
- **Spotify Backstage** (if need sophisticated portal)
- **Custom portal** with Azure Functions (simpler needs)
- **Azure Portal extensions** (lightweight)

**GitOps (if Kubernetes):**
- **Flux CD** or **ArgoCD** with Azure Arc
- Integrate with Azure DevOps repos

**Secrets Management:**
- **Azure Key Vault** (already included)
- **HashiCorp Vault** (if multi-cloud or specific compliance)

**Observability:**
- **Azure Monitor + Application Insights** (primary)
- **Datadog or New Relic** (if multi-cloud or specific features)

**Testing:**
- **Azure Load Testing** (performance)
- **Playwright** or **Cypress** (E2E)

**Security:**
- **Microsoft Defender for Cloud** (built-in)
- **Snyk or WhiteSource** (dependency scanning)
- **SonarQube** (code quality)

## Implementation Roadmap

### Phase 1: Foundation (Month 1-2)

**Infrastructure:**
- ✅ Bicep module library
- ✅ Naming conventions
- ✅ Azure Policy guardrails
- ✅ Centralized logging

**CI/CD:**
- ✅ Pipeline templates
- ✅ Service connections per environment
- ✅ Approval gates

**Documentation:**
- ✅ Getting started guide
- ✅ Module documentation
- ✅ Best practices

### Phase 2: Self-Service (Month 3-4)

**Automation:**
- ✅ PowerShell scripts for common tasks
- ✅ Service creation workflow
- ✅ Developer environment setup

**Templates:**
- ✅ Web app template
- ✅ API template
- ✅ Microservice template

**Observability:**
- ✅ Standard dashboards
- ✅ Alert rules
- ✅ Runbooks

### Phase 3: Portal (Month 5-6)

**Developer portal:**
- Service catalog
- Template scaffolding
- Documentation hub
- Self-service actions

**Metrics:**
- Adoption tracking
- Developer satisfaction
- DORA metrics

### Phase 4: Optimization (Ongoing)

**Continuous improvement:**
- Feedback loops
- New templates
- Process improvements
- Cost optimization

## Azure-Specific Resources

### Microsoft Documentation
- [ ] Azure Architecture Center
- [ ] Azure DevOps Best Practices
- [ ] Bicep documentation
- [ ] Azure Landing Zones

### Tools
- [ ] Azure Resource Graph Explorer
- [ ] Azure Cost Management
- [ ] Azure Advisor
- [ ] Azure Security Center

### Training
- [ ] Microsoft Learn (free)
- [ ] Azure certifications (AZ-400 DevOps, AZ-305 Architecture)
- [ ] Bicep learning path
- [ ] PowerShell for Azure

### Community
- [ ] Azure DevOps Community
- [ ] Bicep GitHub discussions
- [ ] Azure Tech Community

---

[← Back to Practices](./README.md) | [← Back to Index](../README.md)
