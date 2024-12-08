# Thiết Kế Lớp - Hệ Thống Payroll System

## Mục lục

1. [Giới thiệu](#giới-thiệu)
2. [Các lớp trong hệ thống](#các-lớp-trong-hệ-thống)
3. [Biểu đồ lớp](#biểu-đồ-lớp)
4. [Biểu đồ trạng thái](#biểu-đồ-trạng-thái)
5. [Phụ thuộc và quan hệ kết hợp](#phụ-thuộc-và-quan-hệ-kết-hợp)

---

## Giới thiệu

Hệ thống **Payroll System** giúp quản lý thông tin nhân viên, chấm công, tính lương và tạo báo cáo lương. Mỗi nhân viên có thể có nhiều phiếu chấm công, mỗi phiếu chấm công sẽ được duyệt và tính lương. Hệ thống này cũng hỗ trợ tạo báo cáo lương cho nhân viên.


## Các lớp trong hệ thống
![](https://www.planttext.com/api/plantuml/png/d9KxZjim48PxdMBW9dOGBv9M21QBo9sr1X8BxcTbGIHM8XsRNC08KgT8apvLobGvW8iKsOlu1Bb2-90eKegSHsV-_3ap_6PC_Jnzlpa8t0jPLz4JUFnqFdra15X97hyYLEVJvnsi2B8DBLYKLtWuk2MyYm3cKEDg4yDQx2ahZI0A5gnPYSSrPII61Oh2I0yqszF0L4dEIkKeSbfZPQGxP6L2i4xCJaeFukKhJxgEb0j0aABsvMbupD-QnV30wTOUKmMbEkTqvcS5gF2O4QLdbBKNrHPNAa2EExKZx6bJzosdBeYVHCNQw9jw0Tv7OvJzIXlIlZH6MzFro9QKfrY78AsMAL2XBlOgVaQmwuIfUYkFXGYG1k1aGZWTtswvwdHzjeplHWzgxcqzVytBPF9WcVKOgT-CMDLM6ihtX2DR4fGPaKMF6P6g-RitGQW_trnlBlse0mDoTu41bsOU0yDm88SsqIXcFftSHh-4bYV8GxXEQV1kaP4rviI5zVwYPdtjnjCUReQqkwqM__Mgoh9o4Gr3E_XgX-TMLVYvzanjQh50QMtFJ37BGe6IkPLcmwB7gRoMoD9Zibwa3PHEQ9ZS5sAbKQlXPaKkA6UHgxfvItHrjpZrXrCLuLvOuvRoFnwqvfI5TjSrPT1sRsBS0yUQ7rqblRvu_P-QpuMcrs8jsBPRZY5DVdp9uQqY1kHy-g3UfFFf6qAkLOCtSf-LoOi9pESmUNvrzNGIle4nvFoIqGvehEShwjPzNpVArkdrCRIwJB6fF3sEMtjbgcvSzhRvjJ6wKGJrz_SN0000__y30000)
### 1. Lớp `Employee` (Nhân viên)

- **Thuộc tính**:
  - `id`: Mã nhân viên (String)
  - `name`: Tên nhân viên (String)
  - `dob`: Ngày sinh (Date)
  - `position`: Chức vụ (String)
  - `salary`: Lương cơ bản (Decimal)
  - `timecards`: Danh sách các phiếu chấm công (List<Timecard>)

- **Operations**:
  - `addTimecard(Timecard)`: Thêm phiếu chấm công cho nhân viên.
  - `calculateSalary()`: Tính lương của nhân viên dựa trên giờ làm việc.
  - `getEmployeeDetails()`: Lấy thông tin chi tiết của nhân viên.

### 2. Lớp `Timecard` (Phiếu chấm công)

- **Thuộc tính**:
  - `employeeId`: Mã nhân viên (String)
  - `date`: Ngày làm việc (Date)
  - `hoursWorked`: Số giờ làm việc (Decimal)
  - `overtimeHours`: Số giờ làm thêm (Decimal)
  - `status`: Trạng thái phiếu chấm công (String, ví dụ: "Approved", "Pending")

- **Operations**:
  - `approveTimecard()`: Duyệt phiếu chấm công.
  - `rejectTimecard()`: Từ chối phiếu chấm công.

### 3. Lớp `Payroll` (Phiếu lương)

- **Thuộc tính**:
  - `employeeId`: Mã nhân viên (String)
  - `salary`: Lương cơ bản (Decimal)
  - `overtimePayment`: Tiền làm thêm (Decimal)
  - `taxDeduction`: Khấu trừ thuế (Decimal)
  - `netPay`: Lương sau thuế (Decimal)

- **Operations**:
  - `calculateOvertimePayment()`: Tính tiền làm thêm.
  - `calculateTaxDeduction()`: Tính khấu trừ thuế.
  - `generatePayroll()`: Tạo phiếu lương cho nhân viên.

### 4. Lớp `PayrollReport` (Báo cáo lương)

- **Thuộc tính**:
  - `payrollList`: Danh sách phiếu lương (List<Payroll>)
  - `reportDate`: Ngày báo cáo (Date)

- **Operations**:
  - `generateReport()`: Tạo báo cáo lương cho một kỳ cụ thể.
  - `getPayrollDetails()`: Lấy thông tin chi tiết về các phiếu lương.

### 5. Lớp `DatabaseManager` (Quản lý cơ sở dữ liệu)

- **Thuộc tính**:
  - `connection`: Kết nối cơ sở dữ liệu (Connection)

- **Operations**:
  - `getEmployeeById(String id)`: Lấy thông tin nhân viên theo mã nhân viên.
  - `saveTimecard(Timecard timecard)`: Lưu phiếu chấm công vào cơ sở dữ liệu.
  - `savePayroll(Payroll payroll)`: Lưu phiếu lương vào cơ sở dữ liệu.
## Biểu đồ Trạng thái
![](https://www.planttext.com/api/plantuml/png/f5CzReCm5DvzYhULLCe56AgeeLA6AEg0kbHLzGeMjW8sedObvevTUeHcx1N2a26v22Ve5Mf3VWY1I54c_Dxt-VkUlcV-YjNeNM6cT1AJ6zXybyMNO20Yjlb5K5cvN8W855ilE7oiVo1WEY-BJm6AbyjLQce9zoYYCSDaB0tLyNb20yp20Nc-VO7XyEu8V_MgGdewfugGNgZhOWsu4Dfl4tC6bmdvsg3SAAdgq99gQ_NAD4nS438zFzBMz7AT_dbCm6TSB7hDIgUwskSZvfcCu-DrLfYrGrdFrsYSa4JaSy5yYS96RevxS9jI1_74YE5UuctNRxHRIWVwjKdCZD8JfmASXoIDPKxf8OaTLeq-aQWyuqv8PxjzOHRf1kWQBqmyhIOozUfWUhczpaPbpWDcoodo7SM-e14LeVt1_m400F__0m000)
## Biểu đồ lớp
![](https://www.planttext.com/api/plantuml/png/d5JBRi8m4BpdArOvGILGkKOLGWqtKgIMYFiIhDWYiLkmaL3LB-kXdzHVgECyM0UegXuzdbtFp6xo_VarEsZSQrCMGLRWuG1BZd8jc8Jt06049IxN4QpqNiZS0Pf9xonpFAs4v17CKJC77KMw5nwfC4hcbi4oKMBXe0tAFEPOnkuc4GVzy4YWgIK1QCvAYWxyAderZE2enBOkitgIwid1a3uAKE0fvHPFXMnzLfH6wKVGP43xtigXyaqyvq8bMFeMQoor7dnSxst_b2FD261hJanxPZrB9kPANBtsP3lRjpHV6OE3BYNkk4Avu6XIRbXFFJSskzUNNYkIUjMkdtnrkQ1DBmYeEltNhAaO5JMtHSbNcF6kY2oHEq-xCTN5tR2QjohCYvWiXwUalntF1cLoYbVpf96oOtgfx33jL2JBj52oxTSkcKr4FU603iGsRczhjZ7_sFIcgjQwEKVHWIJ9xiiE9o6CHbC8xyVZkz3VzWWo5NX8mt85jh3h4bMReB8rkzvu4f9zxBhMnmi1v-5Q9ZSOa8nxPFB-coFzmkqv-nE_bT6GWncJs-hl-0C00F__0m00)
## Biểu đồ thuộc tính
![](https://www.planttext.com/api/plantuml/png/b5F1QeGm4Btx5S5ZmKElKfPb5LgexCMmzwah9g39LfE2b7vP3_sa_a8dchL9t2rTRtdpvkMzoVZz-RKT5FHATsrKjJ0CPCz077Wjo7j4y4j81sSe9QNgkMXiGQqGqS1OSi5IaeEgBNZaa34UC0UPeo1b4i9AtG5lB-WUG1RGUSfldFPXk-f1D9IjP5ijHOFTKh-qTVGHsRGxP6SCkWohJc8N3eIkZiEOt87AGNic3VnSAyfqvU4AfKlvo6sgsTVV6OpKNfwiZ9UXqEi0XRxP_TBa69qcbqaiXZQPDrCBccSrquEmW5mwtVllh0WBHkLqiPVOF0iTdRWpiDxFYpWk92vV5w9uLmaL-vrFmGVrS3vk0fepguctd3V6vl8JnVSnIH8ItyN-ggNaLOCenglC-K5J8h0UsRmEPMbBYT9ZBOuQWwnfhjA9WNf2zz7MqF5__m400F__0m00)
## Biểu đồ phụ thuộc, quan hệ kết hợp
![](https://www.planttext.com/api/plantuml/png/b5H1IiD05DtFAOPk124Bjq5AQGeAXcuIkl-c8JEOpCHaHWZYsZEu5F4ITj659-a9l89_qfXE9gre5wLv__qtx_tvwTTcEwiLL4eNEKbog6kwP21MF1NqaL3yUBI07yYdaQguoBg26Y4YWoRYWlbq0Ihjm3M7W767MSi52iPCWbj92-3v4TqLo12AWV83ZoktNLKWifYDP7CjHORTKj_cANaYNTeviWC6HO1LAx4DEq8dns5Cpa4jG0zC6lWcLJ7JoG1NA1t9AzwbsllwFOEHMigoanba2FKuGAZ_xRvlieosamia5bsRR33J3ZJNQgO7RW6vSNlkdxCYB5WisuC7YSsrn8qLTm-Cz_CeZWk9orUuA9uLGS8EymbvhIv_7gSEpPfLo-kVfyRc6Gq-NnDwhq5GjjiyqxlTnrQPds-bJ_fNR78nePv79-UJuIBwRMVOd6Jkhzkd0kkacuP5wTjygdIJYhN6c6EQhLGoKDUOxOZt4h_VpMtlDY-9JmvTdZUrZogPnYsN2HbaEKMQ6Lluh_CD003__mC0)


