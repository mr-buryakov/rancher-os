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
    #cloud-config

    hostname: rancheros
    rancher:
      console: debian
      network:
        interfaces:
          eth0:
            address: 10.6.131.30/25
            gateway: 10.6.131.1
            mtu: 1500
            dhcp: false
        dns:
          nameservers:
          - 10.6.131.146
          - 8.8.4.4  	  
    write_files:
      - path: /etc/rc.local
        permissions: "0755"
        owner: root
        content: |
          #!/bin/bash
          apt-get -y update
          apt-get -y install python
    ssh_authorized_keys:
      - ssh-rsa AAAABM7p7G........o77vsFONVPgfutxAgIGzLVw==
# rancher-os installation steps

    9. SSH rancher@10.10.10.1
    10. vi cloud-config.yml
    Copy-paste the cloud-config edited with your settings, make sure the pasted data is pated correctly, add your key in a single line
    press esc :wq to save
    11. Validate the config file:
    #sudo ros config validate -i cloud-config.yml
    12.Apply it:
    #sudo ros install -c cloud-config.yml -d /dev/sda
    13. Remove CD Image from VM, and then reboot.
    14. SSH back into RancherOS (rancher@) using your new ssh private key
    __________________________________________________________________________________
    Some of configurations you can apply after rancher OS already configured and installed:
    1. Network parameters may be changed with:
    #sudo ros config set rancher.network.interfaces.eth0.address 10.6.131.30/25
    #sudo system-docker restart network
    #ip a
    

