# Tài liệu Thiết kế Hệ thống Con cho Payroll System

## 1. Giới thiệu

Hệ thống **Payroll System** được thiết kế để tự động hóa quy trình quản lý lương của **Acme, Inc.**. Hệ thống này chia thành 5 hệ thống con:
1. **Quản lý thẻ chấm công**.
2. **Tạo và tính toán phiếu lương**.
3. **Hiển thị phiếu lương**.
4. **Báo cáo hiệu suất và lương nhân viên**.
5. **Quản lý thông tin nhân viên**.

---

## 2. Tổng quan Kiến trúc Hệ thống

### 2.1 Biểu đồ Thành phần
https://www.planttext.com/api/plantuml/png/XD4zJWCn40NWVaynsZuNe40HFu862K544wMmdD7QaZssl5xG2b5JKt20WDBGG46rBbAib7lu15o18H0GIX0kflBxDCz-IujYM4SHOcDD8PtrZf0YbAUY3SuOE6_hYBQ4wmBuZ4VQeXHX2YU2H8MMxqvWCDY5yJfmX8H1HEre0ZjGxZTKWSpTt4DKkKiWUSujoFwLgl8JtHRzPLvelD9KhS23d9x1w9nk6_1AvsxHW5c-B6SRt7TgPPsXTo6kbRr-vdW77Z6dUrvHvVJelu13wurh4JTBRgtFt4Xzr07cWLJ_G72f-oVwb_lZpOwv7DGvtVqKkoc6I5F-etS0003__mC0
## 2.2. Bảng Mô tả Hệ thống Con

| Hệ thống con            | Chức năng chính                        | Mô tả ngắn gọn                                                                 |
|--------------------------|----------------------------------------|--------------------------------------------------------------------------------|
| **Timecard Management**  | Thêm, sửa, xóa thẻ chấm công          | Quản lý thời gian làm việc hàng ngày của nhân viên, đảm bảo dữ liệu chính xác để tính lương. |
| **Payroll Generation**   | Tính toán lương dựa trên giờ làm việc và các hệ số lương | Sử dụng thẻ chấm công và thông tin nhân viên để tạo phiếu lương chi tiết cho mỗi nhân viên. |
| **Payroll Viewing**      | Hiển thị phiếu lương chi tiết theo tháng hoặc năm | Cho phép nhân viên và quản lý xem thông tin chi tiết về phiếu lương đã được tạo. |
| **Reporting**            | Tạo báo cáo hiệu suất làm việc và tổng hợp lương nhân viên | Cung cấp dữ liệu báo cáo cho quản lý để đưa ra quyết định chiến lược.         |
| **Employee Management**  | Thêm, sửa, xóa thông tin nhân viên    | Đảm bảo rằng thông tin nhân viên luôn được cập nhật, bao gồm lương cơ bản, chức vụ, và các thông tin cá nhân khác. |

---

## 3. Mô tả Chi tiết Từng Hệ thống Con

### 3.1. Timecard Management Subsystem

#### Mục tiêu
- Quản lý dữ liệu thời gian làm việc của nhân viên.
- Hỗ trợ nhân viên dễ dàng thêm hoặc chỉnh sửa thẻ chấm công.

#### Biểu đồ Trình tự (Sequence Diagram)
https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aO9Vnk55UM6PXrVbSHK09JAJCmiIyqeKF1xkRW_9UBXxObwwGcAnGd1bSKbgBeeAvs0N7v2KIs99Ob9YSIeN5y8e1Lqxg1OhXICJZZG33SdBUBXhRG4NH1Ga3z9lfU2T-N1tSwv2IL6YGad6uIr0XIMPULnWitMH38aul30POaGU3cj2CWwl0fe3LB9R8Hb8BirLI0QPXs6Zpx4DfKXsOTE2ptg57A1-kA50DGZdM2buW7m3Dd9tDz1F3tSj15cISNXX9eXSa9S1jS0XDIy560K00000__y30000
### Chức năng chi tiết:

| Tên chức năng       | Mô tả                                                 | Đầu vào                    | Đầu ra                           |
|---------------------|-------------------------------------------------------|----------------------------|----------------------------------|
| Thêm thẻ chấm công  | Nhân viên nhập thông tin giờ bắt đầu và kết thúc ca làm việc. | Nhân viênID, Giờ làm việc   | Thẻ chấm công được lưu.         |
| Sửa thẻ chấm công   | Nhân viên chỉnh sửa giờ làm hoặc xóa thẻ chấm công.  | Mã thẻ chấm công            | Dữ liệu thẻ được cập nhật.      |
## 3.2. Payroll Generation Subsystem

### Mục tiêu:
Tự động hóa quy trình tính lương dựa trên thẻ chấm công và thông tin nhân viên.

### Biểu đồ Hoạt động (Activity Diagram):

https://www.planttext.com/api/plantuml/png/J90nQiD044NxFSKlvIj8HLoa2xXAarAHPEt2QYIqAr_0XUiK8LN0IaWJC4aWbRPmiU1xp0boXOm38jvY-F3VxF_CJpWkdSzxFpHM_GcLhZHF1qAPauQBOw51EhuGDYQ-KwRI6yDXsy3tERoW0ONCjmP5_AOwKsQDv9h31wnmkm6Qmsi7A_fg8GiL8Rcht491NdeR3vBYEJnIZLeMdc7ZliakNNlwF8rYbno-9BAN5XSeDd5_pjZ1SNYOuVa3diOMdJOy7OT_hxAkGh9gvnBwt1ptKLZf-MI4eDAivI1jfvQYvJg_0000__y30000
## Chức năng chi tiết:

| Tên chức năng   | Mô tả                                               | Đầu vào                             | Đầu ra               |
|-----------------|-----------------------------------------------------|-------------------------------------|----------------------|
| Tạo phiếu lương | Tính toán lương hàng tháng dựa trên giờ làm và hệ số lương. | Thẻ chấm công, thông tin nhân viên | Phiếu lương chi tiết.|

## 3.3. Payroll Viewing Subsystem

### Mục tiêu:
Hiển thị phiếu lương chi tiết cho nhân viên và quản lý.

## Chức năng chi tiết:

| Tên chức năng   | Mô tả                                               | Đầu vào                             | Đầu ra               |
|-----------------|-----------------------------------------------------|-------------------------------------|----------------------|
| Tạo phiếu lương | Tính toán lương hàng tháng dựa trên giờ làm và hệ số lương. | Thẻ chấm công, thông tin nhân viên | Phiếu lương chi tiết.|
## 3.4. Reporting Subsystem

### Mục tiêu:
Tạo các báo cáo tổng hợp cho quản lý.

### Biểu đồ Thành phần chi tiết:

https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bT1Od9sOdggWb9GQa5-KKbcNhf2S6bISMLnIMgkaa8rbm8G9ESa5XShE1rUcEyCn3x7DXnR25G6aOE0aeUx5kR358Ha70RAQsY2vMkvi1ZXdlbmzrmy1fG-tBKy3vy1Blc9UHaX6QMupV0xqfmBDw6Moo4rBmNeNG00003__mC0
## Chức năng chi tiết:

| Tên chức năng       | Mô tả                                               | Đầu vào   | Đầu ra           |
|---------------------|-----------------------------------------------------|-----------|------------------|
| Báo cáo lương tháng | Tổng hợp lương từng tháng của nhân viên.           | Tháng     | Báo cáo chi tiết.|

## 3.5. Employee Management Subsystem

### Mục tiêu:
Quản lý thông tin cá nhân của nhân viên.

### Biểu đồ Trạng thái:

https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTWdF6iGs9HoOSQSvBzyjuk6jj0HU6Y09G6GhVIW7AACaul2KlNQ4aCuyBKyFXnMYQ8WulJ5R80_7oa7Gg79buU5TUEXU61g0XmGzthqqC0IiD0QgqKd06ou3DA46s7KqXTljzZcqe1MbQa9UXa0nIYiLEe4vGo5X1FQnGKVfmrz8IBeVKl1HWg040003__mC0


