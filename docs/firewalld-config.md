# Cấu hình - Configuration
---
## Tổng quan
Cấu hình firewalld được lưu dạng XML file bên trong nhưng thư mục chứa cấu hình.

## Directories
Firwalld cung cấp 2 thư mục chứa cấu hình

### Thư mục cấu hình mặc định, dựa phòng (Default and Fallback Configuration)
Thư mục `/usr/lib/firewalld` chứa các cấu hình mặc định và dự phòng, được cung cấp bởi firewalld cho các dạng icmptypes, services, zones.

Các file bên trong được cung cập mặc định theo package firewalld cung cấp. Nếu thay đổi, khi update các giá trị này sẽ tự khôi phục

### Thư mực cấu hình hệ thống (System Specific Configuration)
Các cấu hình chỉ định cho hệ thống lưu tại `/etc/firewalld/` được tạo bởi user, sysadmin hoặc các custom đi theo package, ..

Nếu thư mục `/etc/firewalld/` trống, firewalld sẽ khởi động theo cấu hình mặc định, đã được chỉ định trước trong `firewalld.conf`

## Runtime versus Permanent
Các cấu hình trong firewalld chia thành `runtime` và `permanent` config
### Runtime config
- runtime config là các config đang có hiệu lực, các config này được nạp tại module firewalld trong kernel.
- Khi firewall service bắt đầu chạy, các permanent config sẽ chuyển thành các runtime config. Việc thay đổi runtime config không tự động lưu lại trên permanent config.
- Các runtime config sẽ mất khi firewalld service stop, firewalld reload sẽ chạy lại các permanent config.
### Permanent Configuration
- Perman config được lưu tại config file và cho phép nạp lại, chúng sẽ trở thành các runtime config khi service restart, reboot, boot..

### Runtime to Permanent
- Runtime environment sử dụng các set firewall khác nhau phù hợp với các thời điểm. Khi các cấu hình đã phù hợp với yêu cầu,

Chuyển runtime tới permanent
```
firewall-cmd --runtime-to-permanent
```
