# Activity Log: She's Gotta Develop It
What am I making? 

_Log notes organized by date (most recent)_
<!---
<details><summary>template for entries</summary>

## Entry No. 00x
**Day xx/xx/xxxx**

</details>
--->
## Entry No. 009
**Tuesday 11/5/2019**

Backk to theming. I'm going to give Local by Flywheel a try... again. I'm using the Beta version for 5.something. I didn't know that this application was basically a Docker app, so that is pretty cool.

That said, because it stores things in `/mnt/c/users/username` I decided to create a symlink to that directory in my regular project folder because I don't use my Windows home directory. 

I used my own [tutorial](https://akudo.codes/2018/12/10/mklink-command-in-windows-ubuntu-wsl/) on creating cross-platform symlinks but ran into an issue when I tried to run my command using absolute paths.

```bash

pwd /mnt/c/myProjectFolder/localSites
$ mklink localSites /users/myUserAccount/localSites

```
That command would result in a broken symlink that looked like this `localSites -> /mnt/c/mnt/c/users/myUserAccount/localSites`. Not sure why it kept adding an extra `/mnt/c`. So after almost an entire hour of debugging, I tried this instead: `mklink localSites /users/myUserAccount/localSites` and it finally worked. Not sure why that is though. 

## Entry No. 008
**Monday 11/4/2019**

I decided to try out Local by Flywheel and I think I'm going to pass on that for now. Seems like it really makes things easier but having to store files in my Windows user directory is not the wave.

So I need to resume my previous activity of watching a video tutorial on how to get up & running with Vagrant & VCCW with WSL. 

Video: https://www.youtube.com/watch?v=W6Yp9PO7mr0

I manually added these settings to my `.bashrc` file so I don't need to type the command in each time. Lets see if it actually works. 

```bash
export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
export VAGRANT_WSL_WINDOWS_ACCESS_USER_HOME_PATH="/mnt/c/vvv" # this is modified home path because vagrant will fail if commands run in a directory is not the actual home directory
```

I think I'll try this again to set up the project I'm trying to set up.

I'm going through the steps for setting up vagrant with the help of some scripts again. Will recap at some point. 

## Entry No. 007
**Friday 11/1/2019**

So I'm working on my iTunes-sync script.

Back up: I never got around to finishing the migration of my site to a new host because the host is having issues with my SSL. 

Now back to the iTunes sync script. Access my project here:

I store my iTunes library on MyCloud so in order to run a script that can copy my library XML file, I'll need to have access to this Network Storage Device from the commandline. I can do that by mounting, which WSL apparently enables but I kept running into issues, which I figured out were a result of me only referencing my actual server and not the actual directory on the server.

The commands for mounting are:
```bash
sudo mkdir /mnt/music-library
sudo mount -t drvfs '\\server\myMusicCollection' /mnt/music-library # the issues I ran into occured when I only used \\server without adding the actual directory
```

I think created a symlink my home directory like this `ln -sf /mnt/music-library ~/music`.


New commands I've learned during this process:
```bash
sudo mount -a
mount -l # lists out the mounted drives with their "metadata"
```

Other important things worth noting: apparently, you're now able to access linux files from the Windows Explorer using this command in the HOME directory: `explorer.exe .`. And apparently you can manipulate the Linux files from Windows. Yes, my mind is blown now. More details [here](https://www.thurrott.com/windows/windows-10/199652/windows-10s-file-explorer-will-soon-let-you-access-your-linux-subsystem-files)

Anyway, what is next? I need to create a script that copies the file I have in my main library to a new location. 

The command I'm starting with is simple `cp itunes/"iTunes Library.xml" itunes/library-itunes12/`. I looked into other options like `rsync` and whether there are benefits to use that. I'd say, it doesn't seem like an issue to keep using `cp`. I did notice the program lagged while copying but it is a large file.

What I might also implement is a way to copy over the existing itunes12 library to the "Previous Libraries" folder as a backup. I think the library does that already, but it doesn't hurt to do it again :-). 

## Entry No. 006
**Thursday 10/31/2019**

Why does it feel like it's been so long since I did anything?? Today I'm migrating my blog to a new host, so mostly admin stuff. But decided to put together a easy breezy cheatsheet I can use whenever I have to do this, which is not often but sometimes you need to switch hosts.


## Entry No. 005
**Tuesday 10/22/2019**

Today I decided to read up on Jamstack. I don't think there are a lot of good explanations or articles making enough distinctions between it and other options. But I found some interesting stuff:
- https://itnext.io/why-building-with-a-jamstack-is-awesome-39696e9ef8d6
- https://bejamas.io/blog/jamstack/

My dive into JAMstack then led me into an exploration of __headless CMSs__. I'm interested enough to explore it for a project at some point. Sounds like it would allow you to maintain content the same way, using the admin dashboard & whatnot, but then I could use Nunjucks templating (or something else) to create layouts and render without being tied to the PHP templating options.

## Entry #004
**Monday 10/21/2019**
Ok I'm giving vagrant a spin, for real this time.

The issue I'm having right now is the `vagrant-hostsupdator` package won't install. I'm getting this error:  `timed out (https://gems.hashicorp.com/specs.4.8.gz)`

Found some issues on GH related to it: https://github.com/hashicorp/vagrant/issues/8795 but nothing to help me work around the issue. Luckily this is optional. So I'll keep it moving. Picking up where I left off and following this [video](https://www.youtube.com/watch?v=W6Yp9PO7mr0)...

*What I already did:*
- installed VirtualBox
- installed vagrant on Windows & in WSL, using the same version
- tested to see if vagrant was installed with `vagrant -v`. Things are looking good so far.


Following the tutorial, I decided to download the vagrant-wordpress starter scripts from (VCCW)[vccw.cc].
I downloaded those files into my project folder labeled `vagrant-starter`. And that was where I left off before today.


1. I need to modify my `hosts` file to add the IP address found in `default.yml`. I can do that from the command line, using a terminal with elevated Windows privileges: `nano /mnt/c/Windows/System32/drivers/etc/hosts`. No need for `sudo` because Windows does not care about that. 
2. I could also create an alias that would write to the `hosts` file

I ran into some permission issues and recalled this article, so I needed to set some environment variables:
```bash 
#  export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"
#  export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
#  export VAGRANT_WSL_WINDOWS_ACCESS_USER_HOME_PATH="/mnt/c/sgdi/vvv"

```

I had to `vagrant halt` and then `vagrant up` and then `vagrant provision` before the wordpress install was successful. Successful meaning the `vagrant up` command would terminate prematurely for reasons I don't know yet and when I checked the project folder, I didn't see any files in the wordpress directory which let me know the install was not successful yet.

Very excited that things worked out. 

Now let's see about configurations, turning this thing on again later this week and making some things with this fancy vagrant box.

## Entry #003
**Friday 10/18/2019**
I actually created a script for updating my hosts file LOL. Why am I like this?? It is here in my [github](https://github.com/shesgottadevelopit/wamp-vhost).

So I guess I can now focus on vagrant and doing all the stuff I did in WAMP in WSL without WAMP. 

Let me start with the WAMP stuff, the process for setting up a site in WAMP is something like this:
- add a vhost (there is a built-in mechanism for this but you can also add it manually) and this typically appears in `C:\wamp_directory\bin\apache\apache2.2.22\conf\extra\httpd-vhosts.conf`
- update host files, which is typically in `C:\windows\System32\drivers\etc\hosts`
- restart services
- the end

The process is a little different for WSL. When I was working on my lil script above about 9 months ago, I found a bunch of other scripts that basically do all the steps I outlined above. So I'm not about to do that exercise again, but I do want to understand whats happening and really walk through all the steps without automation, particularly for the WSL stuff. How does the WSL process differ from WAMP? 

**the hosts files**
in WSL, the host file is a mirror of Windows host file, so I won't need to worry about modifying that file. I'll only need to continue to modify the Windows one, which can be accessed through this path `/mnt/c/windows/System32/drivers/etc/hosts`.

**vhost conf locations & process**
- As for the vhost configuration. Apparently there are two key directories: `/etc/apache2/sites-enabled` and `/etc/apache2/sites-available`. Inside the latter is a `default.conf` file which resembles the `httpd-vhosts.conf` file for the WAMP environment. You would copy that default file and create a new file that will be associated with you new vhost. 
- For example, if we have a project stored in `/mnt/c/myprojects/site1` and we want to create a vhost for that project called `site1.local`. Then we'd created a config file and label it `site1.local.conf`. That file would live in `sites-available`. Inside the config file, we'd add all the important details I included above, like where to find projects files and what you want to refer to this project by. 
- Once you've saved that new file, you'll need to run this command: `sudo a2ensite site1.local.conf` which basically tells enables the new site in the `sites-enabled` directory. 
- Of course you'd need to update the hosts file (which I covered already) and then restart.

These are the scripts that allow you to automate this process and I'm looking forward to using them:
- https://github.com/RoverWire/virtualhost/blob/master/virtualhost.sh
- https://github.com/mattmezza/vhost-creator

This tutorial covers the WordPress part of it and how to integrate wp-cli: https://hellojason.net/blog/how-to-setup-wordpress-locally-on-windows-subsystem-for-linux/

**Final comments**
I tested it out and all works out fine. Things I could probably adjust in the script:
- the userDir
- the IP address being piped into the `hosts` file.

I guess it is time to move on to vagrant for real for real this time. I'll also need to figure out how to launch apache2 and mysql when I open the terminal because I always forget. 

## Entry #002
**Thursday 10/17/2019**
Started watching this tutorial: https://www.youtube.com/watch?v=W6Yp9PO7mr0
When he got to the `default.yml` file updates, I realized I'd need to make changes to the hosts.conf file on Windows and theres no easy way to do that. So I decided to try setting up an apache server via WSL and seeing if I can utilize their `hosts` mechanism instead.

I successfully installed the lamp stack, configured apache, mysql and phpmyadmin. I suppose this would also eliminate WAMP maybe??

I'd need to figure out a way to automate updates to this file: `/mnt/c/Windows/System32/drivers/etc/hosts`. Reading up on solutions: https://www.reddit.com/r/bashonubuntuonwindows/comments/65fav1/syncing_windows_hosts_file_to_etchosts/.

I haven't found a script for adding and removing entries in the host file so I may have to create one or update the one I have using these as inspiration:
- https://gist.github.com/markembling/173887/1824b370be3fe468faceaed5f39b12bad010a417
- https://tomssl.com/2019/04/30/a-better-way-to-add-and-remove-windows-hosts-file-entries/
  
Okay before I log off here is what I've got:
- I can modify the host script from WSL but I'll need to launch my terminal with elevated privileges in Windows to make sure I'm actually able to write the changes when I run the command and/or script. 
- Closest answer my question came from here: https://www.reddit.com/r/bashonubuntuonwindows/comments/9glbro/how_to_manage_administrator_permissions_with_wsl/


## Entry #001
**Wednesday 10/16/2019**
Spent the evening reading up on using vagrant for WordPress development. This way I don't need to worry about conflicts with package versioning, etc.

I installed VirtualBox and also Vagrant but didn't get anything up & running

