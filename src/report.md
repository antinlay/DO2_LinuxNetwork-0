# DO2 Linux Network
## Part 1. ipcalc tool
### 1.1. Networks and Masks
#### 1) Network address of 192.167.38.54/13 
![1.1.1](../misc/images/report_img/1.1.1.png)
#### 2) Conversion of the mask 255.255.255.0 to prefix and binary, /15 to normal and binary, 11111111.11111111.11111111.11110000 to normal and prefix
![1.1.2](../misc/images/report_img/1.1.2.png)
#### 3) Minimum and maximum host in 12.167.38.4 network with masks:
* /8

![1.1.3.1](../misc/images/report_img/1.1.3.1.png)

* 11111111.11111111.00000000.00000000

![1.1.3.2](../misc/images/report_img/1.1.3.2.png)

* 255.255.254.0

![1.1.3.3](../misc/images/report_img/1.1.3.3.png)

* /4

![1.1.3.4](../misc/images/report_img/1.1.3.4.png)

### 1.2. localhost
#### Define and write in the report whether an application running on localhost can be accessed with the following IPs:
IP localhosts on ranges [127.0.0.1 - 127.255.255.254]
|IP|ACCESS|
|--|----|
|194.34.23.100|FALSE|
|127.0.0.2|TRUE|
|127.1.0.1|TRUE|
|128.0.0.1|FALSE|

### 1.3. Network ranges and segments
#### Define and write in a report:
#### 1) which of the listed IPs can be used as public and which only as private: 10.0.0.45, 134.43.0.2, 192.168.4.2, 172.20.250.4, 172.0.2.1, 192.172.0.1, 172.68.0.2, 172.16.255.255, 10.10.10.10, 192.169.168.1
|Private range|10.0.0.0 – 10.255.255.255|172.16.0.0 – 172.31.255.255|192.168.0.0 – 192.168.255.255|
|-|-|-|-|

[Difference private and public IP](https://www.geeksforgeeks.org/difference-between-private-and-public-ip-addresses/)
|PUBLIC|PRIVATE|
|------|-------|
|134.43.0.2|10.0.0.45|
|172.0.2.1|192.168.4.2|
|192.172.0.1|172.20.250.4|
|172.68.0.2|172.16.255.255|
|10.10.10.10|192.169.168.1|

#### 2) which of the listed gateway IP addresses are possible for 10.10.0.0/18 network: 10.0.0.1, 10.10.0.2, 10.10.10.10, 10.10.100.1, 10.10.1.255
Access IP range: 10.10.0.1 - 10.10.63.254
![1.1.4.2](../misc/images/report_img/1.1.4.2.png)

|IP|ACCESS|
|------|-------|
|10.0.0.1|FALSE|
|10.10.0.2|TRUE|
|10.10.10.10|TRUE|
|10.10.100.1|FALSE|
|10.10.1.255|TRUE|

## Part 2. Static routing between two machines
#### Start two virtual machines (hereafter -- ws1 and ws2 View existing network interfaces with the ip a command
![2.1.1](../misc/images/report_img/2.0.1.png)

* enp0s3 name interface for ws1 and ws2

#### Describe the network interface corresponding to the internal network on both machines and set the following addresses and masks: ws1 - 192.168.100.10, mask */16 *, ws2 - 172.24.116.8, mask /12

`sudo nano etc/netplan/00-installer-config.yaml`
* ws1:

![2.0.2](../misc/images/report_img/2.0.2.png)

* ws2:

![2.0.3](../misc/images/report_img/2.0.3.png)

`sudo netplan apply`

* ws1:

![2.0.4](../misc/images/report_img/2.0.4.png)

* ws2:

![2.0.5](../misc/images/report_img/2.0.5.png)

### 2.1. Adding a static route manually

* ws1:

`sudo ip r add 172.24.116.8 dev enp0s3`
`sudo ping 192.168.100.10`

![2.1.1](../misc/images/report_img/2.1.1.png)

* ws2:

`sudo ip r add 192.168.100.10 dev enp0s3`
`sudo ping 172.24.116.8`

![2.1.2](../misc/images/report_img/2.1.2.png)

### 2.2. Adding a static route with saving

* ws1:

![2.2.1](../misc/images/report_img/2.2.1.png)

* ws2:

![2.2.2](../misc/images/report_img/2.2.2.png)