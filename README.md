# kubernets-install
Install kubernets
Debian pc in master node and kali and two ubuntu **pc** **will** be worker node.  
    
    
    debian pc ip 192.168.1.5
    ubuntuone ip 192.168.1.2
    ubuntutwo ip 192.168.1.3
    kali      ip 192.168.1.4
    
## ***Set up hostsname***    

Change host name from ```/etc/hosts``` to rename an ip human readable format like ```192.168.1.4 kali```

Now we can ping ```192.168.1.4``` using name like ping kali from any network pc, in network pc will should apply this method.  
Need to  `sudo swapoff -a` run all pc master and worder node to off the the swap memeory.
It will temporarily off swap memeory. To off the swap memory permanently we should run this command.

    `sudo sed -i '/swap/s/^/#/' /etc/fstab`
This mean when pc resteart its see fstab which progrma should run but above command swap memory program will commnet it. So it will run on swap memory.

To check the swap memory status run this command `sudo swapon --show `

Then set hostname by command line or manually.
command line:  

    sudo hostnamectl set-hostname "your-expected-name-here"

Then to verify run this command:  
    
    exec bash



