# winget

Windows package manager.

## Installation

Run PowerShell as Administrator:

    Set-PSRepository -N 'PSGallery' -InstallationPolicy Trusted  
    Install-Script -Name winget-install -Force  
    winget-install.ps1

