
#####	Đọc file chứa các gói tin

<img src="https://camo.githubusercontent.com/de5b2a8f78c1b7d0a8f9e3d055e9273b7fd6a9bd/687474703a2f2f692e696d6775722e636f6d2f3277694853745a2e706e67 />

- Đọc file chứa các gói tin lớn hơn 1 kích cỡ cho sẵn
	 
```
$ tcpdump -r filename.pcap greater 'size'
```

Ví dụ:

```
root@ubuntu:~# tcpdump -r cap_tcpdump.pcap greater 128
reading from file cap_tcpdump.pcap, link-type EN10MB (Ethernet)
22:13:17.997440 IP6 fe80::a12e:2592:be84:e696.dhcpv6-client > ff02::1:2.dhcpv6-server: dhcp6 solicit
```

- Đọc file chứa các gói tin nhỏ hơn 1 kích cỡ cho sẵn

```
$ tcpdump -r filename.pcap less 'size'
```

Ví dụ:

```
root@ubuntu:~# tcpdump -r cap_tcpdump.pcap less 128
reading from file cap_tcpdump.pcap, link-type EN10MB (Ethernet)
22:13:17.669209 IP6 fe80::a12e:2592:be84:e696.49300 > ff02::1:3.hostmon: UDP, length 22
22:13:17.669275 IP6 fe80::a12e:2592:be84:e696.55047 > ff02::1:3.hostmon: UDP, length 22
22:13:17.669544 IP 192.168.0.6.55047 > 224.0.0.252.hostmon: UDP, length 22
22:13:17.669575 IP 192.168.0.6.49300 > 224.0.0.252.hostmon: UDP, length 22
22:13:18.007332 IP 192.168.0.6.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
22:13:18.758076 IP 192.168.0.6.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
```
	 
#####	Bắt các gói tin với địa chỉ IP thông qua tcpdump –n

<img src="https://camo.githubusercontent.com/cea5c6513120a8d041eabe7ebd8ed5b1922237eb/687474703a2f2f692e696d6775722e636f6d2f783566486f446a2e706e67" />

#####	Bắt theo protocol

Bắt theo các gói TCP (Có thể là ARP, UDP, ICMP,... )

<img src="https://camo.githubusercontent.com/4748c12820907982dd24438caf88a83c201f5726/687474703a2f2f692e696d6775722e636f6d2f4659616f4b75322e706e67" />

Ví dụ về bắt gói ARP

<img src="https://camo.githubusercontent.com/b2e827d9348e1378e5a373597e52345597182d8f/687474703a2f2f692e696d6775722e636f6d2f3374336f63694f2e706e67" />

#####	Bắt các gói theo port

Ví dụ Port 22

<img src="https://camo.githubusercontent.com/f359d28546a33e34fcf47f5cd3302bc1463f7d4b/687474703a2f2f692e696d6775722e636f6d2f316a634563537a2e706e67" />

#####	Bắt theo địa chỉ nguồn hoặc đích

Theo địa chỉ nguồn:

<img src="https://camo.githubusercontent.com/8ad58497317817c791d00548d6e59b50fd9bef9b/687474703a2f2f692e696d6775722e636f6d2f794f7477664d322e706e67" />

Theo địa chỉ đích:

<img src="https://camo.githubusercontent.com/09bccaf73778146ded762d059efb4c977a0561bd/687474703a2f2f692e696d6775722e636f6d2f303168386f684d2e706e67 />

#####	Kết hợp bắt gói tin với nhiều điều kiện

Dưới đây là ví dụ, bắt 10 gói tin theo UDP hoặc TCP sử dụng Port 53 (DNS)

<img src="http://i.imgur.com/c26Xuhy.png" />

*Lưu ý: Trong lệnh tcpdump bạn có thể kết hợp các tùy chọn và sử dụng điều kiện “and”, “or” hoặc “not” để lọc các gói tin.*
