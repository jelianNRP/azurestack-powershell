<!-- region Generated -->
# Azs.Update.Admin
This directory contains the PowerShell module for the UpdateAdmin service.

---
## Status
[![Azs.Update.Admin](https://img.shields.io/powershellgallery/v/Azs.Update.Admin.svg?style=flat-square&label=Azs.Update.Admin "Azs.Update.Admin")](https://www.powershellgallery.com/packages/Azs.Update.Admin/)

## Info
- Modifiable: yes
- Generated: all
- Committed: yes
- Packaged: yes

---
## Detail
This module was primarily generated via [AutoRest](https://github.com/Azure/autorest) using the [PowerShell](https://github.com/Azure/autorest.powershell) extension.

## Authentication
AutoRest does not generate authentication code for the module. Authentication is handled via Az.Accounts by altering the HTTP payload before it is sent.

## Development
For information on how to develop for `Azs.Update.Admin`, see [how-to.md](how-to.md).
<!-- endregion -->

## Generation Requirements
Use of the beta version of `autorest.powershell` generator requires the following:
- [NodeJS LTS](https://nodejs.org) (10.15.x LTS preferred)
  - **Note**: It *will not work* with Node < 10.x. Using 11.x builds may cause issues as they may introduce instability or breaking changes.
> If you want an easy way to install and update Node, [NVS - Node Version Switcher](../nodejs/installing-via-nvs.md) or [NVM - Node Version Manager](../nodejs/installing-via-nvm.md) is recommended.
- [AutoRest](https://aka.ms/autorest) v3 beta <br>`npm install -g autorest@beta`<br>&nbsp;
- PowerShell 6.0 or greater
  - If you don't have it installed, you can use the cross-platform npm package <br>`npm install -g pwsh`<br>&nbsp;
- .NET Core SDK 2.0 or greater
  - If you don't have it installed, you can use the cross-platform npm package <br>`npm install -g dotnet-sdk-2.2`<br>&nbsp;

## Run Generation
In this directory, run AutoRest:
> `autorest`

---
### AutoRest Configuration
> see https://aka.ms/autorest

``` yaml
require:
  - $(this-folder)/../readme.azurestack.md
  - $(repo)/specification/azsadmin/resource-manager/update/readme.azsautogen.md

metadata:
  description: 'Microsoft AzureStack PowerShell: Update Admin cmdlets'

subject-prefix: ''
module-version: 1.0.1
service-name: UpdateAdmin

### File Renames
### IMPORTANT - Note that the following settings are case sensitive ###
module-name: Azs.Update.Admin
csproj: Azs.Update.Admin.csproj
psd1: Azs.Update.Admin.psd1
psm1: Azs.Update.Admin.psm1
sanitize-names: true
```

### Parameter default values
``` yaml
directive:
  - where:
      parameter-name: UpdateLocation
    set:
      parameter-name: Location
  - where:
      parameter-name: ResourceGroupName
    set:
      default:
        script: -join("System.",(Get-AzLocation)[0].Location)
  - where:
      verb: Add
    set:
      verb: Install
  - where:
      verb: Invoke
      subject: RerunUpdateRun
    set:
      verb: Resume
      subject: UpdateRun
  - where:
      subject: Update 
      parameter-name: Location
    clear-alias: true
  - where:
      subject: Update 
      parameter-name: Name
    clear-alias: true
  - where:
      subject: UpdateLocation 
      parameter-name: Location
    set:
      parameter-name: Name
      default:
        script: (Get-AzLocation)[0].Location
  - where:
      subject: (.*)Run$
      parameter-name: RunName
    set:
      parameter-name: Name
    # Hide the auto-generated Get-AzsUpdateRun and Resume-AzsUpdateRUn and expose it through customized one
  - where:
      subject: UpdateRun
    hide: true
    # Hide the auto-generated Get-AzsUpdateRunTopLevel. This will effectively remove the commandlet since we dont have a customized one
  - where:
      subject: UpdateRunTopLevel
    remove: true
    # Hide the auto-generated Install-AzsUpdate and Get-AzsUpdate and exposte it through customized one
  - where:
      subject: Update
    hide: true
    # Format Output Values
  - where:
      model-name: Update
    set:
      format-table:
        properties:
          - Location
          - DisplayName
          - Name
          - State
          - Publisher
        width:
          Location: 15
          DisplayName: 30
          Name: 40
          State: 20
          Publisher: 15
  - where:
      model-name: UpdateLocation
    set:
      format-table:
        properties:
          - Name
          - CurrentVersion
          - CurrentOemVersion
          - State
        width:
          Name: 20
          CurrentVersion: 20
          CurrentOemVersion: 20
          State: 20
  - where:
      model-name: UpdateRun
    set:
      format-table:
        properties:
          - Name
          - State
          - ProgressStartTimeUtc
          - ProgressEndTimeUtc
        width:
          Name: 40
          State: 15
          ProgressStartTimeUtc: 25
          ProgressEndTimeUtcate: 25

# Add release notes
  - from: Azs.Update.Admin.nuspec
    where: $
    transform: $ = $.replace('<releaseNotes></releaseNotes>', '<releaseNotes>AzureStack Hub Admin module generated with https://github.com/Azure/autorest.powershell.</releaseNotes>');

# Add Az.Accounts/Az.Resources as dependencies
  - from: Azs.Update.Admin.nuspec
    where: $
    transform: $ = $.replace('<dependency id="Az.Accounts" version="2.2.3" />', '<dependency id="Az.Accounts" version="[2.2.8]" />\n      <dependency id="Az.Resources" version="[0.11.0]" />');

# PSD1 changes for RequiredModules
  - from: source-file-csharp
    where: $
    transform: $ = $.replace('sb.AppendLine\(\$@\"\{Indent\}RequiredAssemblies = \'\{\"./bin/Azs.Update.Admin.private.dll\"\}\'\"\);', 'sb.AppendLine\(\$@\"\{Indent\}RequiredAssemblies = \'\{\"./bin/Azs.Update.Admin.private.dll\"\}\'\"\);\n      sb.AppendLine\(\$@\"\{Indent\}RequiredModules = @\(@\{\{ModuleName = \'Az.Accounts\'; RequiredVersion = \'2.2.8\'; \}\}, @\{\{ModuleName = \'Az.Resources\'; RequiredVersion = \'0.11.0\'; \}\}\)\"\);');

# PSD1 changes for ReleaseNotes
  - from: source-file-csharp
    where: $
    transform: $ = $.replace('sb.AppendLine\(\$@\"\{Indent\}\{Indent\}\{Indent\}ReleaseNotes = \'\'\"\);', 'sb.AppendLine\(\$@\"\{Indent\}\{Indent\}\{Indent\}ReleaseNotes = \'AzureStack Hub Admin module generated with https://github.com/Azure/autorest.powershell\'\"\);' );
```
