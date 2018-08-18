### Suggested Steps for semi-automated install of prerequisites
#### Boxstarter - install Windows features
- Open PowerShell session as Administrator
#### Install other prerequisites and tools 
- Create a working directory
	```PowerShell
	md c:\projects
	Set-Location c:\projects
	```

- Download packages.config from repository

	```PowerShell
	Invoke-WebRequest -Uri https://raw.githubusercontent.com/Sitecore/Sitecore.HabitatHome.Utilities/master/Prerequisites/packages.config -UseBasicParsing | set-content packages.config
	```

- Install Chocolatey

    ```PowerShell
    Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
    ```
- Review packages.config to ensure it matches what you'd like to install
- Install prerequisites and tools using chocolatey
    `choco install packages.config -y`

- Set the password and enable the SA user (assumes current user has admin privileges)
> You may need to specify the instance name using the -S .\<InstanceName> if you aren't using a default SQL Server instance or if you're using SQLExpress
> Ensure you've installed SQL Server with Mixed Mode authentication (or enable it)

	Install-Module -Name SqlServer
	$saPassword = "SUPERS3CR3T!!"
	$instanceName = "your-instance-name"
	Invoke-sqlcmd -Query $("ALTER LOGIN [sa] WITH PASSWORD=N'" + $saPassword + "'") -ServerInstance $instanceName
	Invoke-sqlcmd -Query "ALTER LOGIN [sa] ENABLE" -ServerInstance $instanceName


### RESTART COMPUTER

- Clone the [Sitecore.HabitatHome.Utilities](https://github.com/Sitecore/Sitecore.HabitatHome.Utilities/) repository

	```PowerShell
	git clone https://github.com/Sitecore/Sitecore.HabitatHome.Utilities.git
	```

See the [README.md](../XP/install/README.md) in the XP/install folder

	
