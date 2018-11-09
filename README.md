### 10 cách dùng cơ bản với useradd
==========
#### 1.1: Làm thế nào để tạo user trong Linux
Để tạo mới 1 user ta dùng lệnh useradd hoặc adduser với tên user muốn tạo. Tên user mới phải không được trùng với tên user đã có trong hệ thống.
Giả sử ta muốn tạo 1 user testuser:
 ```
    root@thanhha:~# useradd test
 ```
 Sau khi tạo user thì user sẽ ở trạng thái bị khóa, để mở khóa user ta thiết lập mật khẩu cho user
 ````
	root@thanhha:~# passwd testuser 
	Changing password for user testuser.
	New UNIX password:
	Retype new UNIX password:
	passwd: all authentication tokens updated successfully
 ````
 Sau khi tạo user, thông tin user sẽ được lưu trong file /etc/passwd
 ```
	usertest:x:1001:1001:usertest:/home/usertest:/bin/bash
 ```
 Ý nghĩa các trường:
 * 	Username: tên user để đăng nhập vào hệ thống.
 * 	Password: Password của user được mã hóa.
 * 	User ID (UID): Mỗi user có 1 UID riêng, mặc định UID=0 dành cho user root, UID thuộc từ 1 đến 999 dành riêng cho các tài khoản được xác định trước.từ 1000 trở đi dành cho user khác.
 * 	Group ID (GID): Group ID (GID) Group Identification Number được lưu tại /etc/group file.
 * 	User Info: Cho phép xác định thêm thông tin user như tên đầy đủ.
 * 	Home Directory: Thư mục home của user.
 * 	Shell: Tên chương trình sẽ thực thi ngay sau khi user login vào. Nếu không có shell user sẽ không thể login. Mặc nhiên trên Linux sẽ dùng bash shell ở đây.

