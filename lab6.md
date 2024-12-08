
# THIẾT KẾ LỚP HỆ THỐNG PAYROLL SYSTEM

## 1. **Lớp Employee (Nhân Viên)**
https://www.planttext.com/api/plantuml/png/Z5JBRjGm5DtdAwwoeLIQHRSHgeeqIAs4r3B33xZELMBas94VWqQeQnPiO8dOm0gnG7n05YocFv8lw2_WnB4R3zEgk_ZSw-DxZezpr_qzquOeOnkUPS_WzdFVVH8rYAg-_KM0xdvGu7tthONDxZkOslRTLmfczzlrqBxxIQ3kku-kq7TVH0LNPAiavx3UQeDDbb5Ej8PNJSlb5X4-P00Bm6bvKHQmDeg9QeG5QJ01IcpTO0qAay2jrCmmAHBGi0OfKQKku3NJviNRQNtggW3QNZVC1EmeD1SGeES5R2Ghn-ODm_UJZXMsKfcZUTMs9J4O52tH4CPrxBW9aWFnuvA7GIwSaAMZ77P4yDAQVLGQmi-bLKxXKjfhxc5tTyRgUo7hSJrEIWcdbWySSMkYXBIjaXjCC8Nla1uI7BrxKAa_UT8RnefQ0QvGbEuxmLxw4Se4N8qppC1uL4ZNevvgmedQ9YQv8zJWwl_sZQuwMX-oM9YPjnxf4aTYxNBYJQeL2bIkU3X2KSlvoh-HFJ4Xlo5WfpxodYiK9sgVRUSWHQqdxD0DFp7t_kwVq7mp_2ZUM2ByswzOt_sP_ogo-DxpanoE5ml8Z_Fx5r50JNGMzSzxuiO26Y98XG_qXI0KqMsTHVxOU9BlXzCVdPsvA0x_kty0003__mC0
### **Thuộc Tính (Attributes):**
- `employeeId` (String): Mã nhân viên, duy nhất.
- `name` (String): Tên nhân viên.
- `department` (String): Phòng ban của nhân viên.
- `position` (String): Chức vụ của nhân viên.
- `timecards` (List<Timecard>): Danh sách các thẻ chấm công của nhân viên.

### **Operations (Phép Toán):**
- `submitTimecard(timecard: Timecard): void`: Nhân viên gửi thẻ chấm công mới.
- `viewPayrollReport(): void`: Nhân viên xem báo cáo lương của mình.
- `updateEmployeeDetails(): void`: Cập nhật thông tin nhân viên.

### **Quan Hệ (Relationships):**
- Một **Employee** có thể có nhiều **Timecard**.
- Quan hệ: `Employee "1" *-- "*" Timecard : has`

---

## 2. **Lớp Timecard (Thẻ Chấm Công)**

### **Thuộc Tính (Attributes):**
- `employeeId` (String): Mã nhân viên.
- `timeIn` (DateTime): Thời gian vào làm.
- `timeOut` (DateTime): Thời gian ra về.
- `totalHours` (Double): Tổng số giờ làm.
- `status` (TimecardStatus): Trạng thái thẻ chấm công (Pending, Approved, Rejected).

### **Operations (Phép Toán):**
- `calculateTotalHours(): void`: Tính tổng số giờ làm của thẻ chấm công.
- `approve(): void`: Phê duyệt thẻ chấm công.
- `reject(): void`: Từ chối thẻ chấm công.
- `updateTimecard(): void`: Cập nhật thông tin thẻ chấm công.

### **Trạng Thái (States):**
- `Pending`: Thẻ chấm công đang chờ duyệt.
- `Approved`: Thẻ chấm công đã được phê duyệt.
- `Rejected`: Thẻ chấm công đã bị từ chối.

### **Quan Hệ (Relationships):**
- **Timecard** có một trạng thái **TimecardStatus**.
- Quan hệ: `Timecard "1" *-- "1" TimecardStatus : has`

---

## 3. **Lớp Payroll (Bảng Lương)**

### **Thuộc Tính (Attributes):**
- `employeeId` (String): Mã nhân viên.
- `salary` (Double): Lương cơ bản của nhân viên.
- `overtimeHours` (Double): Số giờ làm thêm của nhân viên.
- `totalPayment` (Double): Tổng số tiền phải trả cho nhân viên (lương cơ bản + làm thêm).

### **Operations (Phép Toán):**
- `calculateSalary(): void`: Tính lương cơ bản của nhân viên.
- `calculateOvertime(): void`: Tính số tiền làm thêm của nhân viên.
- `generatePayrollReport(): void`: Tạo báo cáo lương cho nhân viên.

---

## 4. **Lớp HRSystem (Hệ Thống Quản Lý Nhân Sự)**

### **Thuộc Tính (Attributes):**
- `employees` (List<Employee>): Danh sách tất cả nhân viên.
- `payrolls` (List<Payroll>): Danh sách tất cả bảng lương của nhân viên.

### **Operations (Phép Toán):**
- `processPayroll(): void`: Xử lý bảng lương cho tất cả nhân viên.
- `approveTimecard(timecard: Timecard): void`: Duyệt thẻ chấm công của nhân viên.
- `rejectTimecard(timecard: Timecard): void`: Từ chối thẻ chấm công của nhân viên.

### **Quan Hệ (Relationships):**
- **HRSystem** quản lý nhiều **Employee** và nhiều **Payroll**.
- Quan hệ: `HRSystem "1" *-- "*" Employee : manages`
- Quan hệ: `HRSystem "1" *-- "*" Payroll : generates`

---

## 5. **Biểu Đồ Trạng Thái (State Diagram)**

### **Trạng Thái Timecard**

- `Pending`: Thẻ chấm công chưa được duyệt.
- `Approved`: Thẻ chấm công đã được phê duyệt.
- `Rejected`: Thẻ chấm công bị từ chối.

```plaintext
[*] --> Pending
Pending --> Approved : approve()
Pending --> Rejected : reject()
Approved --> [*]
Rejected --> [*]
