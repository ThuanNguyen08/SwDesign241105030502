# Welcome
## Lab4
### Nguyễn Văn Thuận - 4451050990
# ------------------------------------------------------------

# ***Thiết kế các ca sử dụng cho hệ thống `Payroll System` dựa vào kết quả phân tích ca sử dụng và các phần tử thiết kế***
## 1. Login
- Mô tả sự tương tác giữa các đối tượng thiết kế:
    + Employee (Tác nhân): Nhân viên là người khởi tạo yêu cầu đăng nhập bằng cách cung cấp thông tin tài khoản.
    + LoginUI (Giao diện đăng nhập): Hiển thị biểu mẫu đăng nhập và xử lý thông tin nhập vào.
    + AuthSystem (Hệ thống xác thực): Thực hiện kiểm tra thông tin đăng nhập để xác nhận tài khoản.
    + Database (Cơ sở dữ liệu): Lưu trữ thông tin xác thực và được truy vấn bởi AuthSystem.

- Đơn giản hóa biểu đồ tuần tự bằng cách sử dụng các hệ thống con  
    ![Diagram](https://www.planttext.com/api/plantuml/png/Z5BFIiCm6B_dAJvwKj0Ns44cA2eC4PmFaBPX2MlJqgJJddVmu4NniEl6476uW-2fFUoGlKYUm5VmQsjP9uBh8Npvyllt9VqgLbsbQQBJC23Kqr42pcaO1r76c0DK0GjZ4kEvy4HCfGQd5ms4lBce3eEwtWOSfvfVPqgpiC9Gt6u3JgYcBbMrlkyIWXvmUDIeGGSkkSsNCMYpaB1-Me_b06JT6fafX5Xf66BZBIKD2Vcb4vBFRB4Ka9b52fxDNrEuCpCFDBV5XmTxgMA9f24xW9WgTHib_ZwfY2ZWkqZl9sa68vk_IEIOJxJM0aip5MWPsNmk2Gqqz5iDGErv384jxWdWXpgREFsDo2zOOxkP-uetSiy2dFLZUt8CCvKSl5BDgVYjqSiRxC2viCLOLgC-G8XmuEQzv72pb9omGB7jtCCwsuxn_qR_DqNF5XFHVeDTml_Sl6jcKUaq4OH9dtHnAV_JRm000F__0m00)

- Mô tả hành vi liên quan đến lưu trữ
    + AuthSystem truy cập Database để thực hiện việc:
        - Tra cứu thông tin tài khoản (tên đăng nhập và mật khẩu băm).
        - Lưu trạng thái phiên làm việc nếu đăng nhập thành công.
    + Database lưu trữ:
        - Thông tin xác thực (username, hashed password).
        - Lịch sử đăng nhập (nếu cần).

- Tinh chỉnh mô tả luồng sự kiện:
    + Ca sử dụng Login bao gồm các luồng sự kiện:
        - Luồng chính (Basic Flow):
            + Nhân viên nhập tên đăng nhập và mật khẩu.
            + Hệ thống xác thực thông tin và thông báo thành công nếu thông tin hợp lệ.
        - Luồng thay thế (Alternative Flows):
            + Thông tin không hợp lệ:
                - Nếu tên đăng nhập hoặc mật khẩu không khớp, thông báo lỗi hiển thị.
                - Người dùng có thể nhập lại thông tin.
            + Khóa tài khoản:
                - Nếu nhập sai quá số lần cho phép, hệ thống khóa tài khoản và yêu cầu liên hệ quản trị viên.

- Hợp nhất các lớp và hệ thống con:
    + UI Subsystem:
        - Lớp LoginUI: Xử lý giao diện và thu thập dữ liệu người dùng.
    + Authentication Subsystem:
        - Lớp AuthSystem: Chứa logic xác thực.
        - Lớp Database: Lưu trữ thông tin tài khoản và hỗ trợ truy vấn.
    + Liên kết:
        - LoginUI gửi yêu cầu đến AuthSystem.
        - AuthSystem tương tác với Database để xác minh thông tin.


## 2. Maintain TimeCard 
- Mô tả sự tương tác giữa các đối tượng thiết kế
    + Employee (Tác nhân): Nhân viên là người thực hiện việc cập nhật và lưu bảng chấm công.
    + TimecardForm (Giao diện): Biểu mẫu giao diện để hiển thị và thu thập thông tin từ nhân viên.
    + TimecardController (Bộ điều khiển): Xử lý logic nghiệp vụ liên quan đến việc truy xuất và cập nhật bảng chấm công.
    + Timecard (Đối tượng dữ liệu): Đại diện cho bảng chấm công của nhân viên, lưu trữ các giờ làm việc theo từng mã công việc.
    + ProjectManagementDatabase (Cơ sở dữ liệu): Lưu trữ các mã công việc (charge codes) để tham chiếu.

- Đơn giản hóa biểu đồ tuần tự bằng cách sử dụng các hệ thống con 
    ![Diagram](https://www.planttext.com/api/plantuml/png/Z9HBJiCm48RtFeNL5Iou00jKKK2m0B4e1vZOqzGGsz7OGUevMB92Y1kmQXSiE4bEm1MO9YrDseGsKXxZ-Jpvvo7_BBw68GB5mcO2LFGa1vSsp_mCSI0XIBIvoDblbCd1HJaO6uiAI5zviXKnuOzkPEHT99zbI1Me_inkl8BYocWZz-GVKSLRS92YHHSl8482eTQe4o5OfpmvgyJ8Ksd1kCZtElJHiQWyJ6nKC9TY71L47B11DWZcruBwQCYYF2_dxowLQbhEFwnKtvziF4shLomNBuwVypSZ95z_uTgXnmnucNJ4iUNYrGXqMZItjh8WZ0KvgMfjcnAs4rcLHfkGPp1hPD1VcYbGYYElCUoKHITT3A_sYQiuTZ7OBQmBt6ehPuTqxGiAF7trd-yAco25lWONkOQ8XpHtXznNxdg3tbFkcf8FDzkv17Z6VUEvnVHgNt87AEQrYI4BqNZtxt1K0MKebCB0JHZoz2tFXry0003__mC0)

- Mô tả hành vi liên quan đến lưu trữ
    + Timecard:
        - Lưu các thông tin về mã công việc và số giờ làm việc do nhân viên nhập vào.
        - Đảm bảo cập nhật chính xác khi nhân viên thay đổi hoặc thêm mới thông tin.
    + ProjectManagementDatabase:
        - Cung cấp danh sách các mã công việc để nhân viên tham chiếu khi điền bảng chấm công.
        - Đồng bộ hóa dữ liệu với hệ thống quản lý dự án.

- Tinh chỉnh mô tả luồng sự kiện
    + Luồng chính (Basic Flow):
        - Nhân viên mở giao diện bảng chấm công (TimecardForm).
        - Hệ thống hiển thị bảng chấm công hiện tại và danh sách mã công việc.
        - Nhân viên nhập giờ làm việc theo từng mã công việc.
        - Hệ thống cập nhật bảng chấm công.
        - Nhân viên lưu bảng chấm công; hệ thống xác nhận việc lưu thành công.
    + Luồng thay thế (Alternative Flows):
        - Bảng chấm công chưa tồn tại:
            + Nếu bảng chấm công chưa tồn tại, hệ thống tự động tạo mới khi nhân viên mở giao diện.
        - Mã công việc không hợp lệ:
            + Nếu nhân viên nhập mã công việc không có trong danh sách, hiển thị lỗi và yêu cầu nhập lại.
        - Lỗi khi lưu:
            + Nếu xảy ra lỗi trong quá trình lưu, hiển thị thông báo lỗi và yêu cầu nhân viên thử lại.

- Hợp nhất các lớp và hệ thống con
    + Các lớp và hệ thống con:
        - UI Subsystem:
            + Lớp TimecardForm: Hiển thị giao diện bảng chấm công và thu thập dữ liệu từ nhân viên.
        - Business Logic Subsystem:
            + Lớp TimecardController: Thực hiện logic xử lý, như lấy danh sách mã công việc, cập nhật dữ liệu.
        - Persistence Subsystem:
            + Lớp Timecard: Lưu trữ dữ liệu bảng chấm công của nhân viên.
            + Lớp ProjectManagementDatabase: Quản lý và cung cấp danh sách mã công việc.

## 3. Run Payroll
- Mô tả sự tương tác giữa các đối tượng thiết kế:
    + Admin (Tác nhân): Người quản trị hệ thống thực hiện việc tính lương cho toàn bộ nhân viên.
    + PayrollUI (Giao diện): Biểu mẫu giao diện để Admin khởi chạy quy trình tính lương và xem báo cáo kết quả.
    + PayrollController (Bộ điều khiển): Xử lý logic nghiệp vụ liên quan đến việc tính lương.
    + Employee (Đối tượng dữ liệu): Đại diện cho thông tin nhân viên được sử dụng trong tính toán lương.
    + Timecard (Đối tượng dữ liệu): Dữ liệu bảng chấm công được sử dụng để tính lương.
    + PayrollDatabase (Cơ sở dữ liệu): Lưu trữ thông tin lương đã được tính.
- Đơn giản hóa biểu đồ tuần tự bằng cách sử dụng các hệ thống con 
    ![Diagram](https://www.planttext.com/api/plantuml/png/T99DJiGm38NtEOKrgna9Bi023G8MIBD00WxW9e69b3yb3gXdOy6Hk09kscReKBffu_VPpx7x_VcrpuI9YhC29OK4cnlbZDy0Pi3XIqIMZJGHFS7c4ViKh7rvg40ng-fjy3IyTQgKRCSbVU-Y3RtM5T8kBjLduxJ4fAfAqs7LxWu9EynZ7TK9KVk6oslk3wuW5J-1svtW2CTF7R5kl263f4_GBvbXxeofDqrplmUJYQaXVbuhQIh93ocL1Cke43Q42AyyMutos4G1_2ojvckEVlC4jdF6hgOqw1_pfYkUouh98aUYbSKkRlytGtLCPdnlqDpG1SGnKhru95w9i-dL5IYJeyL-Idygpc7gspR6TR73CNn07aKXzbni-2j_0000__y30000)

- Mô tả hành vi liên quan đến lưu trữ
    + Timecard: Lưu trữ thông tin chấm công của nhân viên, được sử dụng để tính toán lương dựa trên số giờ làm việc.
    + PayrollDatabase:
        + Lưu trữ thông tin về bảng lương đã được tính toán.
        + Quản lý báo cáo chi tiết về lương cho từng nhân viên.

- Tinh chỉnh mô tả luồng sự kiện
    + Luồng chính (Basic Flow):
        - Người quản trị khởi chạy quy trình tính lương từ giao diện PayrollUI.
        - Hệ thống truy xuất danh sách nhân viên và bảng chấm công của họ.
        - Hệ thống tính lương cho từng nhân viên dựa trên thông tin lương cơ bản và dữ liệu bảng chấm công.
        - Hệ thống lưu thông tin lương đã tính vào cơ sở dữ liệu.
        - Hiển thị báo cáo tổng quan về lương cho người quản trị.
    + Luồng thay thế (Alternative Flows):
        - Không có bảng chấm công: Nếu không tìm thấy bảng chấm công, hiển thị cảnh báo và bỏ qua nhân viên đó.
        - Lỗi khi lưu: Nếu xảy ra lỗi trong quá trình lưu, hiển thị thông báo lỗi và cho phép Admin khởi chạy lại quy trình.

- Hợp nhất các lớp và hệ thống con
    + Các lớp và hệ thống con:
        - UI Subsystem:
            + Lớp PayrollUI: Hiển thị giao diện cho phép người quản trị khởi chạy và theo dõi quy trình tính lương.
        - Business Logic Subsystem:
            + Lớp PayrollController: Xử lý logic nghiệp vụ tính toán lương và xử lý lỗi khi cần thiết.
        - Persistence Subsystem:
            + Lớp Employee: Lưu trữ thông tin nhân viên, bao gồm các thuộc tính như lương cơ bản.
            + Lớp Timecard: Lưu trữ thông tin về giờ làm việc.
            + Lớp PayrollDatabase: Lưu kết quả tính lương và báo cáo.
