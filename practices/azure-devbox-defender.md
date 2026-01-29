# Azure Dev Box & Microsoft Defender for Cloud

A comprehensive guide to implementing cloud development environments and security at scale.

## Overview

**Azure Dev Box:** Cloud-based, pre-configured development workstations
**Microsoft Defender for Cloud:** Unified security management and threat protection

**Together they provide:**
- Consistent, secure development environments
- Security posture management
- Compliance monitoring
- Threat protection
- Policy enforcement

## Part 1: Azure Dev Box

### What is Azure Dev Box?

**Cloud-based development workstations that are:**
- Pre-configured with tools and access
- Consistent across team
- Accessible from anywhere
- Managed centrally
- Hibernate when not in use (cost savings)

**Use cases:**
- Remote/hybrid teams
- Onboarding new developers
- Contractor/temporary access
- High-security environments
- Consistent development environments
- Heavy compute needs (ML, builds)

### Architecture

```
Dev Center (Platform Team Manages)
├── Dev Box Definitions (VM images)
│   ├── .NET Developer (VS 2022, .NET SDK, Azure CLI)
│   ├── Java Developer (IntelliJ, JDK, Maven)
│   └── Data Engineer (Python, Spark, Databricks)
├── Network Connections (VNet integration)
└── Projects (Teams)
    └── Dev Box Pools (Environment types)
        ├── Development (8 cores, 32GB)
        ├── High-Performance (16 cores, 64GB)
        └── Testing (4 cores, 16GB)

Developers Self-Service
├── Create dev box from portal/CLI
├── Connect via browser or RDP
├── Pre-configured with everything needed
└── Hibernate when done
```

### Setting Up Azure Dev Box

#### Step 1: Create Dev Center (Platform Team)

```bicep
// dev-center.bicep
resource devCenter 'Microsoft.DevCenter/devcenters@2023-04-01' = {
  name: 'devcenter-platform'
  location: location

  identity: {
    type: 'SystemAssigned'
  }

  tags: {
    environment: 'platform'
    managedBy: 'platform-team'
  }
}

// Network connection for dev boxes
resource networkConnection 'Microsoft.DevCenter/networkConnections@2023-04-01' = {
  name: 'nc-devbox-prod'
  location: location

  properties: {
    domainJoinType: 'AzureADJoin'  // or 'HybridAzureADJoin'
    subnetId: devVnetSubnet.id
    networkingResourceGroupName: 'rg-devbox-networking'
  }
}

// Attach network to dev center
resource networkAttachment 'Microsoft.DevCenter/devcenters/attachednetworks@2023-04-01' = {
  parent: devCenter
  name: 'attached-network'

  properties: {
    networkConnectionId: networkConnection.id
  }
}

// Compute gallery for custom images
resource gallery 'Microsoft.Compute/galleries@2022-03-03' = {
  name: 'gal_devbox_images'
  location: location

  properties: {
    description: 'Custom dev box images'
  }
}
```

#### Step 2: Create Dev Box Definitions (Golden Images)

```bicep
// dev-box-definitions.bicep

// .NET Developer box
resource dotnetDevBox 'Microsoft.DevCenter/devcenters/devboxdefinitions@2023-04-01' = {
  parent: devCenter
  name: 'dotnet-developer'
  location: location

  properties: {
    imageReference: {
      // Use marketplace image or custom from gallery
      id: '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroup}/providers/Microsoft.Compute/galleries/${gallery.name}/images/vs2022-dotnet-azure/versions/1.0.0'
      // Or use marketplace:
      // offer: 'visualstudio2022'
      // publisher: 'microsoftvisualstudio'
      // sku: 'vs-2022-ent-general-win11-m365-gen2'
    }

    sku: {
      name: 'general_i_8c32gb256ssd_v2'  // 8 cores, 32GB RAM, 256GB SSD
    }

    osStorageType: 'ssd_256gb'
    hibernateSupport: 'Enabled'  // Save costs when not in use
  }
}

// High-performance developer box (for heavy workloads)
resource highPerfDevBox 'Microsoft.DevCenter/devcenters/devboxdefinitions@2023-04-01' = {
  parent: devCenter
  name: 'high-performance-developer'
  location: location

  properties: {
    imageReference: {
      id: '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroup}/providers/Microsoft.Compute/galleries/${gallery.name}/images/vs2022-dotnet-azure/versions/1.0.0'
    }

    sku: {
      name: 'general_i_16c64gb512ssd_v2'  // 16 cores, 64GB RAM
    }

    osStorageType: 'ssd_512gb'
    hibernateSupport: 'Enabled'
  }
}

// Data engineer box
resource dataEngineerBox 'Microsoft.DevCenter/devcenters/devboxdefinitions@2023-04-01' = {
  parent: devCenter
  name: 'data-engineer'
  location: location

  properties: {
    imageReference: {
      id: '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroup}/providers/Microsoft.Compute/galleries/${gallery.name}/images/python-datascience/versions/1.0.0'
    }

    sku: {
      name: 'general_i_8c32gb256ssd_v2'
    }

    hibernateSupport: 'Enabled'
  }
}
```

#### Step 3: Create Projects (Per Team)

```bicep
// project-team-api.bicep

resource project 'Microsoft.DevCenter/projects@2023-04-01' = {
  name: 'project-api-team'
  location: location

  properties: {
    devCenterId: devCenter.id
    description: 'API Team development project'
  }
}

// Dev box pool for the team
resource devBoxPool 'Microsoft.DevCenter/projects/pools@2023-04-01' = {
  parent: project
  name: 'api-team-developers'
  location: location

  properties: {
    devBoxDefinitionName: 'dotnet-developer'
    networkConnectionName: 'attached-network'
    licenseType: 'Windows_Client'  // or 'Windows_Server'

    localAdministrator: 'Enabled'  // Developers are local admins

    // Auto-stop schedule (cost savings)
    stopOnDisconnect: {
      status: 'Enabled'
      gracePeriodMinutes: 60  // Stop after 60 min of disconnect
    }
  }
}

// Assign developers to project
resource projectAccess 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
  scope: project
  name: guid(project.id, apiTeamGroup.id, 'DevCenter Dev Box User')

  properties: {
    roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', '45d50f46-0b78-4001-a660-4198cbe8cd05') // DevCenter Dev Box User
    principalId: apiTeamGroup.id  // Azure AD group for API team
  }
}
```

#### Step 4: Customize Images

**Using Packer to build custom images:**

```hcl
# devbox-image.pkr.hcl
packer {
  required_plugins {
    azure = {
      source  = "github.com/hashicorp/azure"
      version = "~> 1"
    }
  }
}

source "azure-arm" "devbox" {
  # Use marketplace base image
  image_publisher = "microsoftvisualstudio"
  image_offer     = "visualstudio2022"
  image_sku       = "vs-2022-ent-general-win11-m365-gen2"

  # Azure details
  subscription_id = var.subscription_id
  tenant_id       = var.tenant_id

  # Where to save
  managed_image_resource_group_name = "rg-devbox-images"
  managed_image_name                = "vs2022-dotnet-azure-v1.0.0"

  # VM specs for building
  vm_size = "Standard_D4s_v3"
  os_type = "Windows"

  # Output to Compute Gallery
  shared_image_gallery_destination {
    subscription        = var.subscription_id
    resource_group      = "rg-devbox-images"
    gallery_name        = "gal_devbox_images"
    image_name          = "vs2022-dotnet-azure"
    image_version       = "1.0.0"
    replication_regions = ["eastus", "westus2"]
  }
}

build {
  sources = ["source.azure-arm.devbox"]

  # Install tools
  provisioner "powershell" {
    inline = [
      # .NET SDKs
      "winget install Microsoft.DotNet.SDK.8",
      "winget install Microsoft.DotNet.SDK.6",

      # Azure tools
      "winget install Microsoft.AzureCLI",
      "winget install Microsoft.Bicep",

      # Development tools
      "winget install Git.Git",
      "winget install Docker.DockerDesktop",
      "winget install Microsoft.PowerShell",

      # VS Code extensions
      "code --install-extension ms-dotnettools.csharp",
      "code --install-extension ms-azuretools.vscode-bicep",
      "code --install-extension ms-vscode.powershell",

      # Configure git
      "git config --global core.autocrlf true",
      "git config --global credential.helper wincred"
    ]
  }

  # Configure Windows
  provisioner "powershell" {
    script = "./configure-windows.ps1"
  }

  # Sysprep (required for Azure)
  provisioner "powershell" {
    inline = [
      "& $env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /quiet /quit",
      "while($true) { $imageState = Get-ItemProperty HKLM:\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Setup\\State | Select ImageState; if($imageState.ImageState -ne 'IMAGE_STATE_GENERALIZE_RESEAL_TO_OOBE') { Write-Output $imageState.ImageState; Start-Sleep -s 10 } else { break } }"
    ]
  }
}
```

**Configure Windows script:**

```powershell
# configure-windows.ps1

# Disable unnecessary services
Set-Service -Name "DiagTrack" -StartupType Disabled  # Telemetry
Set-Service -Name "dmwappushservice" -StartupType Disabled

# Enable Windows features
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All -NoRestart
Enable-WindowsOptionalFeature -Online -FeatureName Containers -All -NoRestart

# Configure Windows Defender exclusions (for performance)
Add-MpPreference -ExclusionPath "C:\Users\*\source"
Add-MpPreference -ExclusionPath "C:\Program Files\Docker"

# Set power plan to High Performance
powercfg /setactive 8c5e7fda-e8bf-4a96-9a85-a6e23a8c635c

# Configure Nuget package sources
nuget sources Add -Name "CompanyNuGet" -Source "https://pkgs.dev.azure.com/company/_packaging/feed/nuget/v3/index.json"

# Pre-configure Azure DevOps
git config --global url."https://dev.azure.com/company/".insteadOf "https://dev.azure.com/company/"

# Install company certificates
Import-Certificate -FilePath "C:\Temp\CompanyRoot.cer" -CertStoreLocation Cert:\LocalMachine\Root

# Create standard folder structure
New-Item -ItemType Directory -Path "C:\Source" -Force
New-Item -ItemType Directory -Path "C:\Tools" -Force
```

### Developer Experience

#### Creating a Dev Box (Developer Self-Service)

**Via Azure Portal:**
1. Navigate to dev.microsoft.com/devbox
2. Click "New dev box"
3. Select project and pool
4. Name the dev box
5. Click "Create"
6. Wait 15-30 minutes
7. Connect via browser or RDP

**Via Azure CLI:**
```bash
# List available pools
az devcenter dev dev-box-pool list \
  --dev-center devcenter-platform \
  --project project-api-team

# Create dev box
az devcenter dev dev-box create \
  --dev-center devcenter-platform \
  --project project-api-team \
  --pool api-team-developers \
  --name "mydevbox" \
  --user-id "@me"

# Get connection info
az devcenter dev dev-box show-remote-connection \
  --dev-center devcenter-platform \
  --project project-api-team \
  --name "mydevbox" \
  --user-id "@me"
```

**Via PowerShell:**
```powershell
# Create dev box
New-AzDevCenterUserDevBox `
    -Endpoint "https://devcenter-platform-abc123.centralus.devcenter.azure.com/" `
    -ProjectName "project-api-team" `
    -PoolName "api-team-developers" `
    -Name "mydevbox"

# Start/stop dev box
Start-AzDevCenterUserDevBox -Endpoint $endpoint -ProjectName $project -Name "mydevbox"
Stop-AzDevCenterUserDevBox -Endpoint $endpoint -ProjectName $project -Name "mydevbox"
```

#### Connecting to Dev Box

**Browser (Windows 365 App):**
- Navigate to windows365.microsoft.com
- Click dev box
- Full desktop in browser
- No local RDP client needed

**Remote Desktop Client:**
- Download RDP file from portal
- Open with Remote Desktop client
- Full local integration
- Copy/paste, file transfer

**Mobile:**
- Remote Desktop app (iOS/Android)
- Access dev box from anywhere
- View-only or full control

### Cost Management

#### Auto-Shutdown Policies

```bicep
// Auto-shutdown to save costs
resource devBoxPool 'Microsoft.DevCenter/projects/pools@2023-04-01' = {
  properties: {
    // Stop on disconnect
    stopOnDisconnect: {
      status: 'Enabled'
      gracePeriodMinutes: 60  // After 60 min idle
    }

    // Scheduled shutdown
    schedules: [
      {
        name: 'weeknight-shutdown'
        type: 'StopDevBox'
        frequency: 'Daily'
        time: '19:00'  // 7 PM
        timeZone: 'Eastern Standard Time'
        state: 'Enabled'
      }
    ]
  }
}
```

#### Hibernation (Cost Savings)

**Hibernate vs Stop:**
- **Hibernate:** State saved, instant resume, still charged for storage
- **Stop:** Fully stopped, no charges, slower startup

```bicep
hibernateSupport: 'Enabled'  // In dev box definition
```

**Developers can:**
```bash
# Hibernate (saves state, faster resume)
az devcenter dev dev-box hibernate --name "mydevbox" --project project-api-team

# Stop (fully shutdown, no compute cost)
az devcenter dev dev-box stop --name "mydevbox" --project project-api-team
```

#### Cost Analysis

**Typical costs (East US, as of 2024):**
```
8 cores, 32GB RAM, 256GB SSD: ~$1.50/hour (~$260/month if always on)
16 cores, 64GB RAM, 512GB SSD: ~$3.00/hour (~$520/month if always on)

With hibernation/auto-shutdown (8 hours/day, 5 days/week):
8 core: ~$260/month → ~$65/month (75% savings)
```

**Cost optimization tips:**
- Auto-shutdown after hours
- Hibernate during lunch
- Delete unused dev boxes
- Right-size SKUs (don't over-provision)
- Use pooled environments for testing

### Best Practices

**For Platform Team:**
1. **Standardize images** - Fewer definitions to maintain
2. **Update regularly** - Monthly image updates
3. **Monitor costs** - Alert on high usage
4. **Security scanning** - Scan custom images
5. **Documentation** - Clear guides for developers
6. **Support model** - Office hours for dev box issues

**For Developers:**
1. **Hibernate when stepping away** - Save costs
2. **Delete when done** - Clean up old boxes
3. **Use appropriate SKU** - Don't overprovision
4. **Report issues** - Help improve images
5. **Keep data in cloud** - Azure Repos, OneDrive, etc.

### Integration with Platform

**Dev Box + Azure DevOps:**
```powershell
# Pre-configure in image
git config --global credential.helper manager-core

# Store PAT in Windows Credential Manager
cmdkey /generic:git:https://dev.azure.com/company `
       /user:PAT `
       /pass:$env:AZURE_DEVOPS_PAT

# Clone repos automatically on first login
git clone https://dev.azure.com/company/project/_git/repo C:\Source\repo
```

**Dev Box + Azure Resources:**
- Managed Identity for dev boxes
- Access Key Vault secrets
- Deploy to dev Azure subscriptions
- No credentials in code

**Dev Box + Defender:**
- Antimalware built-in
- Security updates automatic
- Policy enforcement
- Threat detection

---

## Part 2: Microsoft Defender for Cloud

### What is Microsoft Defender for Cloud?

**Unified security management and threat protection:**
- Security posture management (CSPM)
- Cloud workload protection (CWP)
- DevOps security
- Compliance dashboards
- Threat detection and response

**Covers:**
- Azure resources
- AWS resources
- GCP resources
- On-premises servers
- Hybrid/multi-cloud

### Architecture

```
Microsoft Defender for Cloud
├── Secure Score (Posture management)
│   ├── Security recommendations
│   ├── Compliance standards
│   └── Prioritized improvements
├── Workload Protections (Threat detection)
│   ├── Defender for Servers
│   ├── Defender for App Service
│   ├── Defender for SQL
│   ├── Defender for Storage
│   ├── Defender for Containers
│   ├── Defender for Key Vault
│   └── Defender for DevOps
└── Security Alerts (Incidents)
    ├── Alert investigation
    ├── Threat intelligence
    └── Response automation
```

### Enabling Defender for Cloud

#### Step 1: Enable at Subscription Level

```bicep
// defender-for-cloud.bicep

// Enable Defender for Cloud (free tier automatic)
resource defenderPricing 'Microsoft.Security/pricings@2023-01-01' = [for plan in [
  'VirtualMachines'           // Servers
  'AppServices'               // Web Apps
  'SqlServers'                // SQL Databases
  'SqlServerVirtualMachines'  // SQL on VMs
  'StorageAccounts'           // Storage
  'ContainerRegistry'         // Container registries
  'KubernetesService'         // AKS
  'KeyVaults'                 // Key Vaults
  'Arm'                       // Azure Resource Manager
  'Dns'                       // DNS
  'OpenSourceRelationalDatabases'  // PostgreSQL, MySQL
]: {
  name: plan
  properties: {
    pricingTier: 'Standard'  // Or 'Free' (limited features)
  }
}]

// Auto-provisioning (install agents automatically)
resource autoProvisioning 'Microsoft.Security/autoProvisioningSettings@2017-08-01-preview' = {
  name: 'default'
  properties: {
    autoProvision: 'On'
  }
}

// Email notifications
resource securityContact 'Microsoft.Security/securityContacts@2020-01-01-preview' = {
  name: 'default'
  properties: {
    emails: 'security-team@company.com'
    notificationsByRole: {
      state: 'On'
      roles: ['Owner']
    }
    alertNotifications: {
      state: 'On'
      minimalSeverity: 'High'
    }
  }
}
```

#### Step 2: Configure Security Policies

```bicep
// Assign security standards
resource azureSecurityBenchmark 'Microsoft.Security/policyAssignments@2021-06-01' = {
  name: 'ASC-AzureSecurityBenchmark'
  properties: {
    displayName: 'Azure Security Benchmark'
    policyDefinitionId: '/providers/Microsoft.Authorization/policySetDefinitions/1f3afdf9-d0c9-4c3d-847f-89da613e70a8'
    scope: subscription().id
  }
}

// PCI-DSS compliance (if needed)
resource pciDss 'Microsoft.Security/policyAssignments@2021-06-01' = {
  name: 'ASC-PCI-DSS'
  properties: {
    displayName: 'PCI-DSS v3.2.1'
    policyDefinitionId: '/providers/Microsoft.Authorization/policySetDefinitions/496eeda9-8f2f-4d5e-8dfd-204f0a92ed41'
    scope: subscription().id
  }
}
```

### Defender for DevOps

**Secure your Azure DevOps and GitHub:**

#### Enable DevOps Security

```bicep
// DevOps connector
resource devOpsConnector 'Microsoft.Security/securityConnectors@2023-01-01' = {
  name: 'connector-azure-devops'
  location: 'global'

  properties: {
    environmentName: 'AzureDevOps'
    offerings: [
      {
        offeringType: 'CspmMonitorAzureDevOps'  // Security posture
      }
    ]

    environmentData: {
      environmentType: 'AzureDevOpsScope'
      orgName: 'your-org'
      projectNames: ['*']  // All projects or specific
    }
  }
}
```

**What it scans:**
- **Code:** Secret scanning, IaC misconfigurations
- **Dependencies:** Vulnerable packages
- **Pipelines:** Security issues in YAML
- **Repos:** Security findings
- **Pull Requests:** Security annotations

**Integration with Azure DevOps:**

```yaml
# Azure Pipeline with Defender scanning
trigger:
  - main

steps:
  # Microsoft Security DevOps task
  - task: MicrosoftSecurityDevOps@1
    displayName: 'Security scanning'
    inputs:
      categories: 'IaC,secrets,dependencies,code'

  # Publish results to Defender for Cloud
  - task: PublishBuildArtifacts@1
    inputs:
      PathtoPublish: '$(Build.ArtifactStagingDirectory)/.gdn'
      ArtifactName: 'CodeAnalysisLogs'

# Results appear in Defender for Cloud portal
```

### Security Recommendations

**Defender analyzes your environment and provides recommendations:**

**Categories:**
- Enable MFA
- Encrypt storage accounts
- Update vulnerable software
- Enable firewall rules
- Configure network security groups
- Enable auditing
- Implement least privilege

**Example Bicep fix for recommendation:**

```bicep
// Recommendation: "Storage account should use private link"

// Before (public access)
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-01-01' = {
  name: 'stmydata'
  properties: {
    publicNetworkAccess: 'Enabled'  // ❌ Recommendation
  }
}

// After (private endpoint)
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-01-01' = {
  name: 'stmydata'
  properties: {
    publicNetworkAccess: 'Disabled'  // ✅ Secure
  }
}

resource privateEndpoint 'Microsoft.Network/privateEndpoints@2023-04-01' = {
  name: 'pe-storage'
  location: location
  properties: {
    subnet: {
      id: vnet.properties.subnets[0].id
    }
    privateLinkServiceConnections: [
      {
        name: 'storage-connection'
        properties: {
          privateLinkServiceId: storageAccount.id
          groupIds: ['blob']
        }
      }
    ]
  }
}
```

### Secure Score

**Gamified security posture:**
- Score out of 100%
- Each recommendation has points
- Fix recommendations to increase score
- Track progress over time
- Compare to industry benchmarks

**PowerShell to get score:**
```powershell
# Get secure score
$score = Get-AzSecuritySecureScore -Name "ascScore"
Write-Host "Current Secure Score: $($score.Score.Current)/$($score.Score.Max) ($($score.Score.Percentage)%)"

# Get recommendations
Get-AzSecurityAssessment | Where-Object {$_.Status.Code -eq "Unhealthy"} | Select-Object Name, Status, RecommendationSeverity
```

**Automation to remediate:**
```powershell
# Auto-remediate: Enable storage encryption
Get-AzStorageAccount | ForEach-Object {
    if ($_.Encryption.Services.Blob.Enabled -eq $false) {
        Set-AzStorageAccount `
            -ResourceGroupName $_.ResourceGroupName `
            -Name $_.StorageAccountName `
            -EnableBlobEncryption $true

        Write-Host "Enabled encryption for $($_.StorageAccountName)"
    }
}
```

### Security Alerts and Incidents

**Threat detection:**
- Brute force attacks
- Malware detected
- Suspicious PowerShell
- Crypto-mining
- Data exfiltration
- Privilege escalation

**Alert investigation:**
```powershell
# Get recent security alerts
Get-AzSecurityAlert `
    -ResourceGroupName "rg-production" |
    Where-Object {$_.State -eq "Active"} |
    Select-Object AlertDisplayName, Severity, CompromisedEntity

# Get alert details
$alert = Get-AzSecurityAlert -Name "alert-id"
$alert.ExtendedProperties  # Investigation details
```

**Automated response with Logic Apps:**

```json
// Logic App triggered by Defender alert
{
  "trigger": {
    "type": "When_an_Azure_Security_Center_Alert_is_created_or_triggered"
  },
  "actions": {
    "Send_alert_to_Slack": {
      "type": "Http",
      "inputs": {
        "method": "POST",
        "uri": "https://hooks.slack.com/services/...",
        "body": {
          "text": "🚨 Security Alert: @{triggerBody()?['AlertDisplayName']}"
        }
      }
    },
    "Create_incident_ticket": {
      "type": "ServiceNow_CreateIncident",
      "inputs": {
        "severity": "@{triggerBody()?['Severity']}",
        "description": "@{triggerBody()?['Description']}"
      }
    },
    "Isolate_VM_if_malware": {
      "type": "Condition",
      "expression": "@contains(triggerBody()?['AlertDisplayName'], 'Malware')",
      "actions": {
        "Update_NSG": {
          "type": "UpdateNetworkSecurityGroup",
          "inputs": {
            "denyAllInbound": true
          }
        }
      }
    }
  }
}
```

### Compliance Dashboards

**Built-in standards:**
- Azure Security Benchmark
- PCI-DSS
- ISO 27001
- NIST 800-53
- HIPAA
- SOC 2

**View compliance:**
```powershell
# Get compliance results
Get-AzSecurityRegulatoryComplianceStandard |
    Select-Object Name, State, PassedControls, FailedControls

# Get specific control details
Get-AzSecurityRegulatoryComplianceControl `
    -StandardName "Azure-Security-Benchmark" `
    -Name "IM-1"  # Identity Management control
```

### Integration with Platform

**Defender + Bicep modules:**
```bicep
// Bake security into modules

resource webApp 'Microsoft.Web/sites@2022-03-01' = {
  name: webAppName
  properties: {
    httpsOnly: true  // ✅ Defender recommendation
    siteConfig: {
      minTlsVersion: '1.2'  // ✅ Defender recommendation
      ftpsState: 'Disabled'  // ✅ Defender recommendation

      // Defender for App Service monitors this
      appSettings: [
        {
          name: 'WEBSITE_DEFENDER_ENABLED'
          value: 'true'
        }
      ]
    }
  }
}

// Diagnostic settings (Defender requirement)
resource diagnostics 'Microsoft.Insights/diagnosticSettings@2021-05-01-preview' = {
  scope: webApp
  name: 'defender-diagnostics'
  properties: {
    workspaceId: logAnalytics.id
    logs: [
      {
        category: 'AppServiceHTTPLogs'
        enabled: true
        retentionPolicy: {
          days: 90
          enabled: true
        }
      }
    ]
  }
}
```

**Defender + Azure DevOps Pipelines:**
```yaml
# Security gate before production deployment
stages:
  - stage: SecurityValidation
    jobs:
      - job: DefenderCheck
        steps:
          # Check Defender recommendations
          - task: AzurePowerShell@5
            inputs:
              azureSubscription: 'Platform-ServiceConnection-prod'
              ScriptType: 'InlineScript'
              Inline: |
                $unhealthy = Get-AzSecurityAssessment |
                  Where-Object {$_.Status.Code -eq "Unhealthy" -and $_.Status.Severity -eq "High"}

                if ($unhealthy.Count -gt 0) {
                  Write-Error "High severity security issues found. Fix before deploying."
                  exit 1
                }

  - stage: DeployProduction
    dependsOn: SecurityValidation
    # Only deploys if security validation passes
```

### Cost Considerations

**Pricing tiers:**

**Free tier:**
- Secure Score
- Basic recommendations
- Azure Policy integration
- Limited threat detection

**Standard tier (paid):**
- Advanced threat detection
- Just-in-time VM access
- Adaptive application controls
- File integrity monitoring
- Container security
- Multi-cloud support

**Typical costs (per resource/month):**
```
Defender for Servers: ~$15/server/month
Defender for App Service: ~$15/app/month
Defender for SQL: ~$15/server/month
Defender for Storage: ~$10/account/month
Defender for Containers: ~$7/vCore/month
Defender for DevOps: Free (preview)
```

**Cost optimization:**
- Enable only needed workload protections
- Use free tier for non-production
- Leverage DevOps security (currently free)
- Clean up unused resources

### Best Practices

**For Platform Team:**
1. **Enable at subscription level** - Centralized management
2. **Auto-provision agents** - Automatic protection
3. **Configure alerts** - Route to security team
4. **Regular review** - Weekly secure score checks
5. **Remediation automation** - Fix common issues automatically
6. **Compliance tracking** - Monthly compliance reports
7. **DevOps integration** - Security in pipelines

**For Development Teams:**
1. **Review recommendations** - Fix issues in your resources
2. **Scan code** - Use Defender for DevOps
3. **Fix secrets** - Don't commit credentials
4. **Update dependencies** - Patch vulnerable packages
5. **Follow golden paths** - Security built-in

### Monitoring and Reporting

**Weekly security report:**
```powershell
# Generate-SecurityReport.ps1

$report = @{
    SecureScore = (Get-AzSecuritySecureScore -Name "ascScore").Score.Percentage
    HighSeverityAlerts = (Get-AzSecurityAlert | Where-Object {$_.Severity -eq "High" -and $_.State -eq "Active"}).Count
    UnhealthyRecommendations = (Get-AzSecurityAssessment | Where-Object {$_.Status.Code -eq "Unhealthy"}).Count
    CompliancePercentage = (Get-AzSecurityRegulatoryComplianceStandard -Name "Azure-Security-Benchmark").PassedControls / $_.TotalControls * 100
}

# Email to security team
Send-MailMessage `
    -To "security-team@company.com" `
    -Subject "Weekly Security Report" `
    -Body "Secure Score: $($report.SecureScore)%`nHigh Severity Alerts: $($report.HighSeverityAlerts)" `
    -SmtpServer "smtp.office365.com"
```

**Defender workbook (Azure Monitor):**
```json
{
  "version": "Notebook/1.0",
  "items": [
    {
      "type": 3,
      "content": {
        "query": "SecurityAlert | summarize count() by AlertSeverity",
        "visualization": "piechart"
      }
    },
    {
      "type": 3,
      "content": {
        "query": "SecurityRecommendation | where RecommendationState == 'Active' | summarize count() by RecommendationSeverity",
        "visualization": "barchart"
      }
    }
  ]
}
```

## Integration: Dev Box + Defender

**Secure development environments:**

```bicep
// Dev Box with Defender protection

// Defender for Dev Box VMs
resource defenderForDevBox 'Microsoft.Security/pricings@2023-01-01' = {
  name: 'VirtualMachines'
  properties: {
    pricingTier: 'Standard'
    subPlan: 'P2'  // Includes advanced features
    extensions: [
      {
        name: 'MdeDesignatedSubscription'
        isEnabled: 'True'
      }
    ]
  }
}

// Dev boxes get automatic protection
resource devBoxDefinition 'Microsoft.DevCenter/devcenters/devboxdefinitions@2023-04-01' = {
  properties: {
    // Defender agent auto-installed
    // Threat detection enabled
    // Security policies applied
  }
}
```

**Benefits:**
- Malware protection on dev boxes
- Threat detection
- Security baseline enforcement
- Compliance monitoring
- Incident response

## Resources

### Documentation
- [ ] Azure Dev Box documentation
- [ ] Microsoft Defender for Cloud documentation
- [ ] Defender for DevOps guide
- [ ] Azure security best practices

### Training
- [ ] AZ-500 (Azure Security)
- [ ] Microsoft Learn: Defender for Cloud
- [ ] Microsoft Learn: Dev Box

### Tools
- [ ] Packer (image building)
- [ ] Azure CLI
- [ ] PowerShell Az module
- [ ] Defender APIs

---

[← Back to Practices](./README.md) | [← Back to Index](../README.md)
