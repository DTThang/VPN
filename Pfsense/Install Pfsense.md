# 1. Giới thiệu Pfsensen 
- Pfsense là một ứng dụng có chức năng định tuyến vào tường lửa mạnh và miễn phí, ứng dụng này sẽ cho phép bạn mở rộng mạng của mình mà không bị thỏa hiệp về sự bảo mật.
- Pfsense bao gồm nhiều tính năng mà bạn vẫn thấy trên các thiết bị tường lửa hoặc router thương mại, chẳng hạn như GUI trên nền Web tạo sự quản lý một cách dễ dàng
- Pfsense được dựa trên FreeBSD và giao thức Common Address Redundancy Protocol (CARP) của FreeBSD, cung cấp khả năng dự phòng bằng cách cho phép các quản trị viên nhóm hai hoặc nhiều tường lửa vào một nhóm tự động chuyển đổi dự phòng. Vì nó hỗ trợ nhiều kết nối mạng diện rộng (WAN) nên có thể thực hiện việc cân bằng tải
![image](image/imagem-k/Screenshot_2.png)

## 2. Cài đặt Pfsense

- Ở đây tôi thực hành trên WebVirtCloud
- Truy cập vào trang chủ Pfsense https://www.pfsense.org/download/ để tải phiên bản mới nhất của Pfsense. 
![image](image/imagem-k/Screenshot_3.png)


- Ở đây tôi đã có sẵn file iso bản pfSense-CE-2.5.1 trên WebVirtCloud.

##  2.1 Cài đặt pfsense trên WebVirtCloud
- Thiêt lập
    - Tạo Instances có các thiết lập như sau

    - Chọn disk và file ISO tải được từ trang chủ. Lưu ý khi chọn volume chọn bus dạng ide
![image](image/imagem-k/Screenshot_4.png)

    - Sắp xếp thứ tự boot
![image](image/imagem-k/Screenshot_5.png)

    - Chọn chọn card network
![image](image/imagem-k/Screenshot_6.png)

  - Khởi động OS
    - Sau khi pfsense khởi động chọn Accept 
![image](image/imagem-k/Screenshot_7.png)
    
    - Vào mode cài đặt pfsence
![image](image/imagem-k/Screenshot_8.png)

    - Lựa chọn bàn phím sử dụng
![image](image/imagem-k/Screenshot_9.png)

    - Lựa chọn phân vùng cài đặt và phương pháp boot
![image](image/imagem-k/Screenshot_10.png)
![image](image/imagem-k/Screenshot_11.png)

    - Khởi động lại OS

## 2.2 Thiết lập địa chỉ ip  
- Ở bài lab này, tôi thiết lập địa chỉ ip tĩnh cho pfsense

- Sau khi khởi động nhập n để không tạo VLAN cho pfsense
![image](image/imagem-k/Screenshot_12.png)

-  Thực hiện cấu hình dải mạng WAN (tức IP public của máy ảo). Nhập `em0` -> `Enter` -> Nhập `y`
![image](image/imagem-k/Screenshot_13.png)

- Sau khi cấu hình, trên màn hình console sẽ hiển thị địa chỉ public của máy ảo 
![image](image/imagem-k/Screenshot_14.png)

- Cấu hình IP WAN, giao diện web cho Pfsense. Chọn option `2`
![image](image/imagem-k/Screenshot_15.png)

- Cấu hình IPv4 cho mạng WAN, chọn n để bỏ qua cấu hình DHCP và cấu hình IP tĩnh 
![image](image/imagem-k/Screenshot_16.png)

- Tiếp theo nhập `n`, --> `enter` để bỏ qua cấu hình IPv6. 

  Nhập `n` để bỏ qua qua thiết lập DHCP server trên WAN

  Nhập `y` để cấu hình truy cập giao diện của Pfsense thông qua HTTP
  
  Địa chỉ IPv4 đã được cấu hình 

  Nhấn `enter` để hoàn thành 

![image](image/imagem-k/Screenshot_17.png)


## 2.3  Cấu hình Pfsense qua giao diện web

1. Truy cập địa chỉ IP public của máy ảo Pfsense qua trình duyệt web. Tài khoản mặc định:
  - 1.User: admin
  - 2.Password: pfsense
![image](image/imagem-k/Screenshot_18.png)
2. Chọn **Next**
![image](image/imagem-k/Screenshot_19.png)

3. Chọn **Next**
![image](image/imagem-k/Screenshot_20.png)

4. Thiết lập Domain, DNS
![image](image/imagem-k/Screenshot_21.png)

5. Thiết lập Timezone
![image](image/imagem-k/Screenshot_22.png)

6. . Cấu hình WAN, kéo xuống dưới chọn **Next**
![image](image/imagem-k/Screenshot_23.png)

7. Thay đổi mật khẩu quản trị web
![image](image/imagem-k/Screenshot_24.png)

8. Chọn **Reload** để mật khẩu có hiệu lực  
![image](image/imagem-k/Screenshot_25.png)

9. Đợi hệ thống hoàn thành cấu hình 
![image](image/imagem-k/Screenshot_26.png)

10. Chọn **Finish**
![image](image/imagem-k/Screenshot_27.png)

11. Chọn **Accept**
![image](image/imagem-k/Screenshot_28.png)

12. Chọn **Close**
![image](image/imagem-k/Screenshot_29.png)

## 2.4 Cấu hình LAN trên PFSense Web
1. Chọn Interface -> Assignments
![image](image/imagem-k/Screenshot_36.png)

2. Chọn Add -> Save
![image](image/imagem-k/Screenshot_37.png)

3. Chọn Interface -> LAN để cấu hình interface mới
![image](image/imagem-k/Screenshot_38.png)

4. Chỉnh sửa các thông tin của interface mới

- (1) Enable interface
- (2) Lựa chọn Static Ipv4
- (3) Đặt IP cho interface và subnet mask tương ứng
![image](image/imagem-k/Screenshot_39.png)

5. Chọn **Save** 
![image](image/imagem-k/Screenshot_40.png)

6. Chọn Apply Changes để áp dụng interface mới 
![image](image/imagem-k/Screenshot_41.png)
![image](image/imagem-k/Screenshot_42.png)


## 2.5 Tạo rule firewall để cho phép kết nối Pfsense qua giao diện Web
1. Chọn Firewall -> Rules
![image](image/imagem-k/Screenshot_30.png)

2. Bổ sung rule truy cập HTTP. Chọn Add
![image](image/imagem-k/Screenshot_31.png)

3. Tại mục Destination -> Destination Port Range -> Chọn HTTP (80) -> Save
![image](image/imagem-k/Screenshot_32.png)

4. Tạo rule tương tự cho HTTPS
![image](image/imagem-k/Screenshot_33.png)

5. Chọn **Apply Changes** để xác nhận thay đổi
![image](image/imagem-k/Screenshot_34.png)
![image](image/imagem-k/Screenshot_35.png)




# Tham khảo 

- https://docs.smartcloud.vn/index.php/knowledge-base/huong-dan-cai-dat-pfsense/
- https://github.com/hocchudong/ghichep-pfSense/blob/master/docs/pfSense-install.md