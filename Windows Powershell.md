# POWERSHELL

---

**Powershell RTFM**

Everybody needs a little help at one time or another. In this exercise we will check how you can get help on powershell and how you can find interesting commands following your needs.

- Open a PowerShell session in your terminal : Windows button, then search "powershell", launch powershell with admin right
- type `Get-Help`
- Find out what a command such as `Get-Process` does without looking on google
- Now try with the `-online` parameter
- What does `Get-command`?
  	`It show you all the command available on your device`

Optionally:

- Try to get help on common commands such as `ls`, `cp`, `mv`, ...

# Powershell Navigation

Now we will learn how to move around in the filesystem with `Set-Location`, `Get-Location`, `Get-ChildItem` ...

- Print your current location on the screen
	-`get-location` or `gl`
- Print the content of your current directory
	-`get-childitem` or `gci` or `ls`
- Print the content of your root (`C:` _if you're running windows_, `/` _for linux_)
	-`'ls /' or 'gci /' or 'get-childitem /'`
- Go into your home folder (_C:\Users\Username or /home/Username_)
	-`set-location /users/username` or `sl users/username`
- Print the content of your home
	-`ls /users/home/ or gci or get-childitem`
- Those commands are pretty long to type, do you know any shorter way to do it?
	-`ls` for `get-childitem`
	-`sl` for `set-location`
	-`gl` for `get-location`

# Powershell File Operations

Now that we know how to move in the file system, let's check how to manipulate files and folders. In this challenge, you will discover and use the commands `Get-Content`, `echo`, `New-Item`, `Move-Item`, `Copy-Item`, and `Remove-Item`.

- Create a file named story1.txt
	-`new-item (or 'ni') story1.txt`
- Type `echo "Hello World" > story1.txt`
- Print the content of the file
	-`'get-content' or 'gc' story1.txt`
- Create a folder named `story`
	-`'mkdir story'`
- Move `story1.txt` inside `story`
	-`mv story1.txt story`
- Copy `story1.txt` as `story2.txt`
	-`cp story1.txt story2.txt`
- Print both files
	-`gc ./story1.txt
	`>> gc ./story2.txt 
- Rename `story2.txt` as `me.txt`
	-`mv story2.txt me.txt (in the same directory)`
- Append `me.txt` and add "I am a junior at Becode"
	-`echo "I am a junior at becode" >> ./me.txt
- Remove the folder story with it's content
	-`remove-item -recurse ./story`

# Powershell Permissions

Now that we can navigate and create files, we should be able to change permissions on these. We will use the commands `Get-Acl`, `Set-Acl`, `RunAs`

- Create a file
	-`new-item permission.txt`
- Check the owner and the groups
	-`get-acl permission.txt`
- Change the file owner to the built-in administrator
	-`takeown /F permssion.txt /A`
- Check the file's permission
	-`get-acl permission.txt`
- Try to print the content of the file as your normal user
	-`get-content permission.txt`
- Print the content of the file using administrator account
	-`get-content permission.txt`
# Powershell Package Management

It's time to start installing softwares and keep them updated. We will see how to use Chocolatey and how to use Windows Updates.

- Get Windows updates
    - Install the `PSWindowsUpdate` module
	    -`install-package pswindowsupdate`
    - Type `Get-WindowsUpdate` to check for updates
    - Type `Install-WindowsUpdate` to install updates
- Manage Packages
    - Install `Chocolatey`
	    -`chocolatey --install`
    - Install `VLC` from `Chocolatey`
	    -`choco install vlc`
    - Upgrade `VLC` to the latest version (it should already be but it's your first use)
	    -`choco upgrade vlc`
    - Remove the `VLC` package using `Chocolatey`
	    -`choco uninstall vlc`
    - Could you use `Chocolatey` on already installed software? How?
	    -`choco (upgrade) , (uninstall) , *name of the sofware*`
- Manage Windows Features
    - Get installed windows features with the command `Get-WindowsOptionalFeature` (for win 10 and below)
	    -`Get-WindowsOptionalFeature -Online | Where-Object {$_.State -eq "Enabled"} | Select-Object FeatureName, DisplayName, State
`

# Powershell Environment Variables

In any programming language you can store data within variables. However they only exist as long as the program is executed, but what if you wanted to share information between two applications not running at the same time.

Then you could use environment variables, which are variables stored at the OS level. You can access them from anywhere.

- Open a Powershell Terminal
- Type `echo $env:computername`. It should show your computer name
- Create a variable by typing `$env:test = "hello powershell"`
- Check the variable you just created the same way you did with the computer name
  
	-`echo $env:test `

- Now we will add something to this variable by typing `$env:test += " Becode"`
- Check the variable

	-`echo $env:test `

- There is one really important environment variable : `$env:path`. This variable store the location where windows looks for files that are not in your current folder. For example, if you call VSCode from the powershell terminal, it opens it even if the executable isn't present in the current folder. That's because the path to the vscode's executable is stored in `$env:path`. Now download an executable software ([rufus](https://github.com/pbatard/rufus/releases/download/v3.13/rufus-3.13p.exe) for example) and copy it on your desktop. If you try from a command line to launch it, it will fail with a command not found (if you are not in the same folder).
- Try to happen the $env:path to add the path to rufus' executable (It should be something like this if you copied it on your desktop : 
  
	-`C:\Users\Username\Desktop`)

- Try to call rufus from anywhere
- I would like you to have a look at [the recognized environment variables available on windows](https://docs.microsoft.com/en-us/windows/deployment/usmt/usmt-recognized-environment-variables).
- Write a small script reporting your computer specs and convert it in a csv file. You might have some trouble executing your script once saved. Why? How can you change it in a secure way?

	-`When you run PowerShell scripts that involve system-related operations, such as retrieving computer specs, you might encounter security restrictions, especially if the execution policy is set to a restrictive level. PowerShell's execution policy determines which scripts can be run on a system. By default, PowerShell execution policy is set to "Restricted," which prevents running scripts. To execute your script safely, you can change the execution policy temporarily or use a signing mechanism to digitally sign your script. Here's how you can do it securely:`.

