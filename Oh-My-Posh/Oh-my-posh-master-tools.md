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
copy and paste profile.
