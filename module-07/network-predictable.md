# Khái niệm

> Nội dung của section này được lấy chủ yếu từ bài viết **[Predictable Consistent Network Device Naming](https://www.computernetworkingnotes.com/linux-tutorials/predictable-consistent-network-device-naming.html)**

## Quy tắc

- Sử dụng số index **eno[1-N]** cho các onboard interface.
- Sử dụng slot number **ens[1-N]** cho PCI Express hotplug interface.
- Sử dụng index number **enp[PCI slot]s[card index]** cho PCI slot.

Trong các tên được tạo, hai kí tự đầu tiên đại diện cho firmware của thiết bị, Ví dụ, Ethernet interface bắt đầu với **en**, WLAN interface bắt đầu với **wl**, và WWAN interface bắt đầu với **ww**.

![img](/images/module-07/lt43-03-first-two-letters.png)

Kí tự tiếp theo đại diện cho loại thiết bị,  vị trí hoặc topology. Ví dụ kí tự **o** đại diện cho onboard, kí tự **s** đại diện cho hot plug slot, kí tự **p** đại diện cho PCI card.

![img](/images/module-07/lt43-04-second-letter.png)

Số còn lại đại diện cho số index, ID hoặc port.

![img](/images/module-07/lt43-05-example.png)