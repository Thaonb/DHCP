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


### 4. Kết Luận
**Tài liệu tham khảo**
- http://vdo.vn/gioi-thieu-may-chu-dhcp-dhcp-server
- http://vdo.vn/cong-nghe-thong-tin/cac-khai-niem-co-ban-ve-dhcp.html
- http://www.vnpro.vn/
