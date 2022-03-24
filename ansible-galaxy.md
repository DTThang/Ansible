# 1. Giới thiệu
- Ansible Galaxy là một kho lưu trữ cho ansible role có thể sử dụng trực tiếp thông qua playbook nhằm hợp lý hóa các dự án tự động hóa.
- Trang web lưu trữ của Ansible Galaxy là https://galaxy.ansible.com

**Ansible collection**

- Collection là dạng phân phối cho ansible content. Chúng được sử dụng để đóng gói và phân phối playbook, roles, modules và plugins
- Cấu trúc đơn giản của một collection 
```
collection/
├── docs/
├── galaxy.yml
├── plugins/
│ ├──  modules/
│ │ └──  module1.py
│ ├──  inventory/
│ └──  .../
├── README.md
├── roles/
│ ├──  role1/
│ ├──  role2/
│ └──  .../
├── playbooks/
│ ├──  files/
│ ├──  vars/
│ ├──  templates/
│ └──  tasks/
└──  tests/
```
## 1.2 Ansible role

# 2 HƯớng dẫn sử dụng ansible galaxy 
- Cấu trúc: `ansible-galaxy [-h] [--version] [-v] TYPE ..`
- 1. Tìm kiếm role bằng cách sử dụng lệnh `ansible-galaxy search`
  - Ví dụ tìm kiếm các role liên quan tới php dành có các hệ điều hành như 
RedHat/CentOS/Fedora/Debian/Ubuntu

        ansible-galaxy search "PHP for RedHat/CentOS/Fedora/Debian/Ubuntu" 
  
    Kết quả 

```
root@ansible:~# ansible-galaxy search "PHP for RedHat/CentOS/Fedora/Debian/Ubuntu"

Found 26 roles matching your search:

 Name                            Description
 ----                            -----------
 alikins.php                     PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 apham0001.php                   PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 bpresles.php                    PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 call_learning.php               PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 e1mo.php                        PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 entanet_devops.ansible_role_php PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 esperdyne.php                   PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 frogasia.ansible-role-php       PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 geerlingguy.php                 PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 heremias.php                    PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 jhu-sheridan-libraries.php      PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 jibsan94.ansible_php            PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 KAMI911.ansible_role_php        PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 manishjuneja.php                PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 mbaran0v.ansible_role_php       PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 monsieurbiz.geerlingguy_php     PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 nesh-younify.ansible-role-php   PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 net2grid.php                    PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 nycrecords.php                  PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 thom8.ansible-role-php          PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 tobiasehlert.ansible_role_php   PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 vahubert.php                    PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 Vaizard.mage_php                PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 viasite-ansible.php             PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 vvgelder.ansible-role-php       PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
 xylodev.php                     PHP for RedHat/CentOS/Fedora/Debian/Ubuntu.
```


- 2. Bên trên ta có thể thấy danh sách các role được lọc ra. Chọn một role và kiểm tra thông tin về role đó. Sử dụng lệnh `ansible-galaxy info` để xem các thông tin về role 
 
      ansible-galaxy info geerlingguy.php

  ![image](image/Screenshot_16.png)

-  3. Cần  download role về máy để sử dụng trong playbook. Sử dụng lệnh ansible-galaxy install để cài đặt role về máy

      ansible-galaxy install geerlingguy.php

Kết quả

```
root@ansible:~# ansible-galaxy install geerlingguy.php
- downloading role 'php', owned by geerlingguy
- downloading role from https://github.com/geerlingguy/ansible-role-php/archive/4.8.0.tar.gz
- extracting geerlingguy.php to /root/.ansible/roles/geerlingguy.php
- geerlingguy.php (4.8.0) was installed successfully
```
  - Role đã được cài về máy và được lưu tại /root/.ansible/roles/geerlingguy.php
  
- 4. Di chuyển đến vị trí đặt role. Tạo file playbook.yml để chạy role vừa cài về máy với nội dung
```
- host: node1
  roles: geerlingguy.php
```

  - Chạy role với lệnh  `ansible-playbook /root/.ansible/playbook.yml `


- Liệt kê các role được cài đặt trên hệ thống

      ansible-galaxy list

  ![image](image/Screenshot_17.png)


# 3. Một số option chung  

option | description 
---|---
--version | hiển thị tên phiên bản, vị trí file cấu hình, đường dẫn module đã cấu hình, vị trí module, vị trí thực thi và thoát
-h, --help | hiển thi phần trợ giúp 
-v, --verbose| chế độ verboss 
# 4. Actions
## 4.1 collection
- Thực hiện hành động trên Ansible Galaxy collection. Phải được kết hợp với một hoạt động khác nhưu init/install như danh sách bên dưới.
  - **collection init**

    - Tạo khung xương cho một role hoặc collection tuân thủ định dạng của galaxy. Yêu cầu tên của role và collection, định dạng tên `<namespace>.<collection>`


option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
--collection-skeleton  <COLLECTION_SKELETON>| Đường dẫn đến một khung collection mới được gán vào.
--init-path  <INIT_PATH>|  Đường dẫn trong đó khung collection sẽ được tạo. Mặc định là thư mục hiện tại  
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-f, --force | Buộc ghi đè lên role hoặc collection hiện có
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy


  - **collection build**
    - Xây dựng Ansible Galaxy collection artifact có thể được lưu trữ ở repository như ansible galaxy. 
    - Mặc định  lệnh build từ thư mục làm việc hiện tai. Có thể tùy chọn chuyển vào đường dẫn vào collection (where the galaxy.yml file is )


option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
--output-path  <OUTPUT_PATH>|  Đường dẫn mà collection được build tới. Mặc định là thư mục hiện tại
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-f, --force | Buộc ghi đè lên role hoặc collection hiện có
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy

  - **collection publish**
    - Xuất collection vào ansible galaxy. Yêu cầu đường dẫn đến collection tarball để xuất bản 

option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
--import-timeout  <IMPORT_TIMEOUT>|  Thời gian chời cho collection  kết thúc quá trình nhập
--no-wait  |   Đừng đợi kết quả xác thực nhập
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy

  - **collection install**

    - Cài đặt một hoặc nhiều role (ansible-galaxy role install), một hoặc nhiều collection (ansible-galaxy collection install). 
    - Có thể chuyển vào danh sách hoặc sử dụng các option file ở dưới. Nếu chọn một danh sách cần có một tên (được tải xuống thông qua galaxy API và github)

option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
--force-with-deps | Buộc ghi đè một collection hiện có và các phụ thuộc của nó
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-f, --force | Buộc ghi đè lên role hoặc collection hiện có
-i, --ignore-errors| bỏ qua lỗi trong quá trình cài đặt và tiếp tục  với collection được chỉ định. Điều này không bỏ qua lỗi xung đột phụ thuộc 
-n, --no-deps| không tải xuống các collection dưới dạng phụ thuộc
-p  <COLLECTIONS_PATH>, --collections-path  <COLLECTIONS_PATH>| Đường dẫn đến thư mục chứa các collection 
-r  <REQUIREMENTS>, --requirements-file  <REQUIREMENTS> | Một tệp chứa danh sách các collection sẽ được cài đặt.
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy


## 4.2 Role

- Thưc thiện hành động trên ansible galaxy role. Phải được kết hợp với một hành động kkhác như init/install/delete
  - **role init**
    - Tạo khung xương cho một role hoặc collection tuân thủ định dạng của galaxy. Yêu cầu tên của role và collection, định dạng tên `<namespace>.<collection>`


option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
--init-path  <INIT_PATH>|  Đường dẫn trong đó khung collection sẽ được tạo. Mặc định là thư mục hiện tại  
--offline| không truy vấn galaxy API khi tạo role
--role-skeleton  <ROLE_SKELETON>|  đường dẫn để một khung role cái mà role mới phải dựa trên đó 
--type  <ROLE_TYPE>| khởi tạo sử dụng loại role luân phiên. Loại hợp lệ gồm ‘container’, ‘apb’ và ‘network’.
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-f, --force | Buộc ghi đè lên role hoặc collection hiện có
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy

  - **role remove**
    - Loại bỏ danh sách các role được truyền dưới dạng đối số từ hệ thống cục bộ.

option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-p, --roles-path| đường dẫn đến thư mục chứa role. Mặc định là tệp có thể ghi đầu tiên được định cấu hình qua DEFAULT_ROLES_PATH:~/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy

  - **role delete**
    - Xóa role từ ansible galaxy

option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy

  - **role list** 
    - Liệt kê các role  được cài đặt trên hệ thống cục bộ hoặc khớp với một vài role được truyền dưới dạng đối số 

option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-p, --roles-path| đường dẫn đến thư mục chứa role. Mặc định là tệp có thể ghi đầu tiên được định cấu hình qua DEFAULT_ROLES_PATH:~/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy


  - **role search**

    - Tìm kiếm role trên ansible galaxy server

option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
--author  <AUTHOR> | github username
--galaxy-tags  <GALAXY_TAGS> | danh sách galaxy tag để lọc theo
--platforms  <PLATFORMS> | danh sách nền tảng hệ điều hành để lọc theo 
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy

  - **role import** 
    - Sử dụng để nhập một role vào Ansible Galaxy


option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
--branch  <REFERENCE> | Tên của một nhánh cần nhập. Mặc định cho nhánh repo mặc định 
--no-wait| Dừng chờ kết quả nhập 
--role-name | tên của role nên có, nếu khác với tên repo
--status| Kiểm tra trạng thái của yêu cầu nhập gần đây nhất cho github_user/github_repo.
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy


  - **role setup** 

    - Thiết lâp tích hợp từ github hoặc travis cho ansible galaxy role

option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
--list| liệt kê tất cả các tích họp
--remove  <REMOVE_ID>|  Xóa tích hợp 
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-p, --roles-path| đường dẫn đến thư mục chứa role. Mặc định là tệp có thể ghi đầu tiên được định cấu hình qua DEFAULT_ROLES_PATH:~/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy


  - **role info**
    - In ra chi tiết thông tin về role được cài đặt như thông tin có sẵn từ galaxy API

option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
--offline| không truy vấn galaxy API khi tạo role
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-p, --roles-path| đường dẫn đến thư mục chứa role. Mặc định là tệp có thể ghi đầu tiên được định cấu hình qua DEFAULT_ROLES_PATH:~/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy

  - **role install**

    - Cài đặt một hoặc nhiều role (ansible-galaxy role install), một hoặc nhiều collection (ansible-galaxy collection install). 
    - Có thể chuyển vào danh sách hoặc sử dụng các option file ở dưới. Nếu chọn một danh sách cần có một tên (được tải xuống thông qua galaxy API và github)


option | description
---| ---
--api-key  <API_KEY>| Ansible Galaxy API key tìm tại https://galaxy.ansible.com/me/preferences. Có thể đặt mã thông báo cho mục nhập GALAXY_SERVER_LIST
--force-with-deps | Buộc ghi đè một role hiện có và các phụ thuộc của nó
-c, --ignore-certs | Bỏ qua lỗi xác thực chứng chỉ SSL
-f, --force | Buộc ghi đè lên role hoặc collection hiện có
-g, --keep-scm-meta | Sử dụng tar thay vì tùy chọn lưu trữ scm kho đóng gói role
-i, --ignore-errors| bỏ qua lỗi trong quá trình cài đặt và tiếp tục  với role được chỉ định
-n, --no-deps| không tải xuống các collection dưới dạng phụ thuộc
-p, --roles-path| đường dẫn đến thư mục chứa role. Mặc định là tệp có thể ghi đầu tiên được định cấu hình qua DEFAULT_ROLES_PATH:~/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
-r  <ROLE_FILE>, --role-file  <ROLE_FILE> | Tệp chứa danh sách các role sẽ được nhập
-s  <API_SERVER>, --server  <API_SERVER> | URL máy chủ Api Galaxy




