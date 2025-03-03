# A-Setup on mikrotik

You need install and enable container on Mikrotik

## 1. Create VETH Interface

First, create a VETH interface with the following IP address and gateway:

```
/interface veth add name=veth1 address=192.168.34.3/24 gateway=192.168.34.1
```

## 2. Create and Configure Bridge

Create a bridge named `docker` and add the VETH interface to the bridge port:

```
/interface bridge add name=docker
/interface bridge port add bridge=docker interface=veth1
```

## 3. Configure Firewall Rules

Add firewall rules to allow connections to the container:

```
/ip firewall filter add chain=forward action=log protocol=tcp dst-port=2222 log-prefix="SSH_Traffic"
/ip firewall filter add chain=forward action=accept protocol=tcp dst-address=192.168.34.3 dst-port=22 log=no log-prefix="" comment="Allow_Container_Forward"
```

## 4. Configure NAT

Set up NAT to forward connections from MikroTik's port 2222 to port 22 of the container:

```
/ip firewall nat add chain=dstnat protocol=tcp dst-port=2222 action=dst-nat to-addresses=192.168.34.3 to-ports=22
```

## 5. Initialize Container

Initialize a container using the `phusion/baseimage:jammy-1.0.0` image, configure it to use the previously created VETH interface, and set it to start automatically at boot:

```
/container add remote-image=phusion/baseimage:jammy-1.0.0 interface=veth1 start-on-boot=yes
```

## B. Start and setup on container

After completing the above steps, you can start container and connect to the container via SSH through port 2222 of the MikroTik.
You need to access that container directly to install the necessary components.
```
/container/shell 0
```
0 is the id of the newly created container, if you already have previous containers, then you have to find the id of the newly created container 

## Once you have access to the container, install the necessary and important components for your ubuntu
```
apt install -y sudo
```
and
```
apt update && apt install -y curl wget ufw openssh-server git vim net-tools htop build-essential
```
Once done create a user for your virtual machine, because you can not ssh with the root account. SSH is already installed in the above command so you can ssh from other devices
```
ssh -p 2222 user@mikrotik_ip_address
```
[Create User on Ubuntu](https://github.com/x1-2023/phusion-mikrotik/blob/main/user.md)
## Notes

- Ensure that the container service is enabled on the MikroTik
- You may need to restart the device to apply some changes
- Check logs if you encounter connection issues: `/log print`



## References
- [Create User on Ubuntu](https://github.com/x1-2023/phusion-mikrotik/blob/main/user.md)
- [MikroTik Container Documentation](https://help.mikrotik.com/docs/display/ROS/Container)
- [MikroTik Firewall and NAT](https://help.mikrotik.com/docs/display/ROS/Firewall+and+QoS)
