# English Below

## Tài liệu này hướng dẫn các bước tạo user admin với đầy đủ quyền root trên hệ điều hành Ubuntu.

## Các lệnh thực hiện

```bash
# 1. Tạo user mới tên admin
sudo adduser admin

# 2. Thêm user admin vào nhóm sudo
sudo usermod -aG sudo admin

# 3. Kiểm tra xem user admin đã được thêm vào nhóm sudo chưa
sudo groups admin

# 4. Thêm user admin vào các nhóm hệ thống quan trọng khác
sudo usermod -aG adm,cdrom,dip,plugdev,lpadmin admin

# 5. (Tùy chọn) Cho phép user admin sử dụng sudo mà không cần nhập mật khẩu
# echo "admin ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/admin
```

## Các bước thực hiện

1. Mở Terminal trên Ubuntu
2. Chạy lệnh `sudo adduser admin` và nhập mật khẩu khi được yêu cầu
3. Thêm user vào nhóm sudo bằng lệnh `sudo usermod -aG sudo admin`
4. Kiểm tra bằng lệnh `sudo groups admin`
5. Thêm vào các nhóm hệ thống khác bằng lệnh cuối cùng

## Kiểm tra quyền

Sau khi hoàn tất, bạn có thể kiểm tra quyền của user admin:

```bash
# Chuyển sang tài khoản admin
su - admin

# Kiểm tra quyền sudo
sudo ls -la /root
```

---

# Create Admin User with Root Privileges on Ubuntu

This document provides instructions for creating an admin user with full root privileges on Ubuntu operating system.

## Commands

```bash
# 1. Create a new user named admin
sudo adduser admin

# 2. Add admin user to the sudo group
sudo usermod -aG sudo admin

# 3. Verify that admin user has been added to the sudo group
sudo groups admin

# 4. Add admin user to other important system groups
sudo usermod -aG adm,cdrom,dip,plugdev,lpadmin admin

# 5. (Optional) Allow admin user to use sudo without password
# echo "admin ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/admin
```

## Steps to Follow

1. Open Terminal on Ubuntu
2. Run `sudo adduser admin` and enter password when prompted
3. Add the user to sudo group with `sudo usermod -aG sudo admin`
4. Verify with `sudo groups admin`
5. Add to additional system groups with the final command

## Verify Privileges

After completion, you can verify the admin user's privileges:

```bash
# Switch to admin account
su - admin

# Test sudo privileges
sudo ls -la /root
```
