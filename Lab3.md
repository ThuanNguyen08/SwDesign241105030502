# Welcome
## Lab3
### Nguyễn Văn Thuận - 4451050990
# ------------------------------------------------------------

# ***Xác định các phần tử thiết kế của hệ thống `Payroll System`***

1. Subsystem context diagrams.
    - Subsystem context diagrams  
        ![Diagram](https://www.planttext.com/api/plantuml/png/h5BBJiCm4BpdArQvK2JQtYihga0SSgle5nXdIwqaTkHr417qopZmIVm2jlF0IJaYHR8pEpExiydtvzUUB3UshQkauQBaBmWft7DL7ZkoMCEnVQPmI-4z0N3F3HnuPtHLFMXb_Od6eQBYHDSLO4pqBraM302sMp2jWgQdhcuTU1cTSsNHdBX0o7zdS1Nv5pxu5TXeadR5NNDnHb723iRhdLTgBt6WFt9rqgRcLcerQpp5X8FHRntCklVPeiQCqSHlF7yAzo_3F2ehRJVfuktsdenXe0njbyA5zon1X0_Qe7p2Ac1qbWqvvFf3hjVPRFaxI0jfKDWnCq4OZk1LyjHPn6JsiTdCTnfNlNKKTbbQnhaaUrI5_sD_0000__y30000)

        + IBankSystem: Đóng gói giao tiếp với tất cả các hệ thống ngân hàng bên ngoài.
        + deposit: Gửi tiền lương đã chỉ định vào ngân hàng đã chỉ định.

    - PrintService Subsystem  
        ![Diagram](https://www.planttext.com/api/plantuml/png/d591JiCm4Bpx5QjSA19DuHfPKQMAGsyHUO5n5shXEf6zgHe1B-F0a_W2jXC2XlJ2nLvxPsTcr_vuUryx4fQwWsONK8dUDbfl6aDXHmjI2-TON6UodClXK9Rmp01MAx2TWNO0BYxPA_EiMqDe7uH4s5PM6QhH7fL4fkRl8nEquMOXlARSeto20hx2AsXCn7i31TJamyTHgUxkNUy83r3PvjH38ZSsyLE9SpTLjA5YxEDVuhU65FKJydje0mVd605H8XRSeHQa6kFsgdNixtINo_BNP0h8md0ZuUWYOoc4l-HvsdUQ3wIJnVCPRsyZx4uPeHKfdBENNUVvJHRBnZ1ztZMQNVXMdm000F__0m00)

        + IPrintService: Bao gồm giao tiếp với tất cả máy in.
        + print: In Bảng lương đã cho trên máy in được chỉ định.

    - Project Mangement Datebase Subsystem  
        ![Diagram](https://www.planttext.com/api/plantuml/png/f9J1Ji9048RlVOe95y6ae5T220bSJDGOyGMMxL3MjBlDx5GbwfDvy95y1HTRB1lA1hIdPcR-dN-__kdNn-V4iY0kyomwWnakbKPuK3bAGSdKQ2QJPKWWCs4jF2jUmMWag_fu39QHqF2wmAYQQ97kphz6u9x1059aa2KHQWQkDTsUrrq9IX6aIT0sdR9816EBn8edh_mUkVlSOoPO6MrNge0bcRpD7nkukYFpY99lX1OfvixKJB1O28jHYw1pqU-VTo2Enp-lbvs07ePGt-IspEUc98bH0pgWKzgXNGg9M-Y_1HzxCnSup5TN7y4ndcwDBP1iLv9oCqeCOSwaTDeRDiwlbUKAQUtyy2ulARPSsBLpcqD1vcNTbfYGwttvlxplno70pCNYS2f2hD_YEA1i44vt3LROQYHUvo_6_GC2iviC7x7jX6KdxPgWJZP_dcy0003__mC0)

        + IProjectManagementDatabase: Đóng gói giao tiếp với Cơ sở dữ liệu quản lý dự án cũ chứa thông tin về số phí của dự án.
        + getChargeNumbers: Truy xuất số điện tích khả dụng.

2. Ánh xạ các lớp phân tích đến các phần tử thiết kế.
    - LoginForm(AC) -> LoginForm(DE)
    - Maintain TimecardForm(AC) -> MainEmployeeForm(DE), TimecardForm(DE)
    - TimecardController(AC) -> TimecardController(DE)
    - SystemClockInterface(AC) -> SystemClockInterface(DE)
    - PayrollController(AC) -> PayrollController(DE)
    - Paycheck(AC) -> Paycheck(DE)
    - HourlyEmployee(AC) -> HourlyEmployee(DE)
    - Timecard(AC) -> Timecard(DE)
    - Purchase Order(AC) -> Purchase Order(DE)
    - CommissionedEmployee(AC) -> CommissionedEmployee(DE)
    - SalariedEmployee(AC) -> SalariedEmployee(DE)
    - Employee(AC) -> Employee(DE)
    - BankSystem(AC) -> BankSystem subsystem(DE)
    - PrinterInterface(AC) -> IBankSystem interface(DE), IPrintService subsystem(DE)
    - ProjectManagementDatabase(AC) -> Project ManagementDatabase subsystem, IProjectManagementDatabase interface(DE)

    - note: Analysis Class(AC), Design Element(DE)

