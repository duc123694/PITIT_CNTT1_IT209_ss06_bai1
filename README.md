# Bài 1: Khảo sát FHS và Phân quyền File/Folder nâng cao

## 1. Mục tiêu

* Tạo cấu trúc thư mục theo chuẩn Linux FHS.
* Thực hành phân quyền file/folder bằng quyền Octal.
* Thực hành thay đổi Owner và Group.
* Kiểm tra quyền bằng lệnh `ls -la`.

## 2. Tạo cấu trúc thư mục

Đã sử dụng các lệnh:

```bash
sudo mkdir -p /var/www/my-app/public
sudo mkdir -p /var/www/my-app/logs
```

Cấu trúc thư mục:

```text
/var/www/my-app
├── public
└── logs
```

## 3. Phân quyền thư mục public

Yêu cầu:

* Owner: đọc, ghi, thực thi.
* Group: đọc, thực thi.
* Others: không có quyền.

Thực hiện:

```bash
sudo chmod 750 /var/www/my-app/public
```

Quyền `750` tương ứng:

```text
Owner  = rwx
Group  = r-x
Others = ---
```

## 4. Phân quyền thư mục logs

Yêu cầu:

* Owner: toàn quyền.
* Group: toàn quyền.
* Others: không có quyền.

Thực hiện:

```bash
sudo chmod 770 /var/www/my-app/logs
```

Quyền `770` tương ứng:

```text
Owner  = rwx
Group  = rwx
Others = ---
```

## 5. Thay đổi Owner và Group

Sử dụng tài khoản hiện tại làm Owner và nhóm `www-data` làm Group:

```bash
sudo chown -R $USER:www-data /var/www/my-app
```

Kiểm tra tài khoản hiện tại:

```bash
whoami
```

## 6. Kiểm tra kết quả

Sử dụng lệnh:

```bash
ls -la /var/www/my-app
```

Kết quả:

```text
total 16
drwxr-xr-x 4 user www-data 4096 Oct  5 23:30 .
drwxr-xr-x 3 root root     4096 Oct  5 23:30 ..
drwxr-x--- 2 user www-data 4096 Oct  5 23:30 public
drwxrwx--- 2 user www-data 4096 Oct  5 23:30 logs
```

Trong đó:

```text
public → drwxr-x--- → 750
logs   → drwxrwx--- → 770
```

## 7. Kết luận

Đã hoàn thành việc tạo cấu trúc `/var/www/my-app` gồm hai thư mục `public` và `logs`, đồng thời thiết lập quyền truy cập và Owner/Group theo yêu cầu.

* `public`: `750`
* `logs`: `770`
* Group: `www-data`
* Owner: tài khoản non-root hiện tại
