# Cài các ứng dụng cần thiết
>- Google Chrome
>- Obsidian
>- Teams
>- Webstorm
>- Goland -> Dev Go
>- CLion
>- Chocolaty
>- Git
>- Sudo

# Config git
```bash
// Config thông tin cơ bản
git config --global user.name "Minh Tran"
git config --global user.email "minh.tn.hust@gmail.com"
git config --global color.ui true

// Config template
git config --global commit.template ~/.gitmessage.txt

// Config signingkey - personal token trong Dev setting treen github
git config --global user.signingkey <paste_key_vào_đây>
```

Template
```md
########50 characters############################  
Subject  
########72 characters##################################################  
Problem  
# Problem, Task, Reason for CommitSolution  
# Solution or List of ChangesNote  
# Special instructions, testing steps, rake, etc

# Solution

```

# Config terminal
- Tải Windows Terminal
- Tải Caskaydia Code Font và cài đặt vào terminal
- Chạy Script cài đặt các component cần thiết
```powershell
choco install nodejs
choco install sudo
choco install golang
choco install java
```

# Đồng bộ file
## Đồng bộ onedrive
- Đăng nhập tài khoản Onedrive cá nhân
- Đăng nhập tài khoản Onedrive của trường
	- Đồng bộ thư mục TOEIC
	- Đồng bộ thư mực Phim
## Đồng bộ Obsidian
- Clone obsidian-note repo về máy

# Thiết lập cá nhân
## Gõ tiếng việt trong terminal
- Gõ ***intl.cpl*** vào thanh run
- Chọn **Administrative**
- Chọn **Change system locale
- Tick vào **Use Unicode UTF-8 for worldwide language support**

## Giảm độ nhạy touch pad trong khi gõ phím
- Settings
- Devices
- Touchpad
- Touchpad sensitivity -> Low sensitivity