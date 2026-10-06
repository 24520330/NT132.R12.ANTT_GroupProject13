1\. Mạng Quản trị và lưu trữ: Dành cho truy cập giao diện web (vCenter), kết nối các máy chủ với nhau và truyền tải dữ liệu ổ cứng (Storage)

\- Thông số mạng: 

&#x09;Subnet: 192.168.100.0/24 | Subnet Mask: 255.255.255.0 | Gateway: 192.168.100.1

|Thiết bị / Node|Địa chỉ IP tĩnh|Phân hệ (Role)|Người cấu hình|Ghi chú (Host/VM)|
|-|-|-|-|-|
|Gateway/DNS|192.168.100.1|Network Core|Tự động|Khai báo IP này làm DNS Server khi cài vCenter|
|ESXi Host 1|192.168.100.11|Compute|Trực|Cài đặt trên máy của TV2|
|ESXi Host 2|192.168.100.12|Compute|Định|Cài đặt trên máy của TV3|
|vCenter (VCSA)|192.168.100.20|Management|Trực|IP dùng để đăng nhập quản lý toàn hệ thống|
|Storage Server|192.168.100.30|Storage|Định|Máy chủ cấp ổ cứng chung (TrueNAS/Windows)|



2\. Mạng vMotion: Đường ống riêng chỉ dùng để copy RAM khi di chuyển nóng máy ảo giữa 2 host. Tách biệt dải mạng này giúp quá trình vMotion không làm lag mạng quản trị vCenter. Mạng này không ra Internet nên không cần Gateway. 

&#x20;- Thông số mạng:

&#x09;Subnet: 10.10.10.0/24 | Subnet Mask: 255.255.255.0 | Gateway: N/A 

|Cổng mạng ảo|Địa chỉ IP Tĩnh|Nằm trên máy chủ|Người cấu hình|Ghi chú|
|-|-|-|-|-|
|VMkernel vMotion 1|10.10.10.11|ESXi Host 1|Đức|Cấu hình qua giao diện vCenter|
|VMkernel vMotion 2|10.10.10.12|ESXi Host 2|Đức|Cấu hình qua giao diện vCenter|



3\. Quy chuẩn mật khẩu (Credentials):

&#x20;- Để tránh tình trạng quên pass, nhập sai quá số lần dẫn đến khóa tài khoản gây khó khăn trong đồ án, toàn bộ hệ thống từ vCenter, ESXi đến Storage sẽ dùng chung một bộ thông tin duy nhất:

* Tài khoản mặc định (Default User): root (với ESXi/vCenter) hoặc Administrator (với Windows).
* Mật khẩu chung toàn hệ thống: GroupVMware@2026
* Tên miền cục bộ (SSO Domain của vCenter): vsphere.local (Tài khoản login vCenter web: administrator@vsphere.local)



**Lưu ý: Bất kỳ thành viên nào thay đổi IP do lỗi cấu hình, phải lập tức cập nhật file này trên nhánh main để cả nhóm nắm thông tin**

