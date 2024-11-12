# Welcome
## Lab2
### Nguyễn Văn Thuận - 4451050990
# ------------------------------------------------------------

# ***Phân tích kiến trúc các ca sử dụng còn lại trong hệ thống `Payroll System`***


1. Create Administrative Report (Tạo Báo cáo Quản trị)
    - Các lớp phân tích chính
        + Entity:

            - Employee: Lưu thông tin của từng nhân viên để tạo báo cáo.
            - AdministrativeReport: Thực thể báo cáo quản trị lưu các dữ liệu như tổng số giờ làm việc hoặc tổng lương đến thời điểm hiện tại.
        + Boundary:

            - AdminReportUI: Giao diện cho phép quản trị viên nhập thông tin để tạo báo cáo.
        + Control:

            - AdminReportController: Điều khiển quá trình tạo báo cáo quản trị từ thông tin nhập vào của quản trị viên.

    - **Biểu đồ Sequence cho Create Administrative Report**   
        ![Diagram](https://www.planttext.com/api/plantuml/png/V54x3i8m3Drp2eyWmGKw810WmOQG47DeBHIHnfNh5kLi31o9Az0MIZygdPBdFB_dvxmUpsKgcYMBhTAX4CD1UoPhLr5idBfGvYBD7Yfun8HOJdiLafE2rAwkFoMBhD294G_REB7a4MjSaKqghCNa-EbIgcq7yqNNA01Ay8ScKzLvxT6R2G886RLyFIPLm4s1Pu0kAYyTeQQl5Aod3e1Hs62EP-BRZZ9E1uLg_iWmzrgWwD3_dOVs4y0L7NAJfQCr4gEtniYaYTN-AyBLCLNB8aNvyMy0003__mC0)

     - **Các biểu đồ lớp mô tả lớp phân tích và giải thích**  
        ![Diagram](https://www.planttext.com/api/plantuml/png/X5BTIiCm5BxFKvpB2jiB51aJ5To5R2ZYTMmE8ovDmibPeOXFveMFv2kODcdBHfsz29oJxxVav-jx7LWI7siZAYD3WFlQ6zSYmeU0_iEysAWIjEMyjRB64fwPjDtd5M6SiC5NHuS7TwHGzD9taYEoEnU0LatZLTBx5DdvHjNQwi0aMJVuXDuHZoce7oDDbl0e_NLoNi3sxHqhNcNK7Yr6UYONwYzuj6wSLcVUYVMo6KsTnt5P39nqfNJmHhRPAAKhPojSyhfrbiaPWpHwLeHJWNz_uA2yassdqql3ShawBIHEwvtTJo74VBGEFpoB2v2vyc8T4tUFwnS00F__0m00) 

        + Giải thích:
            - Employee

                + Mục đích: Đại diện cho thông tin cơ bản của nhân viên trong hệ thống, phục vụ việc tổng hợp dữ liệu tạo báo cáo.
                + Thuộc tính:
                    - employeeId: Mã định danh duy nhất của mỗi nhân viên.
                    - name: Tên của nhân viên.
                + Phương thức:
                    - retrieveWorkHours(startDate: Date, endDate: Date): Trả về số giờ làm việc của nhân viên trong khoảng thời gian nhất định.

            - AdministrativeReport

                + Mục đích: Đại diện cho báo cáo quản trị tổng hợp thông tin về tổng giờ làm việc hoặc tổng thu nhập của nhân viên.
                + Thuộc tính:
                    - reportData: Dữ liệu báo cáo, lưu dưới dạng key-value chứa thông tin chi tiết về báo cáo.
                + Phương thức:
                    - generateReport(data: Map<String, Object>): Tạo báo cáo dựa trên dữ liệu được cung cấp từ lớp Employee.

            - AdminReportUI

                + Mục đích: Giao diện người dùng cho phép quản trị viên tương tác, tạo và xem báo cáo.
                + Phương thức:
                    - openReportUI(): Mở giao diện báo cáo.
                    - displayReport(report: AdministrativeReport): Hiển thị báo cáo sau khi được tạo.

            - AdminReportController

                + Mục đích: Điều khiển quá trình tạo báo cáo quản trị, nhận yêu cầu từ AdminReportUI và lấy dữ liệu từ Employee.
                + Phương thức:
                    - createReport(startDate: Date, endDate: Date): Tạo báo cáo trong khoảng thời gian nhất định, tổng hợp dữ liệu và hiển thị báo cáo.

    
2. Create Employee Report (Tạo Báo cáo Nhân viên)
    - Các lớp phân tích chính
        + Entity:

            EmployeeReport: Thực thể báo cáo nhân viên chứa dữ liệu về số giờ làm việc, số giờ nghỉ phép, hoặc tổng thu nhập.
        + Boundary:

            EmployeeReportUI: Giao diện cho phép nhân viên tự tạo và xem báo cáo cá nhân.
        + Control:

            EmployeeReportController: Điều khiển quá trình tạo báo cáo cá nhân từ yêu cầu của nhân viên.
    - **Biểu đồ Sequence cho Create Employee Report**  
        ![Diagram](https://www.planttext.com/api/plantuml/png/b95D2i8m48NtSufPjb0lq8KKr8LRmGF4TXQ5D1EcKo5dwy8ZUGLRxG-a8BhBUydxyYPvze-YLIFQDHPCgInuQhpbG0Gtxbnb92pEXJoBNizGibDX6sqSFgub0N9QQnm4c3NkzXjeZkp9pIf98Jwm3QqNvbWA6PtyH8Ed3Dzp7GStGtBLk8YXAs0Bpr58fQRxf8Uy-HdylQiim3_wZ2zKrQst9anJhfWKYg78-8Kl0000__y30000)

    - **Các biểu đồ lớp mô tả lớp phân tích và giải thích**  
        ![Diagram](https://www.planttext.com/api/plantuml/png/b5512i8m4Bpd5Nkiq7wWI2ce1myYA3uWjejKqYOaQw68B_FWa_o2QMtQGrh471PsTdPdXhoVhzGGrtGh1Si4DmOsfHAoGJoWafhWpg1xkclNd7WCEwwMHz95TGbXVxvYHid0iZ3M_NBB3gXH68EZTs8Mjr1RGy0g7zl5zEq7c_HssWxkfCBAWO6zKiiYxqTvOPJWpNSQ_8ZXLcSKLx8YBOL0FIXd6gtn_lgVMPsK4u4eIhoCp0ljiqPVRDQmlyLIQwZz-0y0003__mC0)  

        + Giải thích:
            - EmployeeReport

                + Mục đích: Đại diện cho báo cáo cá nhân của nhân viên, lưu trữ dữ liệu như số giờ làm việc, tổng thu nhập, hoặc thời gian nghỉ phép.
                + Thuộc tính:
                    - reportData: Dữ liệu báo cáo cá nhân lưu dưới dạng key-value.
                + Phương thức:
                    - retrieveReportData(type: String, startDate: Date, endDate: Date): Lấy dữ liệu báo cáo dựa trên loại báo cáo, ngày bắt đầu và ngày kết thúc.

            - EmployeeReportUI

                + Mục đích: Giao diện cho phép nhân viên tạo và xem báo cáo cá nhân.
                + Phương thức:
                    - openReportUI(): Mở giao diện báo cáo cá nhân.
                    - displayReport(reportData: Map<String, Object>): Hiển thị báo cáo cá nhân sau khi tạo.

            - EmployeeReportController

                + Mục đích: Điều khiển quá trình tạo báo cáo cá nhân, nhận yêu cầu từ EmployeeReportUI, và lấy dữ liệu từ EmployeeReport.
                + Phương thức:
                    - createReport(type: String, startDate: Date, endDate: Date): Tạo báo cáo cá nhân cho nhân viên dựa trên yêu cầu.    


3. Login (Đăng nhập)
    - Các lớp phân tích chính
        + Entity:

            - User: Thực thể chứa thông tin về người dùng, bao gồm tên người dùng và mật khẩu.
        + Boundary:

            - LoginUI: Giao diện cho người dùng nhập thông tin đăng nhập.
        + Control:

            - LoginController: Điều khiển quy trình xác thực thông tin đăng nhập của người dùng.
    - **Biểu đồ Sequence cho Login**  
        ![Diagram](https://www.planttext.com/api/plantuml/png/Z9112i8m44NtEKMMBUW5kf12Lu8BKNg0CHaqc2OocIWzcmkFv1LiR6rHkd0t7zv_Cydp_YW30t5ih035dcGTa0GwDjpsyy57fu5QkV57u-grKDunUTldgW-s0uL8l5okFcGXEmzIHQYJ46p8OaSuQ70XBn32pPFEnK2FnKbPo2jOeu7nByTKJAvqJ27L2TLvEt3PLFWwTMQZyMw78LgUKu_lqoPSBBJll6VW6BBVVYvATBhxtnS0003__mC0)

    - **Các biểu đồ lớp mô tả lớp phân tích và giải thích**  
        ![Diagram](https://www.planttext.com/api/plantuml/png/b55B2i8m4Dtd55bMi1Tm8OMk11T2wG76PgZ1D2d9j2BYoLnu9AzW6z9Quyfiadbvl4_oUZmpHs2fQnIh53Z7IuUMtnZtgni63GrkU45MwZh0xK2y62iYk3fXTJw4koGchJRyQ8n2qEpEWjdUr5ANkzaFDQ7DBOhX846v90wm_l4UP7iZHH0GqhKAhbwt8A3E9Svli_d4_ywG6qtMABNeteEI0WZ_ZhDewHypJRTJKJOLdh6FCOk3Z9nHW6MenVX1Rm000F__0m00)

        + Giải thích:
            - User

                + Mục đích: Đại diện cho người dùng trong hệ thống, bao gồm thông tin đăng nhập.
                + Thuộc tính:
                    - username: Tên đăng nhập của người dùng.
                    - password: Mật khẩu của người dùng.
                + Phương thức:
                    - checkPassword(password: String): Kiểm tra tính hợp lệ của mật khẩu nhập vào.

            - LoginUI

                + Mục đích: Giao diện người dùng cho phép nhập tên đăng nhập và mật khẩu.
                + Phương thức:
                    - enterCredentials(username: String, password: String): Nhập thông tin đăng nhập.
                    - displayLoginStatus(status: boolean): Hiển thị trạng thái đăng nhập (thành công hoặc thất bại).

            - LoginController

                + Mục đích: Điều khiển quy trình xác thực đăng nhập, kiểm tra thông tin đăng nhập qua lớp User.
                + Phương thức:
                    - validateCredentials(username: String, password: String): Xác thực thông tin đăng nhập từ LoginUI.


4. Maintain Employee Information (Quản lý Thông tin Nhân viên)
    - Các lớp phân tích chính
        + Entity:

            - Employee: Thực thể lưu thông tin của nhân viên, như loại nhân viên, mức lương, và các thông tin cá nhân.
        + Boundary:

            - EmployeeInfoUI: Giao diện cho quản trị viên để thêm, cập nhật hoặc xóa thông tin nhân viên.
        + Control:

            - EmployeeInfoController: Điều khiển quy trình quản lý thông tin nhân viên.
    - **Biểu đồ Sequence cho Maintain Employee Information**  
        ![Diagram](https://www.planttext.com/api/plantuml/png/Z94n3i8m34Ntd28Z35oW0oeg3DrOE81fN2bIObUk6N8s1ex45IW2rAGIYD5VVl_hs_VhhHuLH2yn6EYKnHuX2OUmSz6JEVE574YoXpW4JeWjzNngJSUaqrOXDoyje1WazJf3nkIcThDTs5MM1wHSMwrDkRA4vh3AWdC5Y-zX3mgbpqpbVfNj147n2_WhUhf3xoM2UgO_aZvrdH-70Ad9wAbnZUIUVtW0003__mC0)

    - **Các biểu đồ lớp mô tả lớp phân tích và giải thích**  
        ![Diagram](https://www.planttext.com/api/plantuml/png/f99DJWCn38NtEOMNWqGl45LL4R2O1IeIS00pyQ0WnucI52b2dAoB7eahGEbC6SBFecHfl_TiVyhhPhjC6MDUErOTOqfmwGBxGWJF2ZuU3ONMQB2IXwgW8mqtELfvg8It9TIjX8onQEZPuvZGHS9CpUYwm8mQhZ3CzyvJMDq_KfSN9ngUl3M3QntC4Iv3J1FNSCgeUL7LxQtq_guz4F21PDfggd2R0cCvzzBRw31RBysVqU_A73qpnSC8DERBXAEe_2TXJ-Z7XE-qhh7izZyppWhCPeiAdAeurehF-zKlMAOEjIGnk__v1W00__y30000)

        + Giải thích:
            - Employee

                + Mục đích: Lưu trữ thông tin của từng nhân viên, cho phép quản trị viên thực hiện các thao tác thêm, sửa, xóa nhân viên.
                + Thuộc tính:
                    - employeeId: ID duy nhất của nhân viên.
                    - name: Tên của nhân viên.
                    - employeeType: Loại nhân viên (theo giờ, lương cố định, có hoa hồng).
                    - salary: Mức lương của nhân viên.
                + Phương thức:
                    - create(employeeData: Map<String, Object>): Tạo mới thông tin nhân viên.
                    - update(employeeData: Map<String, Object>): Cập nhật thông tin nhân viên.
                    - delete(employeeId: int): Xóa thông tin nhân viên.

            - EmployeeInfoUI

                + Mục đích: Giao diện cho phép quản trị viên tương tác để thêm, sửa hoặc xóa thông tin nhân viên.
                + Phương thức:
                    - openEmployeeInfo(): Mở giao diện thông tin nhân viên.
                    - displayConfirmation(): Hiển thị kết quả sau khi thực hiện thao tác.

            - EmployeeInfoController

                + Mục đích: Điều khiển quá trình quản lý thông tin nhân viên, đảm bảo các thay đổi từ EmployeeInfoUI được thực hiện thông qua Employee.
                + Phương thức:
                    - addEmployeeInfo(employeeData: Map<String, Object>): Thêm mới thông tin nhân viên.
                    - updateEmployeeInfo(employeeData: Map<String, Object>): Cập nhật thông tin nhân viên.
                    - deleteEmployeeInfo(employeeId: int): Xóa thông tin nhân viên.


5. Run Payroll (Chạy Bảng lương)
    - Các lớp phân tích chính
        + Entity:

            - Employee: Chứa thông tin về lương của nhân viên.
            - Payroll: Thực thể xử lý tính toán bảng lương.
        + Boundary:

            - PayrollUI: Giao diện để hiển thị thông tin về quá trình chạy bảng lương.
        + Control:

            - PayrollController: Điều khiển quy trình tính toán bảng lương cho nhân viên.

    - **Biểu đồ Sequence cho Run Payroll**  
        ![Diagram](https://www.planttext.com/api/plantuml/png/V54x3i8m3DrpYenqu08TK2LWw5Q1UW2JUeZa9bNY8ELi31o9Az2g3GegPVDxVXzBVZsUbMTm77eIeDWwUOsUiHSt6qm7Bie6ehD4RIsKDJoEYJdEaD09DAmvodC_a8s82Iz28UPCkJ-ilQNKHhC6ncMrAyHAD3bJU2aTijDunyISW65q9RXHWvdwTyD2bb81gK3PIRdtSzv6pp1J5_I1-6zHMvUoqtuWY4rksdr55A92qqt_UGC00F__0m00)

    - **Các biểu đồ lớp mô tả lớp phân tích và giải thích**  
        ![Diagram](https://www.planttext.com/api/plantuml/png/Z9512i8m44NtEKMM5VG2HQIWBheGHV40OpjAP9gKP2e4yMGkF99Nq9Qq5AhYR0R-dtb_I9xtH-8OB5S5YOp0ERaiIZ8UKLw5R0g3aEQnL9g3we30-bWUoK2hMMIhy88jOW4CqIYMAoYdkxUbJsEvFfmnuvcuYP2t0MyDKHUN0MKL0MCm8kpHFhB-JDYdNKQkN4dWWx55Ln57jcdV4Yv6vGFat6YkEzeEhRHYrRk-jxhpZh6Gaybik2-6n7gkVSalTb1_k_jK9AZp-eTV0000__y30000)

        + Giải thích:
            - Employee

                + Mục đích: Đại diện cho từng nhân viên, lưu trữ thông tin cần thiết để tính lương.
                + Thuộc tính:
                    - employeeId: ID duy nhất của nhân viên.
                    - salary: Mức lương cơ bản của nhân viên.
                + Phương thức:
                    - retrieveEmployeeData(): Lấy dữ liệu nhân viên phục vụ tính toán lương.
            - Payroll

                + Mục đích: Thực hiện việc tính toán bảng lương cho nhân viên.
                + Phương thức:
                    - calculatePayroll(employeeData: Map<String, Object>): Tính lương dựa trên dữ liệu của nhân viên.
            - PayrollUI

                + Mục đích: Giao diện người dùng hiển thị kết quả bảng lương sau khi chạy.
                + Phương thức:
                    - displayPayrollResult(result: Map<String, Object>): Hiển thị kết quả bảng lương của nhân viên.
            - PayrollController

                + Mục đích: Điều khiển quá trình tính lương, khởi động và điều phối tính toán bảng lương.
                + Phương thức:
                    - initiatePayroll(): Khởi tạo và tính toán bảng lương cho tất cả nhân viên.

6. Maintain Purchase Order
    - Các lớp phân tích chính
        + Entity:

            - PurchaseOrder: Lớp lưu thông tin về đơn hàng của nhân viên có hoa hồng, bao gồm thông tin khách hàng, sản phẩm mua, và ngày tạo đơn hàng.
        + Boundary:

            - PurchaseOrderUI: Giao diện cho nhân viên nhập liệu để tạo, cập nhật hoặc xóa đơn hàng.
        + Control:

            - PurchaseOrderController: Điều khiển các thao tác trên đơn hàng, đảm bảo rằng chỉ nhân viên có hoa hồng mới có thể truy cập và chỉnh sửa thông tin đơn hàng.
    - **Biểu đồ Sequence (Sequence Diagram) cho Maintain Purchase Order**  
        ![Diagram](https://www.planttext.com/api/plantuml/png/f99D2i8m48NtEKMMxS8BT252TU5AGNg0iHana6JAP2hqR2uyabUmhO8OnH_SJ9WNtlicPCx7qomAiBJUAQY5M9ValOtHKa2py8sZ3b5jgGq6kDFhbkizH5onGQwMggOWJEvHBw-YGrOOn4fYK-eLGq-cQNgXgS6GY5ck4kN9UUSNkcO4wUMgCUFPNsSqr3a8955ttrDaeG_WxEU8jxFS8lfdRmIaZJ_G8np-8G_sljzPzYF_Q_Bm2SR6na4tzjV1ipGlLpCCPbYY2m000F__0m00)

    - **Các biểu đồ lớp mô tả lớp phân tích và giải thích**  
        ![Diagram](https://www.planttext.com/api/plantuml/png/b59BJWCn3Dtd55aE4ht025MLMXPTm21LFO19B0ZAJx63L25Ene8ZSGMO7sKoKD4i7CdsizzxoSVR-ueO4cTdXR909DV1EKDaWaTzxQ8D1qJv8cHtS4XiTIsDvo7hmM4jTvoCVnXIAY4mtkMa7e6mIHfJ5Tgu0OPQta2ywlilPNF_X8gN5xLy3aQBLp4GcO2_6NH3fkjL9WuEq-sSHan1PyKRP32MYkB8vmlKnWdpVvBj8JdgSo4QBOwGGSrf0_RRemKHVL6hYkc6eeL3LzmnSAQAkcjquFIkTV2SWhK_REzTQTA-athcU_xwfHQBPQbGb8fdFKTcuY_6CunOeTVj__u4003__mC0)

        - Giải thích:
            + CommissionedEmployee

                - Mục đích: Đại diện cho nhân viên hưởng hoa hồng, có quyền tạo và chỉnh sửa đơn hàng mua để nhận hoa hồng.
                - Thuộc tính:
                    + employeeId: ID của nhân viên.
                    + name: Tên của nhân viên.
                - Phương thức:
                    + createPurchaseOrder(orderData: Map<String, Object>): Tạo đơn hàng mới để nhận hoa hồng.

            + PurchaseOrder

                - Mục đích: Lưu trữ thông tin về đơn hàng, phục vụ cho việc tính toán hoa hồng của nhân viên.
                - Thuộc tính:
                    + orderId: ID duy nhất của đơn hàng.
                    + customerName: Tên khách hàng.
                    + productDetails: Chi tiết sản phẩm mua.
                    + orderDate: Ngày tạo đơn hàng.
                - Phương thức:
                    + create(orderData: Map<String, Object>): Tạo mới một đơn hàng.
                    + update(orderData: Map<String, Object>): Cập nhật thông tin đơn hàng.
                    + delete(orderId: int): Xóa đơn hàng khỏi hệ thống.

            + PurchaseOrderUI

                - Mục đích: Giao diện cho phép nhân viên tạo và quản lý đơn hàng mua.
                - Phương thức:
                    + openPurchaseOrderUI(): Mở giao diện quản lý đơn hàng mua.
                    + displayOrderStatus(status: String): Hiển thị trạng thái sau khi tạo hoặc cập nhật đơn hàng.

7. **Code Java mô phỏng ca sử dụng Maintain Timecard**

    import java.util.HashMap;

    import java.util.Map;

    class Timecard {

        private Map<String, Integer> hoursWorked = new HashMap<>();

        private boolean submitted = false;

        public void addHours(String date, int hours) throws Exception {

            if (submitted) {

                throw new Exception("Timecard đã được gửi, không thể chỉnh sửa.");

            }

            if (hours < 0 || hours > 24) {

                throw new IllegalArgumentException("Số giờ phải trong khoảng 0 - 24.");

            }

            hoursWorked.put(date, hours);

        }

        public void submit() {

            if (!submitted) {

                submitted = true;

                System.out.println("Timecard đã được gửi.");

            }

        }
        
        public void display() {

            System.out.println("Chi tiết Timecard:");

            hoursWorked.forEach((date, hours) -> System.out.println("Ngày: " + date + ", Giờ làm: " + hours));

            System.out.println("Trạng thái: " + (submitted ? "Đã gửi" : "Chưa gửi"));

        }

    }

    public class Main {

        public static void main(String[] args) {

            try {

                Timecard timecard = new Timecard();

                timecard.addHours("2024-11-01", 8);

                timecard.addHours("2024-11-02", 6);

                timecard.display();

                timecard.submit();

                timecard.display();

                timecard.addHours("2024-11-03", 5);

            } catch (Exception e) {

                System.out.println("Lỗi: " + e.getMessage());

            }

        }

    }

