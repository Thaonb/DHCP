## DHCP
### 1. Khái niệm DHCP
DHCP (Dynamic Host Configuration Protocol) : Là sự quản lý tự động địa chỉ ip bởi việc tự động hóa việc cấp phát thông tin cấu hình ip cho client.

Nó hoạt động ở tầng 7 của mô hình OSI và tương ứng tại tầng 4 của TCP/IP.

<img src="http://2.bp.blogspot.com/-8fw4bZDy7Gk/VUeNH_VvUBI/AAAAAAAAAf8/FLbwHqdTHjc/s1600/model%2Bosi.png">
### 2. Hoạt động
#### 2.1 Quá trình DHCP
- B1: Máy trạm khởi động với “địa chỉ IP rỗng” cho phép liên lạc với DHCP Servers bằng giao thức TCP/IP. Nó broadcast một thông điệp DHCP Discover chứa địa chỉ MAC và tên máy tính để tìm DHCP Server .

- B2: Nhiều DHCP Server có thể nhận thông điệp và chuẩn bị địa chỉ IP cho máy trạm. Nếu máy chủ có cấu hình hợp lệ cho máy trạm, nó gửi thông điệp “DHCP Offer” chứa địa chỉ MAC của khách, địa chỉ IP “Offer”, subnet mask, địa chỉ IP của máy chủ và thời gian cho thuê đến Client. Địa chỉ “offer” được đánh dấu là “reserve” (để dành).

- B3: Khi Client nhận thông điệp DHCP Offer và chấp nhận một trong các địa chỉ IP, Client sẽ gửi thông điệp DHCP Request để yêu cầu IP phù hợp cho DHCP Server thích hợp.

- B4: Cuối cùng, DHCP Server khẳng định lại với Client bằng thông điệp DHCP Acknowledge.

<img src="http://www.highteck.net/images/41-DHCP2.jpg">

#### 2.2 Các thông điệp DHCP

*Để làm rõ các thông điệp DHCP em xin sử dụng DEMO của mình về DHCP để thể hiện rõ ràng hơn.*

Mô hình DEMO gồm có: 1 máy chủ (Ubuntu server 14.04.3), 1 máy trạm (winxp)

Trên máy chủ Ubuntu server cài đặt và chạy dịch vụ DHCP-server.

Trên máy chủ em đã add thêm 1 card mạng và sử dụng card mạng đó để demo với địa chỉ ip: 172.16.0.1

Và dải địa chỉ cấp: 172.16.0.3 - 172.16.0.20

Trên máy trạm: để cấu hình ip động.

Sử dụng gói tcpdump trên ubuntu server để bắt và phân tích gói tin DHCP

##### 1. IP Lease Request

<img src="http://i.imgur.com/PNfID8d.png">

Đầu tiên, client sẽ broadcast một message tên là DHCPDISCOVER, vì client lúc này chưa có địa chỉ IP cho nên nó sẽ dùng một địa chỉ source(nguồn) là 0.0.0.0 và cũng vì client không biết địa chỉ của DHCP server nên nó sẽ gửi đến một địa chỉ broadcast là 255.255.255.255. Lúc này gói tin DHCPDISCOVER này sẽ broadcast lên toàn mạng. Gói tin này cũng chứa một địa chỉ MAC (Media Access Control) và đồng thời nó cũng chứa computer name của máy client để DHCP server có thể biết được client nào đã gởi yêu cầu đến.

##### 2. IP Lease Offer

<img src="http://i.imgur.com/GaX60Ef.png">

Nếu có một DHCP hợp lệ (nghĩa là nó có thể cấp địa chỉ IP cho một client) nhận được gói tin DHCPDISCOVER của client thì nó sẽ trả lời lại bằng một gói tin DHCPOFFER, gói tin này đi kèm theo những thông tin sau:
+ MAC address của client
+ Một IP address cấp cho (offer IP address)
+ Một subnet mask
+ Thời gian thuê (mặc định là 8 ngày)
+ Địa chỉ IP của DHCP cấp IP cho client này

##### 3. IP Lease Selection

<img src="http://i.imgur.com/pjDFd7L.png">

DHCP client đã nhận được gói tin DHCPOFFER thì nó sẽ phản hồi broadcast lại một gói DHCPREQUEST để chấp nhận cái offer đó. DHCPREQUEST bao gồm thông tin về DHCP server cấp địa chỉ cho nó.

##### 4. IP Lease Acknowledgement

<img src="http://i.imgur.com/pfaSM4C.png">

DHCP server nhận được DHCPREQUEST sẽ gởi trả lại DHCP client một DHCPACK để cho biết là đã chấp nhận cho DHCP client đó thuê IP address đó. Gói tin này bao gồm địa chỉ IP và các thông tin cấu hình khác (DNS server, WINS server... ). Khi DHCP client nhận được DHCPACK thì cũng có nghĩa là kết thúc quá trình "tìm kiếm và xin địa chỉ" của mình.

**Tài liệu tham khảo**
- http://vdo.vn/gioi-thieu-may-chu-dhcp-dhcp-server
- http://vdo.vn/cong-nghe-thong-tin/cac-khai-niem-co-ban-ve-dhcp.html
- http://www.vnpro.vn/
- http://www.tecmint.com/12-tcpdump-commands-a-network-sniffer-tool/
- https://github.com/soncaca/command-tcpdump
