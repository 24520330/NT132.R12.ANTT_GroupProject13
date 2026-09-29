# NT132.R12.ANTT
# 🎓 Đồ án: Tìm hiểu và Triển khai Hạ tầng Ảo hóa VMware vSphere

**Môn học:** Quản trị mạng và hệ thống  
**Giảng viên hướng dẫn:** ThS Đỗ Hoàng Hiền  
**Nhóm thực hiện:** Nhóm 13 

---

## 📖 Tổng quan đề tài
Dự án này tập trung nghiên cứu, thiết kế và triển khai một hạ tầng ảo hóa cấp doanh nghiệp sử dụng **VMware vSphere**. Mục tiêu của hệ thống là đảm bảo tính sẵn sàng cao (High Availability), tối ưu hóa tài nguyên phần cứng và cung cấp khả năng di chuyển máy ảo không gián đoạn.

**Các mục tiêu kỹ thuật chính đạt được trong đồ án:**
- Triển khai cụm máy chủ ảo hóa (Type-1 Hypervisor) với tối thiểu **02 host ESXi**.
- Quản trị hạ tầng tập trung thông qua **vCenter Server Appliance (VCSA)**.
- Xây dựng hệ thống lưu trữ dùng chung **Shared Datastore (iSCSI/NFS)** làm nền tảng cho các tính năng nâng cao.
- Kích hoạt và kiểm thử thành công các cơ chế dự phòng và tối ưu tài nguyên: 
  - **vSphere HA (High Availability):** Tự động khôi phục máy ảo khi host vật lý gặp sự cố.
  - **vMotion:** Di chuyển "nóng" máy ảo đang hoạt động giữa các host mà không làm gián đoạn dịch vụ.
  - **vSphere DRS (Distributed Resource Scheduler):** Tự động cân bằng tải CPU/RAM trên toàn bộ Cluster.

---

## 🛠 Nền tảng & Công cụ sử dụng
- **Ảo hóa:** VMware ESXi 7.0/8.0, VMware vCenter Server.
- **Lưu trữ:** VD: TrueNAS / Windows Server / Openfiler].
- **Lưu trữ script/cấu hình:** GitHub Repository.

---

## 👥 Danh sách thành viên và Bảng phân công nhiệm vụ

| STT | Họ và tên | Vai trò & Nhiệm vụ cốt lõi |
| :---: | :--- | :--- |
| **1** | **[Thành viên 1]** | **Trưởng nhóm / vMotion & Thuyết trình**<br>- Quản lý tiến độ (Trello/GitHub).<br>- Cấu hình mạng VMkernel và tính năng vMotion.<br>- Thực hiện kiểm thử vMotion (Live Migration).<br>- Thiết kế slide và lên kịch bản demo tổng. |
| **2** | **[Thành viên 2]** | **Chuyên trách Hạ tầng Compute**<br>- Cài đặt và cấu hình mạng cơ bản cho 02 ESXi host.<br>- Triển khai vCenter Server Appliance (VCSA).<br>- Viết chương Tổng quan và Kiến trúc hệ thống. |
| **3** | **[Thành viên 3]** | **Chuyên trách Hệ thống Lưu trữ & HA**<br>- Triển khai Storage Server, cấu hình iSCSI/NFS.<br>- Gắn Shared Datastore vào ESXi hosts.<br>- Kiểm thử tính năng HA (giả lập sập host).<br>- Viết chương Cấu hình Hệ thống lưu trữ. |
| **4** | **[Thành viên 4]** | **Chuyên trách Cluster & DRS**<br>- Tạo Cluster, kích hoạt HA và DRS trên vCenter.<br>- Deploy máy ảo (VM) kiểm thử vào hệ thống.<br>- Tạo tải giả lập (stress-test) để kiểm thử thuật toán DRS.<br>- Viết chương Cấu hình Cluster & Vận hành. |

---

## 📂 Cấu trúc Repository
- `docs/`: Chứa các tài liệu quy hoạch mạng (IP Schema), mật khẩu mặc định của lab và ghi chú cấu hình.
- `diagrams/`: Hình ảnh sơ đồ topology mạng và kiến trúc hệ thống.
- `scripts/`: Chứa các kịch bản PowerShell/Shell script dùng để tạo tải giả lập hoặc tự động hóa (nếu có).
- `testing_results/`: Hình ảnh/video kết quả kiểm thử vMotion, HA và DRS.

---
*Lưu ý: Mọi thay đổi về cấu hình IP hoặc tài khoản quản trị hệ thống Lab phải được cập nhật vào file `docs/ip_schema.md` để đồng bộ giữa các thành viên.*
