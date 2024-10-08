
# **A Step-by-Step Guide to Opening VS Code via Right-Click in Linux**
	
<br>

<p align="center">
  <img alt="full stack" src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*Nb8Lo_BFJZxu6n0r8JHkkg.png">
</p>

<br>

This post is for those using Linux. If you’re using Linux for programming, Visual Studio Code is an essential code editor. While it’s easy to right-click on the relevant project folder and open it with VS Code, on Windows, it’s a simple task. However, in Linux distributions, you have to add this functionality manually. So, this post explains how to add a VS Code shortcut to the right-click menu in Linux distributions. By the way, this method works specifically for Debian-Gnome-based distributions (e.g., Ubuntu, Debian, Linux Mint, Zorin OS, Fedora) and this method will work on any Linux distribution that meets these criteria:

	

 - Uses GNOME as the desktop environment

 
	

 - Uses Nautilus (GNOME Files) as the file manager

	

 - Has the necessary Python bindings for Nautilus installed


Let’s Start the guide.

**1.First, open the terminal (Ctrl+Alt+T). Then paste this command and press Enter (Ctrl+Shift+V)**
-   For Debian-based distributions (ex : Ubuntu, Linux Mint, Zorin OS), run this:

    

> `sudo apt install python3-nautilus`

-   For Fedora (GNOME and Nautilus) users, run this:

> `sudo dnf install nautilus-python`

**2.Next, paste the following command and press Enter:**

>     mkdir -p ~/.local/share/nautilus-python/extensions   
>     nano ~/.local/share/nautilus-python/extensions/open_in_vscode.py
**3.Now, paste the following code into the open editor in the terminal (Ctrl+Shift+V) and save it (Ctrl+X then press “y” and Enter ) :**
> 
>     import os  
>     import subprocess  
>     from gi.repository import Nautilus, GObject
>     
>     class OpenVSCodeExtension(GObject.GObject, Nautilus.MenuProvider):  
>     def __init__(self):  
>     pass
>     
>     def menu_activate_cb(self, menu, file):  
>     filename = file.get_location().get_path()  
>     subprocess.Popen([‘code’, ‘ — new-window’, filename])
>     
>     def get_file_items(self, window, files):  
>     if len(files) != 1:  
>     return  
>       
>     file = files[0]  
>     if file.is_directory():  
>     item = Nautilus.MenuItem(  
>     name=”OpenVSCodeExtension::OpenVSCode”,  
>     label=”Open in VS Code”,  
>     tip=”Open the selected folder in a new Visual Studio Code window”  
>     )  
>     item.connect(‘activate’, self.menu_activate_cb, file)  
>     return [item]
>     
>     def get_background_items(self, window, file):  
>     item = Nautilus.MenuItem(  
>     name=”OpenVSCodeExtension::OpenVSCode”,  
>     label=”Open with VS Code ”,  
>     tip=”Open the current folder in a new Visual Studio Code window”  
>     )  
>     item.connect(‘activate’, self.menu_activate_cb, file)  
>     return [item]

**4.Alright, the task is complete. Now restart the file manager:**

> nautilus -q

**5.Open the file manager and right-click to see if it works .Thank you..!**


