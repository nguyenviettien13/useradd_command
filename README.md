### 10 cách dùng cơ bản với useradd
==========
#### 1: Làm thế nào để tạo user trong Linux
Để tạo mới 1 user ta dùng lệnh useradd hoặc adduser với tên user muốn tạo. Tên user mới phải không được trùng với tên user đã có trong hệ thống.
Giả sử ta muốn tạo 1 user testuser:
 ```
    root@thanhha:~# useradd test
 ```
 Sau khi tạo user thì user sẽ ở trạng thái bị khóa, để mở khóa user ta thiết lập mật khẩu cho user
 ````
	root@ditu:~# passwd testuser 
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
#### 2: Tạo user với thư mục home
Mặc định lệnh useradd tạo thư mục home theo đường dẫn /home/username. Tuy nhiên ta có thể thay đường dẫn thư mục mặc định này. Giả sư user test đã tạo ở trên ta để thư mục home tại đường dẫn /data/usertest
 ```
	[root@ditu]# useradd -d /data/usertest usertest
 ```
Ta kiểm tra thông tin vừa tạo:
 ````
	[root@ditu]# cat /etc/passwd | grep usertest
	usertest:x:1001:1001::/data/usertest:/bin/bash
 ````
#### 3. Tạo user với User ID
Số đi kèm với username, hệ điều hành dùng số này để quản lý. Như vậy nếu có hai username khác nhau nhưng dùng chung một userID, thì hệ thống xem hai tên này chỉ là một. Mặc định thì khi user mới được tạo thì sẽ được gán ID 1000,1001. Tuy nhiên ta có thể gán User ID cho user. Ví dụ gán User ID 1100 cho user usertest
 ```
	[root@ditu]# useradd -u 1100 test1100
 ```
Kiểm tra user vừa tạo:
 ````
	root@ditu:/home# gedit /etc/passwd
	usertest1100:x:1100:1100::/home/usertest1100:
 ````

