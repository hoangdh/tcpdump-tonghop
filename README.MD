## Tổng quan về tcpdump

#### 1.	Khái niệm

`tcpdump` là phần mềm bắt gói tin trong mạng, làm việc trên hầu hết các phiên bản hệ điều hành Unix/Linux. Nó có thể bắt và lọc các gói tin TCP/IP được truyền trên mạng qua card mạng nào đó. `tcpdump` có tùy chọn để lưu ra file và đọc bằng công cụ đồ họa Wireshark.

#### 2.	Cài đặt

Để sử dụng được lệnh tcpdump trên Linux, chúng ta phải cài một gói với tên tương tự.

Ở Ubuntu, ta dùng lệnh

```
sudo apt-get install tcpdump -y
```

Với CentOS

```
yum install tcpdump -y
```

Hoặc có thể vào trang <a href="http://www.tcpdump.org/#latest-release" >tcpdump</a> để tải mã nguồn của công cụ này.

#### 3.	Cấu trúc câu lệnh

```
tcpdump [ -AbdDefhHIJKlLnNOpqStuUvxX# ] [ -B buffer_size ] [ -c count ]
```

##### Một số tùy chọn

| Tùy chọn | Mô tả |
|----------|-------|
| -A | Hiển thị các gói tin dưới dạng mã ACSII |
| -b | In số AS trong các gói tin BGP trong ký hiệu ASDOT hơn là ký hiệu ASPLAIN |
| -B size | Cài đặt buffer_size |
| -c | Thoát sau khi nhận được số lượng gói tin |
| -D | Liệt kê ra tất cả các interface đang hiện hữu trên máy có thể capture được |
| -e | Thay thế hiển thị địa chỉ IP của người gửi và người nhận bằng địa chỉ MAC |
| -i | Bắt gói tin từ một giao diện ethernet cụ thể |
| -q | Hiển thị ít thông tin hơn |
| -n | Không phân giải từ địa chỉ IP sang hostname|
| -L | Hiển thị danh sách các datalink type mà interface hỗ trợ |
| -N | Không in các quality domain name ra màn hình |
| -s | Định nghĩa snaplength (kích thước) gói tin sẽ lưu lại, sử dụng 0 để mặc định |
| -v | Tăng số lượng thông tin về gói tin có thể nhận được, thậm chí có thể tăng thêm với option –vv hoặc –vvv |
| -t | Bỏ qua thời gian bắt được gói tin khi hiển thị |
| -tt | Thời gian hiển thị trên mỗi dòng lệnh sẽ không được format theo dạng chuẩn |
| -ttt | Thời gian hiển thị chính là thời gian chênh lệnh giữa thời gian tcpdump bắt được gói tin của gói tin và gói tin đến trước |
| -tttt | Hiển thị thêm ngày vào mỗi dòng lệnh |
| -ttttt | Thời gian hiển thị trên mỗi dòng chính là thời gian chênh lệch giữa thời gian tcpdump bắt được gói tin của gói tin hiện tại và gói tin đầu tiên |
| -x | Hiển thị dữ liệu của gói tin capture dưới dạng mã Hex |
| -xx | Tương tự option –x tuy nhiên sẽ chuyển đổi cả Ethernet header |
| -X | Hiển thị dữ liệu của gói tin dưới dạng mã Hex và ASCII |
| -y | Lựa chọn datalinktype khi bắt các gói tin |

#### 4.	Một số bộ lọc cơ bản

- `dst A`: Khi sử dụng option này, tcpdump sẽ chỉ capture các gói tin có địa chỉ đích là “A”, có thể sử dụng kèm với từ khóa net để chỉ định một dãy mạng cụ thể. Ví dụ: tcpdump dst net 192.168.1.0/24.
- `src A`:Tương tự như option dst, nhưng thay vì capture các gói tin có địa chỉ đích cụ thể thì nó sẽ capture các gói tin có địa chỉ nguồn như quy định.
- `host A`: Khi sử dụng option này, tcpdump sẽ chỉ capture các gói tin có địa chỉ nguồn hoặc địa chỉ đích là “A”.
- `port / port range`: Khi sử dụng option này, tcpdump sẽ chỉ capture các gói tin có địa chỉ port được chỉ định rõ, hoặc nằm trong khoảng range định trước. Có thể sử dụng kèm với option dst hoặc src.
- `less`: Khi sử dụng từ khóa này, tcpdump sẽ lọc (filter) các gói tin có dung lượng nhỏ hơn giá trị chỉ định.
- `greater`: Khi sử dụng từ khóa này, tcpdump sẽ lọc (filter) các gói tin có dung lượng  cao hơn giá trị chỉ định.
- `(ether | ip) broadcast`: Capture các gói tin ip broadcast hoặc ethernet broadcast.
- `(ether | ip | ip6) multicast`: Capture các gói tin ethernet, ip , ipv6 multicast.
- Ngoài ra, tcpdump còn có thể capture các gói tin theo các protocol như : `udp, tcp, icmp, ipv6`  (chỉ cần gõ trực tiếp các từ khóa vào là được). Ví dụ: tcpdump icmp


#### 5.	Sử dụng – ví dụ
#####	Xem các Interface đang hoạt động

```
tcpdump -D
```

<img src="http://i.imgur.com/wTtQFpe.png" />

#####	Bắt gói tin trên Interface

```
tcpdump -i <tên-interface>
```

Ví dụ, bắt gói tin trên card `enp0s3`

<img src="http://i.imgur.com/5VuEOwf.png" />

Bấm tổ hợp phím `Ctrl` + `C` để dừng.

Sau khi ta dừng, sẽ hiện ra một bảng với các thông số:

- **Packet capture**: số lượng gói tin bắt được và xử lý.
- **Packet received by filter**: số lượng gói tin được nhận bởi bộ lọc.
- **Packet dropped by kernel**: số lượng packet đã bị dropped bởi cơ chế bắt gói tin của hệ điều hành.


##### Định dạng chung của một dòng giao thức tcpdump là:

```
time-stamp src > dst:  flags  data-seqno  ack  window urgent options
```

Tên trường | Mô tả |
--- | --- |
Time-stamp | hiển thị thời gian gói tin được capture. |
Src và dst | hiển thị địa IP của người gửi và người nhận. |
Cờ Flag| S(SYN):  Được sử dụng trong quá trình bắt tay của giao thức TCP.</br>.(ACK):  Được sử dụng để thông báo cho bên gửi biết là gói tin đã nhận được dữ liệu thành công.</br>F(FIN): Được sử dụng để đóng kết nối TCP.</br>P(PUSH): Thường được đặt ở cuối để đánh dấu việc truyền dữ liệu.</br>R(RST): Được sử dụng khi muốn thiết lập lại đường truyền. |
Data-sqeno | Số sequence number của gói dữ liệu hiện tại. |
ACK | Mô tả số sequence number tiếp theo của gói tin do bên gửi truyền (số sequence number mong muốn nhận được). |
Window | Vùng nhớ đệm có sẵn theo hướng khác trên kết nối này. |
Urgent | Cho biết có dữ liệu khẩn cấp trong gói tin. |


#####	Giới hạn số lượng gói tin

<img src="https://camo.githubusercontent.com/eaef1cc891146c8fabe4ec19f72cc5de91eeda59/687474703a2f2f692e696d6775722e636f6d2f46537a546554342e706e67" />

#####	Hiển thị dạng ASCII của gói tin bắt được

<img src="https://camo.githubusercontent.com/2b4877da907dad04e9f72515110fb84a7ce6e24b/687474703a2f2f692e696d6775722e636f6d2f6c32494e7645442e706e67" />

#####	Hiển thị dạng Hex và ASCII của gói tin bắt được

<img src="https://camo.githubusercontent.com/8401cc473509319442326a80cbb3d0f640a73751/687474703a2f2f692e696d6775722e636f6d2f51384a454258452e706e67" />

#####	Lưu các gói tin bắt được vào file

<img src="https://camo.githubusercontent.com/f77c0af661e91a7fbad6b0377649e8e9228db1cd/687474703a2f2f692e696d6775722e636f6d2f75346e52366f352e706e67" />

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

#### 6. Nguồn Tổng hợp và tham khảo
##### Tổng hợp từ các bài viết

- Đào Huy Hoàng: https://github.com/hoangdh/tcpdump
- Nguyễn Tiến Huy: https://github.com/huynt2016/tcpdump
- Kiều Tùng Lâm: https://github.com/kieulam141/TCPdump
- Vũ Xuân Lộc: https://github.com/locvx1234/tcpdump
- Nguyễn Nam Phong: https://github.com/phong041294/TCPDUMP

##### Tham khảo

- http://www.tcpdump.org/manpages/tcpdump.1.html#lbAD
- http://www.thegeekstuff.com/2010/08/tcpdump-command-examples/
- https://vinahost.vn/ac/knowledgebase/248/TCPDUMP-va-cac-th-thut-s-dng.html
- http://securitydaily.net/phan-tich-goi-tin-15-lenh-tcpdump-duoc-su-dung-trong-thuc-te/