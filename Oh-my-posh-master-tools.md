# First Step - Use default usar (non admin) Powershell 7:

iwr -useb get.scoop.sh | iex

# Second Step - Add this line to system variable:

~\scoop\shims

# Third Step - Re-open Powershell 7 (non admin) and run this:

scoop install curl sudo jq neovim gcc fzf

# Four Step - Open Powershell 7 admin user and run this:

Set-ExecutionPolicy RemoteSigned
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser
Install-Module posh-git -Scope CurrentUser
Install-Module -Name PowerShellGet -Force 
Install-Module -Name PSReadline -AllowPrerelease -Scope CurrentUser -Force -SkipPublisherCheck
Install-Module -Name Terminal-Icons -Repository PSGallery
Install-Module PSFzf -Scope CurrentUser
Install-Module -Name Z -Force

# Optional Step - Module to Azure Tools
Install-Module Az.Accounts -Scope CurrentUser
Install-Module Az.Tools.predictor -Scope CurrentUser

# Optional Step - Install Powerlevel10k Theme or other theme (for user choice)
curl https://raw.githubusercontent.com/Kudostoy0u/pwsh10k/master/pwsh10k.omp.json --output pwsh10k.omp.json
Copy-Item -Path pwsh10k.omp.json -Destination $HOME

# Five Step - Create Powershell profile (admin user):

New-item -type file -force $profile
notepad $profile

# Six Step - Paste this line in new profile:

# Powershell default profile for Poweruser
Import-Module posh-git
Import-Module oh-my-posh
#Import-Module Az.Tools.Predictor
Set-PoshPrompt -Theme  ~/pwsh10k.omp.json

# Autocomplete, keybinds and history
Set-PSReadlineKeyHandler -Key Tab -Function MenuComplete
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward
Set-PSReadlineOption -HistorySearchCursorMovesToEnd

# Autosuggestions for PSReadline
Set-PSReadlineOption -ShowToolTips
Set-PSReadlineOption -PredictionSource History

# Terminal-Icons
Import-Module Terminal-Icons

# Fzf
Import-Module PSFzf
Set-PsFzfOption -PSReadLineChordProvider 'Ctrl+f' -PSReadLineChordReverseHistory 'Ctrl+r'

# Alias (Optional)
Set-Alias vim nvim
Set-Alias g git
Set-Alias ll ls
Set-Alias grep findstr
Set-Alias tig 'C:\Program Files\Git\usr\bin\tig.exe'
Set-Alias less 'C:\Program Files\Git\usr\bin\less.exe'

# Ultilities (Optional)
function which ($command) {
    Get-Command -Name $command -ErrorAction SilentlyContinue |
        Select-Object -ExpandProperty Path -ErrorAction SilentlyContinue
}

clear