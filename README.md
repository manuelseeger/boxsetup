# boxsetup

## Why?
On this post, I am showing how I am setting up my dev environment in a way that I can restore it at any moment.

## How?
Using Chocolatey & BoxStarter.
Why? To have fully automated and repeateable installations that can be deployed in local, virtual or remote environments. Also only on windows systems.
More on this on (why Chocolatey)[https://chocolatey.org/why-chocolatey] and (why BoxStarter)[https://boxstarter.org/WhyBoxstarter]. 
Essentially, save Time, Complexity and reduce cost. But, mostly, time.

Official websites:
- [Chocolatey official site](https://chocolatey.org/)
- [BoxStarter](https://boxstarter.org/)

## Let's get it done
1.  First things first - Install Chocolatey https://chocolatey.org/install
1.  Install powertoys. https://github.com/microsoft/PowerToys/
1.  Set PowerToys Awake to awake indefinitely. This is so that your laptop does not go to sleep / standby while boxstarter is running. 
1.  Install BoxStarter.  
    Just type from an administrative commandline:  `choco install boxstarter`   
1. Create the script
   Next we can create the Installation script, it is basically made of PowerShell with some Chocolatey commands. 

    Should look like:   
    ```
    Set-WindowsExplorerOptions -EnableShowHiddenFilesFoldersDrives -EnableShowProtectedOSFiles -EnableShowFileExtensions
    Enable-RemoteDesktop
    choco install vlc
    choco install 7-Zip
    ....
    ```
1. Run the script   
   Once created and reviewed, we can go and execute it from a new, elevated (read, with Administrator permissions) command prompt. We might need to import the choco boxstarter module:
   ```
   Set-ExecutionPolicy Bypass -Scope Process
   Import-Module Boxstarter.Chocolatey
   ```
   Invoke the `Install-BoxstarterPackage` command pointing to the install script created above. In our case it would look like:  `Install-BoxstarterPackage -PackageName boxstarter_script.txt -DisableReboots`

## References used:   
 - https://octopus.com/blog/automate-developer-machine-setup-with-chocolatey
 - https://boxstarter.org/Learn/WebLauncher
 - https://boxstarter.org/
 - https://devblogs.microsoft.com/cesardelatorre/automating-windows-environments-setup-with-boxstarter-and-chocolatey-packages/
 - http://www.hanselman.com/blog/scott-hanselmans-2014-ultimate-developer-and-power-users-tool-list-for-windows
