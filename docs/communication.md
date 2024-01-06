# Node's Communication

## Infrastructure mode and communication
Infrastructure-based networks rely on a centralized infrastructure, typically consisting of routers, access points, and base stations. Devices in these networks connect to this fixed infrastructure to communicate with each other and access resources. The centralized nature of the infrastructure allows for better management, scalability, and reliability, making these networks ideal for scenarios where a consistent and managed network is essential.

### Fix static ip in the wireless interface of the pi’s

Enter into dhcpcd.conf 

``` bash
    sudo nano /etc/dhcpcd.conf
```
Add the static configurations
Example:

``` bash
    interface wlan0
    static ip_address=192.168.1.101/24
    static routers=192.168.1.1
    static domain_name_servers=192.168.1.1
```
* Ping and show the network is reachable.
* Write UDP client socket program to sending and receiving the messages 
* Exchage the sensor collected values

## Ad Hoc mode and communication
Ad hoc networks are decentralized and dynamic communication systems that form spontaneously without the need for a pre-existing infrastructure. In ad hoc networks, devices communicate directly with each other, allowing for quick and flexible connectivity in scenarios where a centralized infrastructure is impractical or unavailable. Ad hoc networks are well-suited for situations such as emergency response, military operations, or temporary gatherings, where the ability to establish a network on-the-fly is crucial.

### Adhoc setup

* Check your device the configuration and communication mode using ifconfig and iwconfig
* Setup raspberry pi wireless interface to ad-hoc mode

Modify interface file

```bash
 /etc/network/interfaces
```
```bash
    auto lo
    iface lo inet loopback
    
    auto eth0
    iface eth0 inet dhcp

    auto wlan0
    iface wlan0 inet static
    address 10.1.1.1
    netmask 255.255.255.0
    wireless-channel 5
    wireless-essid VANET
    wireless-mode ad-hoc
```
[Download the configuration file from here.](https://drive.usercontent.google.com/u/1/uc?id=1CShhOWfbWg19sD1HuZv_AYr8HQThXh_W&export=download)

+ <span style="color:red">
 Don't forget change the IP address of the node.
</span>

+ Reboot the device after configuration.

+ Check the change in communication mode using iwconfig


### Communication between adhoc nodes
 * Write socket program to communicate between the nodes
 * Exchange the the position information
 * Write code to for periodic becon message
