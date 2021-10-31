# rancher-os
# rancher-os installation steps

    1. Download RancherOS ISO.
    2. Upload the iso to local pve storage.
    3. Add new VM with RancherOS ISO as CD. Give it at least 3gb ram to start. Rancher Server failed with low ram
    Boot.
    4. Boot from CD.
    5. Change rancher user password in terminal:   (need to ssh)
    #sudo bash
    #passwd rancher
    6. Add non persistent IP address to existing network interface:
    #ifconfig eth0 10.10.10.1 netmask 255.255.255.0 up
    #ip a
    7. Generate your ssh keys with putty gen or ssh-keygen linux.
    8 .Prepare your cloud-config file with next parameters:
# cloud-config.yml
    

    7. SSH rancher@10.10.10.1
    vi cloud-config.yml

    Copy-paste the cloud-config edited with your settings, make sure the pasted data is pated correctly, add your key in a single line
    press exit exit :wq to save


