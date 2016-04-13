# DarkBoot

This should enable the black boot screen + white Apple logo on Macs running 10.11 (OS X El Capitan).

![Preview](example.png)

### Information:
This method uses your Mac's built-in NVRAM to specify the background you seen when you
boot up your Mac. For reasons that I have yet to identify, your Mac resets this background
value to the default value sometime during the boot process. In order to combat
this, I created a daemon that is run automatically by the Mac process launchd during boot
time.

In order to edit the NVRAM (aka use the /usr/sbin/nvram command), you need have to have
root privileges. This means that we need to use a Global Daemon instead of a User Daemon.

To learn more about launchd, LaunchDaemons, and LaunchAgents, check out http://launchd.info
which has an excellent explanation. They're pretty simple yet incredibly powerful.

### How to use:

Copy the com.dabrain13.darkboot.plist file into your /Library/LaunchDaemons folder.

If you want, you can do that in terminal. So assuming the file is in your Downloads folder:

mv ~/Downloads/com.dabrain13.darkboot.plist /Library/LaunchDaemons/

Then you need to let launchd know that you want this to be run every time you boot:

sudo launchctl load /Library/LaunchDaemons/com.dabrain13.darkboot.plist
	
Note: because we are installing a Daemon and NOT an agent, we must use sudo to call launchctl.

And you're done! Reboot (you may have to reboot twice) and you should see your Mac 
boot with the black boot screen.

### To Uninstall:

If you want to go back to your default boot screen, just run:

sudo launchctl unload /Library/LaunchDaemons/com.dabrain13.darkboot.plist

and remove the com.dabrain13.darkboot.plist file from the /Library/LaunchDaemons/ 
directory.
	
### License:
The MIT License (MIT)
Copyright (c) 2016 dabrain13

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.