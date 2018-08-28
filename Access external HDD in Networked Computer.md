### How to Access external HDD by Brows Network in Ubuntu

Samba is a file sharing system between all machine in a local network.This documentation describes the way to install samba and configuration to share file or folder from second HDD of your machine

### Step 1 - Install samba 
Installing samba both host and client.Open Terminal `(ctrl+alt+t)`, then type:

```
	sudo apt-get install samba
```
and press enter.

Now, Configuration in host machine

After installing samba push the following command in terminal and press enter:

```bash
	sudo smbpasswd -a <sambausername>
  # EX - sudo smbpasswd -a plab-9
```
Here `<sambausername>` means the `user name` for samba you want to create. Press enter. You will be asked to give a password for samba.

### Step 2 - Edit `smb.conf` file
Open the `/etc/samba/smb.conf` file with gedit or any other editor:

```bash
	sudo gedit /etc/samba/smb.conf
```
add the following section in `Share Definitions` part of `smb.conf` file:
```bash
[foldername]
   comment = Accesing 2HDD
   path = /path/to/the/folder/you/want/to/share/of/second/hdd
   available = yes
   valid users = <sambausername>
   read only = no
   browseable = yes
   guest ok = yes
   public = yes
   writable = yes
```
*N.B.:* Here `foldername` is the folder you want to share and `<sambausername>` is the user name that was given by you. Save `smb.conf` and close it.

### Step 3 - Rstart samba
Now you should restart samba by entering the following command in terminal:
```bash
	sudo service samba restart
```
### Step 4 - Check installation 
Finally check everything by entering the following command in terminal:
```bash
	testparm
```

### Setp 5 - Browsing file or folder from client machine

- First browse <Network> from nautilus, then enter `WindowsNetwork/WORKGROUP/HostNameOfTheMachineYouWantToLook/`

- Second you can see the folder you want to access, click it, it show a window like,
			

![alt text](https://github.com/lab-semantics/Quick-Configuration/blob/master/img/samba_login.png)


Fill the username and password by the `<sambausername>` and `<sambapassword>` of host machine and click connect.


