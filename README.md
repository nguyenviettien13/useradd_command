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

#### 4. Tạo user với Group ID
Mặc định thì khi tạo user thì thường Group ID bằng với UserID, tuy nhiên ta có thể thay thế Group ID như sau:
 ```
		[root@tiennv]# useradd -u 1000 -g 500 hatt
		[root@tiennv]# cat /etc/passwd | grep hatt
		htt:x:1000:500::/home/hatt:/bin/bash
 ```

#### 5. Thêm user vào nhiều nhóm
Ta có thể thêm user vào nhiều nhóm thông qua thuộc tính -G. Ví dụ
 ```
		[root@tiennv~]# useradd -G admins,webadmin,developers tiennv 
		[root@tiennv~]# id tiennv
		uid=1001(tiennv) gid=1001(tiennv)
		groups=1001(tiennv),500(admins),501(webadmin),502(developers)
		context=root:system_r:unconfined_t:SystemLow-SystemHigh
 ```
#### 6.  Tạo user không có thư mục home
Trong một vài trường hợp ta không muốn tạo thư mục home cho user, ví dụ trong trường hợp bảo mật ta thực hiện
 ```
[root@tiennv ~]# useradd -M nohomeuser
 ```
Kiểm tra
 ````
		[root@thanhha~]# ls -l /home/nohomeuser
		ls: cannot access /home/nohomeuser: No such file or directory
 ````
#### 7.Gán thời hạn cho tài khoản
Mặc định khi 1 user mới được tạo thì user đó được hoạt động vô thời hạn. Ta có thể gắn thời hạn tài khoản cho user bằng thuộc tính -e cùng với ngày tháng hết hạn hoạt động của tài khoản
 ```
		tiennv@ditu:~$ sudo chage -l limittimeuser
		[sudo] password for tiennv: 
		Last password change					: Th11 09, 2018
		Password expires					: never
		Password inactive					: never
		Account expires						: Th11 09, 2018
		Minimum number of days between password change		: 0
		Maximum number of days between password change		: 99999
		Number of days of warning before password expires	: 7
 ```

#### 8. Gán thời hạn cho mật khẩu của user
Tham số -f dùng để gán thời hạn hoạt động của mật khẩu, giá trị 0 có nghĩa là mật khẩu người dùng đã hết hạn, giá trị 1 có nghĩa mật khẩu không có thời hạn sử dụng, ta có thể gán thời hạn sử dụng cho tài khoản
 ```
		[root@thanhha~]# useradd -e 2014-04-27 -f 45 thanhha
 ```
#### 9. Thêm các chú thích cho user
Ta có thể thêm các chú thích cho các user ví dụ như tên đầy đủ, số điện thoại, địa chỉ thông qua lựa chọn -c
 ```
		Ta có thể xem chú thích trong file /etc/passwd
 ```
#### 10. Thay thế shell cho user
Ta có thể thay thế shell đăng nhập cho user ngoài shell mặc định là bash shell
 ```
	[root@ditu~]# useradd -s /sbin/nologin tiennv000 
 ```




