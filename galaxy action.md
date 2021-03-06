# 1. Một số option chung  

option | description 
---|---
--version | hiển thị tên phiên bản, vị trí file cấu hình, đường dẫn module đã cấu hình, vị trí module, vị trí thực thi và thoát
-h, --help | hiển thi phần trợ giúp 
-v, --verbose| chế độ verboss 
# 2. Actions
## 2.1 collection
- Thực hiện hành động trên Ansible Galaxy collection. Phải được kết hợp với một hoạt động khác nhưu init/install như danh sách bên dưới.
  - **collection init**

    - Tạo khung cho một role hoặc collection tuân thủ định dạng của galaxy. Yêu cầu tên của role và collection, định dạng tên `<namespace>.<collection>`


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


## 2.2 Role

- Thưc thiện hành động trên ansible galaxy role. Phải được kết hợp với một hành động kkhác như init/install/delete
  - **role init**
    - Tạo khung cho một role hoặc collection tuân thủ định dạng của galaxy. Yêu cầu tên của role và collection, định dạng tên `<namespace>.<collection>`


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