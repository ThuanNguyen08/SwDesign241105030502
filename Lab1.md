# Welcome
## Lab1
### Nguyễn Văn Thuận - 4451050990

# ***Phân tích kiến trúc và ca sử dụng hệ thống `Payroll System`***

1. **Phân tích Kiến trúc**

    - **Kiến trúc lựa chọn**: Kiến trúc `MVC` (Model-View-Controller) phù hợp với hệ thống `Payroll System` vì nó tách biệt rõ ràng các phần xử lý dữ liệu (Model), giao diện người dùng (View), và xử lý logic nghiệp vụ (Controller). Điều này giúp duy trì và mở rộng hệ thống dễ dàng hơn khi có thay đổi về logic hoặc giao diện.

    - **Các thành phần MVC**: 
        + **Model**: Quản lý dữ liệu và logic nghiệp vụ cốt lõi (thông tin nhân viên, thẻ chấm công, và phiếu lương). Model sẽ liên kết với cơ sở dữ liệu để lưu trữ và truy xuất thông tin cần thiết cho quá trình tính lương.

        + **View**: Chịu trách nhiệm hiển thị giao diện người dùng để nhân viên và quản trị viên nhập liệu, xem báo cáo, và kiểm tra trạng thái thẻ chấm công.

        + **Controller**: Nhận yêu cầu từ người dùng, điều hướng giữa View và Model, và cập nhật các thay đổi lên giao diện dựa trên dữ liệu từ Model.

    - **Biểu đồ package mô tả kiến trúc**:
    
        ![Diagram](https://www.planttext.com/api/plantuml/png/V90z2iCm34Ptdq9apmKob9JIiT2XT1UoQ4ty4so744fFrg57wXKQPqXS4Ze9dZuz97rUxpf4zB4pMhH83TuOYZCEtcbzSf9r0Gy1G1f3WADfjHkOPt1HXWczdC4uINUcHZp5IdTLt6_P4f_XNXfb9x9XE3WRKsM_vLcwlxQCZywL2ifo1_d5K04ISGWS_gVJccEuQoN69JlHB9NDLg1iP8yKWn0rMvc-_WK00F__0m00)
    
    -  **Các thành phần:**
        + **PayrollView**: Chứa các lớp liên quan đến giao diện người dùng như `EmployeeView, AdminView.`
        + **PayrollController**: Chứa các lớp xử lý logic nghiệp vụ như `EmployeeController, AdminController,` và điều phối giữa Model và View.
        + **PayrollModel**: Chứa các lớp liên quan đến dữ liệu như `Employee, Timecard, Paycheck`.

2. **Cơ chế phân tích**
    - Dựa trên yêu cầu của hệ thống Payroll, các cơ chế phân tích cần thiết bao gồm:

        + **Bền vững Dữ liệu (Persistency)**: Model cần đảm bảo rằng thông tin về nhân viên, thẻ chấm công, và phiếu lương được lưu trữ một cách ổn định ngay cả khi ứng dụng không hoạt động. Điều này có thể đạt được qua các cơ chế lưu trữ dữ liệu như JDBC kết nối với CSDL quan hệ.

        + **Bảo mật (Security)**: Đảm bảo rằng chỉ nhân viên mới có thể xem và chỉnh sửa thông tin cá nhân của họ; trong khi đó, Quản trị viên bảng lương có quyền thay đổi thông tin nhân viên khác (ngoại trừ phương thức thanh toán).

        + **Giao diện Hệ thống Kế thừa (Legacy Interface)**: Hệ thống Payroll sẽ tích hợp với CSDL Quản lý Dự án hiện có để truy xuất các mã số dự án liên quan mà không cần cập nhật trực tiếp vào đó.

        + **Xử lý Phân tán (Distribution)**: Các thành phần trong Controller có thể được phân tán để tăng cường khả năng xử lý độc lập, giúp tối ưu hóa hiệu suất hệ thống khi có số lượng lớn người dùng.

3. **Phân tích ca sử dụng Select Payment**
    - **Các lớp phân tích chính:** 
        + **Entity (PayrollModel)**:
            - Employee: Chứa các thuộc tính về nhân viên, bao gồm thông tin thanh toán.
            - PaymentMethod: Đại diện cho các phương thức thanh toán mà nhân viên có thể lựa chọn (nhận trực tiếp, gửi qua bưu điện, chuyển khoản).
        + **Boundary (PayrollView)**:
            - EmployeeView: Hiển thị cho nhân viên các lựa chọn về phương thức thanh toán.
        + **Control (PayrollController)**: 
            - EmployeeController: Điều khiển quy trình chọn phương thức thanh toán và cập nhật thông tin thanh toán vào Model.

    - **Biểu đồ Sequence cho Select Payment**

        ![Diagram](https://www.planttext.com/api/plantuml/png/b9EnJiCm48PtFyMz02_G0LL2Z4XCx95ZnPRYSvHUWCoCYA4p2u41KQbI1nRgWS4ex-4du1Lm2eKcf25C9z-Tl_lrd_rkNwSpYd8gTCeYJYQ7OvsbfXI2PI6jkCeYfE_aaK7AJPgAlBTyfiH5Rw6LF8rABP1E14aJCxRjWOF35cW2kl1sZi2bjpS8cQnNTOK9K3W_yH0Yb436LGXiz-8kw4SmJA1qYmAuNpyM89MtLxX1NGDt5H_2invQHsoW_qQIUoctwljmNR5TIDnScGMI75Itry706-6TDY7_QVKu6nDlbseG-JQlLzu-yA_nV_ZNoFJhPGOeGw11CfScjBbxX7Fb5ll8hHVs7xpszbQDtizbi-GD5TiZIBgxmEJk6HF6fWBZvdzz0000__y30000)

    - **Các biểu đồ lớp mô tả lớp phân tích và giải thích**

        ![Diagram](https://www.planttext.com/api/plantuml/png/Z9BDQiCm3CVlUGhHKmhBOLSpIc7RRLymjhk9rKRWZs2h2s7ioNRO8-qLbZXk5fV2TZAMV_hhBydVdr_RmDBpmUYYrZ84k3MjTZqYl1S05P0IyCoUx3vUhJIO1LhP6xHyZzou0NrQNWS08A36chDuQSxHQm5lZbJnKIGdsMkoCsK-v2u0zfYm6sH9EfJh-NcMEpPsxInxfpNwg0cWABHQzgdSOylaR5I8TaRYq2h9cFU0IKxCmXVmlxwE_2jXboo4ndKdzIUj8E2E0bzbYfkbjzhP7NcJW9Vej5pKdFUvkbn1LMtYcOzMf2M5uioCnfJCiG2oZ5uEF7J4pLz9Gy8qlr_vg7F2MCUqem7QebNZT_m1003__mC0)

        + Giải thích: 
            - **Employee**
                + Mục đích: Đại diện cho thông tin về nhân viên trong hệ thống.
                + Thuộc tính:
                    - id: Mã định danh duy nhất cho mỗi nhân viên.
                    - name: Tên nhân viên.
                    - paymentMethod: Phương thức thanh toán được chọn (sử dụng đối tượng PaymentMethod).
                + Phương thức:
                    - selectPaymentMethod(method: PaymentMethod): Cập nhật phương thức thanh toán mới cho nhân viên.

            - **PaymentMethod**
                + Mục đích: Đại diện cho các phương thức thanh toán có thể lựa chọn, như nhận trực tiếp, chuyển khoản, hay gửi qua bưu điện.
                + Thuộc tính:
                    - methodName: Tên phương thức thanh toán (ví dụ: "Chuyển khoản").
                + Phương thức:
                    - sgetMethodDetails(): Trả về chi tiết của phương thức thanh toán.

            - **EmployeeController**
                + Mục đích: Làm nhiệm vụ điều phối yêu cầu từ Employee, yêu cầu hiển thị từ EmployeeView, và cập nhật thông tin thanh toán cho Employee trong Model.
                + Phương thức:
                    - displayPaymentOptions(): Yêu cầu EmployeeView hiển thị các phương thức thanh toán.
                    - updatePaymentMethod(employee: Employee, method: PaymentMethod): Cập nhật phương thức thanh toán mới vào thông tin của Employee.


4. **Phân tích ca sử dụng Maintain Timecard**
    - Các lớp phân tích chính: 
        + **Entity (PayrollModel)**:
            - Employee: Lớp đại diện cho nhân viên, liên kết với lớp Timecard.
            - Timecard: Quản lý thông tin về thời gian làm việc và mã số dự án mà nhân viên đã làm.

        + **Boundary (PayrollView)**:
            - TimecardView: Hiển thị giao diện cho phép nhân viên nhập thời gian làm việc.

        + **Control (PayrollController)**:
            - TimecardController: Điều khiển quá trình tạo, cập nhật và nộp thẻ chấm công từ View đến Model.

    - **Biểu đồ Sequence cho Maintain Timecard**

        ![Diagram](https://www.planttext.com/api/plantuml/png/d9D1IiGm58RtESMxW1Tm8GFY3SHzJ4CRIDAIIQjTYWiNhkO0OaiHGHXKSDKiN4IyHqxW5KogCxIIiU8cYxoyx_tl_yc7ULqiDLQw51nXedC5HwBWUKqfAlmr8wp0KiCn4vHWbHpcKgkSSwgYvHD6poQ5Ns48RSgmTn0P0VjGsuSIYEllIn3Et8BEN6-0-FDE0B4lCeMCENCbGRk-PIW26Q4zaFlEscE6LiraXBY5x5IbbUixg9ov-2CfBYUuvMbXWSkXtLpFyAA6VMEaVxWk1imDWvHX2Tms0ghW3u7ADY1i1qjdLf0uymosbMZ2sBLkwioQXPv7u05Mnc9uMxq_ETEHa9QNCQZHytcCNy-CGF-myzosv8ikfwEyputCViIqSM7hSZoSKzlcOp9QK9c43_G9003__mC0)

    - **Các biểu đồ lớp mô tả lớp phân tích và giải thích**

        ![Diagram](https://www.planttext.com/api/plantuml/png/Z59BJWGX4DrpYaglHcDFufQ5cMJ64wZZ6g6qKPhg0EraOZoP2u_a5GIaF-fCT0DKyUgzLmKVR-yh7uGBVMkODC9xk6mxGtj4U640DMZ5uIeuRHzoQ4MBimG0TMYlTOjIEBKuuV1CMh5NLiY6cqAcH8ZLcxZciA7U-LjoJnX5DjJVcQzyv-WHPLYJ-gxLTubWLClbG-4Po1dyg94rsU3867JPqW__M7hdunGYqN1xo48eXmbrL7chSLSqbVQT4Vj_i2Iq97klNNkJbUSZ7b-gEg-WhY_YlboULjFGEJJ2imEj9_0CfMr09sJmiDEX-QiWDyA79YR-d4_0qTSlPhP2gz9N-mG00F__0m00)

        + Giải thích: 

            - **Employee**
                + Mục đích: Đại diện cho nhân viên trong hệ thống, lớp này liên kết với Timecard để theo dõi thời gian làm việc của từng nhân viên.
                + Thuộc tính:
                    - id: Mã định danh duy nhất cho mỗi nhân viên.
                    - name: Tên nhân viên.
                + Phương thức:
                    - openTimecard(): Nhân viên yêu cầu mở thẻ chấm công để kiểm tra hoặc cập nhật.

            - **Timecard**
                + Mục đích: Quản lý thông tin chấm công của nhân viên, bao gồm thời gian làm việc và mã số dự án liên quan.
                + Thuộc tính:
                    - date: Ngày làm việc của thẻ chấm công.
                    - hoursWorked: Số giờ làm việc trong ngày.
                    - projectCode: Mã số dự án mà nhân viên làm việc trong ngày.
                + Phương thức:
                    - updateTimecard(hours: Double, code: String): Cập nhật thời gian làm việc và mã số dự án.

            - **TimecardController**
                + Mục đích: Điều khiển các thao tác liên quan đến thẻ chấm công, từ việc mở, hiển thị cho đến cập nhật khi có thay đổi.
                + Phương thức:
                    - openTimecard(employee: Employee): Timecard: Mở thẻ chấm công của nhân viên đã chọn.
                    - updateTimecard(timecard: Timecard): Cập nhật thông tin mới vào thẻ chấm công.

             - TimecardController
                + Mục đích: Là giao diện người dùng hiển thị và xác nhận thông tin liên quan đến thẻ chấm công.
                + Phương thức:
                    - displayTimecard(timecard: Timecard): Hiển thị thông tin thẻ chấm công.
                    - confirmUpdate(): Xác nhận thông tin đã được cập nhật thành công.



        
        
5. **Hợp nhất kết quả phân tích**

# Tài liệu Mô tả Hệ thống Quản lý Chấm công và Thanh toán

1. Tổng quan
    - Hệ thống này cho phép nhân viên quản lý thẻ chấm công và chọn phương thức thanh toán. Các ca sử dụng "Select Payment" và "Maintain Timecard" cung cấp chức năng cho nhân viên lựa chọn phương thức nhận lương và ghi lại giờ làm việc. Hệ thống tuân theo mô hình kiến trúc MVC (Model-View-Controller) để đảm bảo tính rõ ràng và dễ dàng mở rộng.

2. Phân tích Lớp
    - Các lớp chính
        1. **Entity (PayrollModel)**
            - **Employee:** Đại diện cho thông tin của nhân viên, bao gồm các thuộc tính như mã nhân viên, tên, và phương thức thanh toán.
                + Thuộc tính:
                    - id: Mã định danh duy nhất cho mỗi nhân viên.
                    - name: Tên nhân viên.
                    - paymentMethod: Phương thức thanh toán của nhân viên.
                + Quan hệ: Kết nối với Timecard và PaymentMethod.

            - **Timecard:** Quản lý dữ liệu về thời gian làm việc và mã số dự án của nhân viên.
                + Thuộc tính:
                    - date: Ngày làm việc.
                    - hoursWorked: Số giờ làm việc của nhân viên trong ngày.
                    - projectCode: Mã dự án mà nhân viên đã tham gia.
                + Phương thức:
                    - updateTimecard(hours: Double, code: String): Cập nhật thông tin thời gian và mã dự án.
                + Quan hệ: Được liên kết với Employee.

            - **PaymentMethod:** Đại diện cho các phương thức thanh toán có thể chọn như chuyển khoản, nhận tiền mặt, hoặc gửi qua bưu điện.
                + Thuộc tính:
                    - methodName: Tên phương thức thanh toán.
                + Phương thức:
                    - getMethodDetails(): Trả về thông tin chi tiết của phương thức thanh toán.

        2. **Boundary (PayrollView)**
            - **EmployeeView:** Hiển thị giao diện để nhân viên lựa chọn phương thức thanh toán.
                + Phương thức:
                    - displayPaymentOptions(methods: List<PaymentMethod>): Hiển thị danh sách phương thức thanh toán.
                    - confirmPaymentUpdate(): Xác nhận lựa chọn đã được cập nhật thành công.
            - TimecardView: Hiển thị giao diện cho nhân viên ghi lại giờ làm việc.
                + Phương thức:
                    - displayTimecard(timecard: Timecard): Hiển thị thẻ chấm công.
                    - confirmUpdate(): Xác nhận thẻ chấm công đã được cập nhật.

        3. **Control (PayrollController)**
            - **EmployeeController:** Điều khiển việc chọn phương thức thanh toán của nhân viên và cập nhật thông tin vào Model.
                + Phương thức:
                    - displayPaymentOptions(): Lấy danh sách phương thức thanh toán từ Model và hiển thị qua EmployeeView.
                    - updatePaymentMethod(employee: Employee, method: PaymentMethod): Cập nhật phương thức thanh toán của nhân viên.
            - **TimecardController:** Điều khiển việc tạo, cập nhật, và lưu thẻ chấm công từ TimecardView vào Model.
                + Phương thức:
                    - openTimecard(employee: Employee): Timecard: Lấy thông tin thẻ chấm công hiện tại của nhân viên.
                    - updateTimecard(timecard: Timecard): Cập nhật thông tin chấm công mới vào Model.

    - **Biểu đồ lớp tổng hợp**

        ![Diagram](https://www.planttext.com/api/plantuml/png/Z5JBJiCm4BptArOv5THMuXgXgbBBZPV4wsoIfJ4uTcHlg2h4bt7Wa_W5dCH9upejN9BOdfsT6Tlv-VfU66AQoboC4i6CWOky46gB21yZW2dmD8Oxqbokww5aENeJ1TlcAEaAALCMUjiVMW20GO49UVFZV0Xz4iExuasHAb3UynmJfjDnk_0vSXAzCgUpeRpsvG6iqS5MI8mBKv6vvOwkRUIOKaQMOsMVzJ1JfJPFIh-X5RnIvRDevWkjNgsnfKhzZcLH4NJYw_AsS0993nxuQgDVAabQ2O6wbWIGSbC8jdM-RmhYIffnFx2cgvyoEhgu8vx0qUI3H08Xthw4_9QeNHtAWjp73dKmWaUEcwFc6oCssKjkwDopC-y7aoZvmdNk00-reF14jNh2jlyGtsiJydVNAJgBO3gTs_TiTXhj3bqC6JD3i6ZldCUGP4ePt85xsrELUDd5hG4p6jZD2kvvxi4FiE-BuP9GiuGCR3XbVpK92nOeq-glymi00F__0m00)

3. Mô tả ca sử dụng
    - **Ca Sử dụng: Select Payment**
        + Luồng hoạt động:
            - `Employee` yêu cầu `EmployeeController` hiển thị danh sách các phương thức thanh toán có sẵn.
            - `EmployeeController` yêu cầu `EmployeeView` hiển thị danh sách các phương thức thanh toán từ `PaymentMethod.`
            - `Employee` chọn phương thức thanh toán mong muốn từ `EmployeeView.`
            - `EmployeeController` cập nhật thông tin `Employee` với phương thức thanh toán mới trong `Model`.
            - `EmployeeView` hiển thị thông báo xác nhận cập nhật thành công.

        + Mục tiêu: Nhân viên có thể lựa chọn và cập nhật phương thức thanh toán mong muốn thông qua hệ thống.

    - **Ca Sử dụng: Maintain Timecard**
        + Luồng hoạt động: 
            - `Employee` yêu cầu `TimecardController` mở thẻ chấm công hiện tại.
            - `TimecardController` lấy thông tin `Timecard` từ `Model` và hiển thị qua `TimecardView`.
            - `Employee` nhập thời gian làm việc và các mã số dự án liên quan vào `TimecardView`.
            - `TimecardController` xác nhận thông tin và cập nhật dữ liệu vào `Timecard` trong `Model`.
            - `TimecardView` hiển thị thông báo xác nhận rằng thẻ chấm công đã được cập nhật.
        
        + Mục tiêu: Nhân viên có thể quản lý và cập nhật thông tin chấm công của mình một cách chính xác.

# ---------------------- HẾT ----------------------------------
