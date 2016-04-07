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
tcpdump -i enp0s3
```

#####	Giới hạn số lượng gói tin
#####	Hiển thị dạng ASCII của gói tin bắt được
#####	Hiển thị dạng Hex và ASCII của gói tin bắt được
#####	Lưu các gói tin bắt được vào file
#####	Đọc file chứa các gói tin
	-	 Đọc file chứa các gói tin lớn hơn 1 kích cỡ cho sẵn
	-	 Đọc file chứa các gói tin nhỏ hơn 1 kích cỡ cho sẵn
#####	Bắt các gói tin với địa chỉ IP thông qua tcpdump –n
#####	Lọc theo protocol
#####	Bắt các gói theo port
#####	Bắt theo địa chỉ nguồn hoặc đích
#####	Các tùy chọn hiển thị thời gian
