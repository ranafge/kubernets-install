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

Install ```containerd``` in all node as well as master node using  
 
     sudo apt isntall containerd
Check the status using ``` sudo systemctl status containerd``` command if not then run these commands.

    sudo systemctl enable containerd
    sudo systemctl start containerd

Then create ```sudo mkdir /etc/containerd ``` in the all nodes.


    containerd config default | sudo tee /etc/containerd/config.toml

Create ```config.toml``` with the ``` containerd config default ``` settings in   ``` /etc/containerd/``` folder in the all nodes.

Then restart

    sudo systemctl restart containerd

Then need to configure ``` /etc/containerd/config.toml```

    [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
    SystemdCgroup = true
Because K8s wants to use System Control group.

After that edit ```sudo nano /etc/sysctl.conf``` for forward ip packet forward betweens k8s network.

    sudo nano /etc/sysctl.conf
    net.ipv4.ip_forward=1


If the file is not exist then create the file.

Create another file ```sudo nano /etc/modules-load.d/k8s.conf```
and edit
    
    br_netfilter

In Kubernetes, when pods communicate with each other or with the outside world, this module ***(br_netfilter)*** helps in forwarding the packets. After that reboot system using

    sudo reboot


The next step is the install he packages that are required for Kubernetes. First, we’ll add the required GPG key:

    sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://
    packages.cloud.google.com/apt/doc/apt-key.gpg

After that, install the packages that are required for Kubernetes:

    sudo apt install kubeadm kubectl kubelet