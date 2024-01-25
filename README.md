# boxsetup

## Why?
On this post, I am showing how I am setting up my dev environment in a way that I can restore it at any moment.
Of course this does not fit all as we all have different Os and different set of favourite tools so adjust. 

## How?
Using Chocolatey & BoxStarter.
Why? To have fully automated and repeateable installations that can be deployed in local, virtual or remote environments. Also only on windows systems.
More on this on (why Chocolatey)[https://chocolatey.org/why-chocolatey] and (why BoxStarter)[https://boxstarter.org/WhyBoxstarter]. 
Essentially, save Time, Complexity and reduce cost. But, mostly, time.

Official websites:
- [Chocolatey official site](https://chocolatey.org/)
- [BoxStarter](https://boxstarter.org/)


## Let's get it done
1.  First things first - Install Chocolatey
    - First, you need to install Chocolatey. You can do that by running the scripts [found here](https://chocolatey.org/install). After you do that, you can start using Chocolatey to install applications. If you have some trouble you can follow the [more detailed instructons here](https://chocolatey.org/docs/development-environment-setup).
    - Once installed, we can check that it works by opening PowerShell and issuing a chocolatey command such as `choco install vlc`. Note we will need an elevated (aka admin enabled) powershell for this and further chocolatey commands. We should see a prompt like: 
<IMG  src="https://i.octopus.com/blog/2019-08/automate-developer-machine-setup-with-chocolatey/choco-install-vlc-start.png"/>
Which is a bit bothersome, but avoidable adding the `-y` in our command, so let's do that again. We type  `choco install vlc -y`.

   - To update we should use upgrade instead of install, such as:        
  `choco upgrade vlc -y`
2.  Install BoxStarter.  
    After Chocolatey we can proceed to install BoxStarter, we can use PowerShell or choco for this as it makes it more simpler. Just type from an administrative commandline:  `choco install boxstarter`   

1. Create the script
   Next we can create the Installation script, it is basically made of PowerShell with some Chocolatey commands. 
We can create it as a single text file or any text based HTTP resource (like a Github Gist)[https://gist.github.com/].
Should look like:   
```
Set-WindowsExplorerOptions -EnableShowHiddenFilesFoldersDrives -EnableShowProtectedOSFiles -EnableShowFileExtensions
Enable-RemoteDesktop

choco install vlc
choco install 7-Zip
....
```
    

4. Run the script   
   Once created and reviewed, we can go and execute it from an elevated (read, with Administrator permissions) command prompt.  
   Invoke the the `Install-BoxstarterPackage` command pointing to the gist created above. For this we will need the RAW link to the GIST script content. In our case it would look like:  `Install-BoxstarterPackage -PackageName boxstarter_newdev_script.txt -DisableReboots`   
   Note that I used the `-DisableReboots`  option as it is stated on the BoxStarter example, but BoxStarter runs from an elevated prompt and can handle reboots and continue with the installation tasks completely unnatended..



## References used:   
 - https://octopus.com/blog/automate-developer-machine-setup-with-chocolatey
 - https://boxstarter.org/Learn/WebLauncher
 - https://boxstarter.org/
 - https://devblogs.microsoft.com/cesardelatorre/automating-windows-environments-setup-with-boxstarter-and-chocolatey-packages/
 - http://www.hanselman.com/blog/scott-hanselmans-2014-ultimate-developer-and-power-users-tool-list-for-windows
