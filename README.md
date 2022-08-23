<p align="center"><img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/raspberry_logo.png" height="100" alt=" " /></p>
<br>
<h1 align="center">Raspberry pi Guide</h1> 
<h4 align="right">Aug 22</h4>

<img src="https://img.shields.io/badge/OS%20-Raspbian%20GNU%2FLinux%2011%20(bulleye)-yellowgreen">
<img src="https://img.shields.io/badge/Hardware-Raspberry%20ver%203 & 4-red">

# How to Find your IP Address
test connection in the same net:
```
ping raspberrypi.local
```

# Ethernet MAC address
```
ethtool -P eth0
```

# Enabling SSH

Raspberry Pi OS has the SSH server disabled by default. It can be enabled manually from the desktop:

1. Launch Raspberry Pi Configuration from the Preferences menu
2. Navigate to the Interfaces tab
3. Select Enabled next to SSH
4. Click OK

Alternatively you can enable it from the terminal using the raspi-config application,

1. Enter sudo raspi-config in a terminal window
2. Select Interfacing Options
3. Navigate to and select SSH
4. Choose Yes
5. Select Ok
6. Choose Finish

# SSH Shell desde Linux, Mac o Windows OS
```
ssh pi@<IP>
ssh <USER>@<IP-ADDRESS> 
e.g. pi@192.168.1.10
e.g. eben@192.168.1.5
```
Next you will be prompted for the password for the pi login: the default password on Raspberry Pi OS is raspberry.

# Copying Files to your Raspberry Pi
```
scp myfile.txt pi@192.168.1.3:
```
Copy the file to the /home/pi/project/ directory on your Raspberry Pi (the project folder must already exist):
```
scp myfile.txt pi@192.168.1.3:project/
```
# Copying Files from your Raspberry Pi
Copy the file myfile.txt from your Raspberry Pi to the current directory on your other computer:
```
scp pi@192.168.1.3:myfile.txt .
```
# Copying Multiple Files
```
scp myfile.txt myfile2.txt pi@192.168.1.3:
scp *.txt pi@192.168.1.3:
scp m* pi@192.168.1.3:
scp m*.txt pi@192.168.1.3:
```

# Copying a Whole Directory
Copy the directory project/ from your computer to the pi user’s home folder of your Raspberry Pi at the IP address 192.168.1.3
```
scp -r project/ pi@192.168.1.3:
```

# DHCP Server
```
$ sudo apt-get install isc-dhcp-server
```
Modify the configuration in /etc/default/isc-dhcp-server
```
DHCPDv6_CONF=/etc/dhcp/dhcpd6.conf
INTERFACESv6="eth0"
```

In /etc/dhcp/dhcpd6.conf you need to specify the TFTP server address and setup a subnet. Here the DHCP server is configured to supply some made up unique local addresses (ULA). The host test-rpi4 line tells DHCP to give a test device a fixed address.
```
not authoritative;

# Check if the client looks like a Raspberry Pi
if option dhcp6.client-arch-type = 00:29 {
        option dhcp6.bootfile-url "tftp://[fd49:869:6f93::1]/";
}

subnet6 fd49:869:6f93::/64 {
        host test-rpi4 {
                host-identifier option dhcp6.client-id 00:03:00:01:e4:5f:01:20:24:0b;
                fixed-address6 fd49:869:6f93::1000;
        }
}

```
Your server has to be assigned the IPv6 address in /etc/dhcpcd.conf

```
interface eth0
static ip6_address=fd49:869:6f93::1/64
```

Now start the DHCP server.
```
$ sudo systemctl restart isc-dhcp-server.service
```
 revisar: https://www.raspberrypi.com/documentation/computers/remote-access.html#introduction-to-remote-access



# SERVICES
```
sudo systemctl enable systemd-networkd
sudo reboot

```




---
Copyright &copy; 2022 [carjavi](https://github.com/carjavi). <br>
```www.instintodigital.net``` <br>
carjavi@hotmail.com <br>
<p align="center">
    <a href="https://instintodigital.net/" target="_blank"><img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/developer.png" height="100" alt="www.instintodigital.net"></a>
</p>
