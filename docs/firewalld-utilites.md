# Các công cụ Firewalld
---
## firewall-cmd
- là cmd tool chủ yếu sử dụng cho firewalld.
- Sử dụng để lấy các trạng thái về firewalld, lấy các config firewall cho runtime hoặc thay đổi môi trường, đưa runtime xuống perman
- Dựa trên việc yêu cầu policy, cần xác nhận để truy cập hoặc thay đổi firewalld config. Polkit được sử dụng cho vấn đề này

VD:

To get the firewalld version:
```
$ firewall-cmd --version
0.4.3.3
```
To get the firewall-cmd help output:
```
$ firewall-cmd --help
```
To get the firewalld state:
```
$ firewall-cmd --state
running
```
To get the active zones with bindings:
```
$ firewall-cmd --get-active-zones
public
  interfaces: em1
```
To get the zone of the interface em1
```
$ firewall-cmd --get-zone-of-interface=em1
public
```

__Chi tiết__
http://www.firewalld.org/documentation/man-pages/firewall-cmd

## firewall-offline-cmd
- cmd tool sử dụng để config firewall ngay cả khi firewalld được chạy hoặc ko chạy.
- cần sử dụng quyền root để sử dụng firewall-offline-cmd
- convironment chỉ cho phép cung cấp các thông tin về các perman environment và thay đổi nó. Nó sử dụng firewall core với file IO handlers.
- firewall-offline-cmd có thể sử dụng khi firewalld đang chạy (Ko khuyền dùng). Các thay đổi sẽ được áp dụng sau 5s

VD:

To get the firewalld version:
```
# firewall-offline-cmd --version
0.4.3.3
```

To get the firewall-offline-cmd help output:
```
# firewall-offline-cmd --help
```
To get the zone of the interface em1
```
# firewall-offline-cmd --get-zone-of-interface=em1
no zone
```
__Chi tiết__
http://www.firewalld.org/documentation/man-pages/firewall-offline-cmd

## firewallctl
- là cmd tool mới hỗ trợ bởi firewalld. Sử dụng các simpler và shorter option.
- Có thể sử dụng để lấy trạng thái về firewalld, lấy firewall config trong môi trường runtime và môi trường perman.
- Dựa trên việc lựa chọn các chính sách, cần xác thực để được quyền truy cập và thay đổi config firewalld. Nó sử dụng polkit để giải quyết vấn đề này
- firewalldctl được thêm vào tại phiên bản 0.4.3

Examples of the firewall-cmd usage
To get the firewalld version:
```
$ firewallctl version
0.4.3.3
```

To get the firewallctl help output:
```
$ firewallctl --help
```
To get the firewalld state:
```
$ firewallctl state
running
```
To get the active zones:
```
$ firewallctl list zones --active
public
```
To get the firewalld configuration:
```
$ firewallctl config list
default-zone public
lockdown     no
log-denied   off
panic        no
```
To get firewalld runtime settings:
```
$ firewallctl settings list
BRIDGE          yes
CleanupOnExit   yes
IPSet           yes
IPSetTypes      hash:mac hash:net hash:ip
IPv4            yes
IPv6            yes
IPv6_rpfilter   yes
IndividualCalls no
MinimalMark     100
```
Xem thêm về cmd tool tại man page
http://www.firewalld.org/documentation/man-pages/firewallctl

## firewall-config
- Là grapphical conf tool sử dụng chi firewalld
Xem thêm tại:
http://www.firewalld.org/documentation/utilities/firewall-config.html

## firewall-applet
- firewall-applet cung cấp các thông tin về firewalld config như default zone cung như zone binding như connection, interfaces, sources
- There is a left and also right mouse button menu and also a tooltip with the active settings when moving the mouse over the icon.
- The applet has ben ported over to Qt4 as the StatusIcon support in Gtk3 has been deprecated.
