
I browsed to check if there are any best practices listed on what is possibly the right way to setup ones computer for this course and also to be able to use it all later on. I could not find much material.

Working as a IT professional in Infrastructure projects, I have found it helpful to contain a software or set of software's to a particular machine in such a way that it would not cause harm elsewhere.
Virtualbox is one such software which helps play with software fearlessly, I have been using it over many years.
It lets you create VirtialMachines (VMs) through by allotting diskspace, ram etc from your laptop/desktop.

Advantages:
1. All the software you will install on this VM will be contained in the VM, won't mess with your laptop/desktop. So any number of Install/Un-install, trail and error will cause no damage outside of the VM.
2. It can be backed up, shipped to other machines and used conveniently (no installations required on the other machine, share it..)
3. There is a feature in VirtualBox named 'snapshot' if you have to install series of software and perform multiple configurations in between, it is safe to keep taking snapshots after every milestone is achieved, that is like an insurance, if you happen to screw-up in the next step there is always the good snapshot to go back to.
4. Operating system is not a limitation, you don't like one, use another, yes there are multitude of OS that one could install in a VirtualBox VM.
5. The list goes on...

Download VirtualBox from here:
https://www.virtualbox.org/wiki/Downloads
I have created a VM with 2Cpu's, 4G Ram. Initially I tried Ubuntu but did not like it that much, One of the limitations was Hard Disk it was limited to around 8G, which means I have to add another hard disk and use fdisk to get it working etc.
Instead I used Centos, you can get it here:
http://virtualboxes.org/images/centos/
Scroll to the end and pick the latest version, you will get a torrent file, I guess you know how to use a torrent file, there is utorrent, transmission, bittorent many software which could help you use the torrent file and download the file you are interested in.
After downloading just double click the .ova file, it will open up in VirtualBox software, follow the instructions, in couple of mintues you will have a live and kicking centos to play with.

After the Centos is available for use:
1. I added an extra ethernet card, so that I can use eth0 for internet (NAT) and eht1 (host only adapter) for local lan (meaning I can work from Mac using iterm, putty if windows box).
2. Enabled port sharing for 8787 for local machine, so your local machine will start listening to 8787. (this is the default port for RStudio).
3. Installed "R", it is so damn easy:
Refer here for full details: http://www.jason-french.com/blog/2013/03/11/installing-r-in-linux/
tl;dr here:
$ sudo su -
(password is reverse)
$ rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
$ sudo yum update
$ sudo yum install R

Thats it, see it is so easy, you don't have to hunt the website to download a software or to update it etc, YUM will do it all for you.

Likewise install Rstudio:
_________________________
$ yum install wget
refer to full details here: https://www.rstudio.com/products/rstudio/download-server/
tl;dr here:
$ wget https://download2.rstudio.org/rstudio-server-rhel-0.99.484-x86_64.rpm
$ sudo yum install --nogpgcheck rstudio-server-rhel-0.99.484-x86_64.rpm

Now turn the IPTables off:
$ chkconfig iptables off

Create a OS user, I used the name ruser, here is how you do that:
$ sudo su -
(password is reverse)
$ mkdir -P /home/ruser
$ useradd ruser
$ chown -R ruser:ruser /home/ruser
Assign a password to the new user:
$ passwd ruser
(Remember the password you type there, no problem if you forget you can always come back, issue the same command and reset it)

On your Laptop/Desktop go to http://localhost:8787
Login as ruser password is what you entered in the last step.

How to shutdown your VM:
$ shutdown -h now
How to reboot:
$ reboot
If you don't like the fact that the VirtualBox starts up the VM in its own dedicated window, you can start it headless, hold the shift key and double click on the VM name in the left panel in virtual box. This wont bring up a dedicated window (console) of the VM, but you can connect to it remotely from your Laptop/Desktop.
If you are using a Mac, go to iterm and do this:
ssh root@<ip of the vm>
If you are using windows, download putty and connect to the VM.

How do you check IP of your VM:
$ ifconfig -a
look for 'eth1' you would have assigned 192.168.x.x (I can't tell what x in your case would be).

Now its all merry.

ps:
--12Sep2015:
I am adding these few lines based on receiving some of the initial comments:
If you are a novice to the world of computer, it might be a bit difficult for you to understand or implement what is mentioned here.
But if you are interested and take it further, try what is written here, you will safe tons of time in future and reap the benefits of being able to do, re-do, undo and share your work globally.

If you are not a novice, you already know how to install/un-install software and have experienced the changes a software installation causes to your computer, you will appreciate the manner in which this article saves you from the headache of backing up your entire system in order to restore from a damage that you might have accidentally caused.

The practices mentioned here will bring you back even from a point of no return :))