# Organizing

To keep things simple on a Windows machine I try to compile to single binaries and deploy to one directory seperated by subfolders

Directory: `c:\MyPrograms`

![[Pasted image 20230506165009.png]]

# Deploying

I love Jetbrains products and since I'm only locally deploying to my machine, I have build configurations to build and copy these binaries. I want things to be simple and easy. Here are some examples for .NET and GoLang:

![[Pasted image 20230506165208.png]]

![[Pasted image 20230506165239.png]]

# Running

If I need to run something ad-hoc, of course I can `cd` to their respective directories and invoke them. I typically have a http api though that needs to be running on startup. I use shortcuts in the Windows startup folder to accompish this:

1. `ctrl + r`
2. `shell:startup`
3. Right click, new, shortcut
4. Choose the `exe` to run

![[Pasted image 20230506165612.png]]

# Accessing Over The Internet

TODO