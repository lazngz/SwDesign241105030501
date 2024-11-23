# Các Bước Thiết Kế Ca Sử Dụng (Use Case Design)

## 1. Xác định các Ca sử dụng (Use Cases)

- **Maintain Timecard**: Quản lý thẻ chấm công của nhân viên.
- **Generate Payroll**: Tạo phiếu lương từ giờ làm việc và doanh thu của nhân viên.
- **View Payroll**: Xem phiếu lương đã được tạo.
- **Generate Reports**: Tạo báo cáo cho các nhân viên hoặc cho quản lý.
- **Employee Information Management**: Quản lý thông tin của nhân viên.
  

## 2. Mô tả chi tiết từng Ca sử dụng

### 2.1. Maintain Timecard
- **Mô tả**: Ca sử dụng này cho phép nhân viên hoặc quản lý cập nhật thời gian làm việc của nhân viên vào hệ thống. Thẻ chấm công có thể được chỉnh sửa khi có sự thay đổi về giờ làm việc.
- **Tác nhân**: Nhân viên, Quản lý.
- **Mục tiêu**: Đảm bảo rằng tất cả giờ làm việc của nhân viên được ghi lại chính xác để tính lương.
- **Tiến trình chính**:
    1. Nhân viên hoặc quản lý đăng nhập vào hệ thống.
    2. Nhân viên chọn thẻ chấm công để sửa đổi.
    3. Nhân viên hoặc quản lý cập nhật thời gian làm việc.
    4. Hệ thống xác nhận và lưu lại dữ liệu thẻ chấm công.

### 2.2. Generate Payroll
- **Mô tả**: Ca sử dụng này cho phép hệ thống tự động tạo phiếu lương dựa trên thời gian làm việc và doanh thu của nhân viên.
- **Tác nhân**: Quản lý.
- **Mục tiêu**: Tạo phiếu lương đúng và chính xác cho tất cả nhân viên.
- **Tiến trình chính**:
    1. Quản lý đăng nhập vào hệ thống.
    2. Quản lý chọn nhân viên và tạo phiếu lương.
    3. Hệ thống tính toán lương và tạo phiếu lương.
    4. Phiếu lương được gửi tới nhân viên.

### 2.3. View Payroll
- **Mô tả**: Ca sử dụng này cho phép nhân viên và quản lý xem các phiếu lương đã được tạo.
- **Tác nhân**: Nhân viên, Quản lý.
- **Mục tiêu**: Cung cấp thông tin lương cho nhân viên và quản lý.
- **Tiến trình chính**:
    1. Nhân viên hoặc quản lý đăng nhập vào hệ thống.
    2. Nhân viên hoặc quản lý tìm kiếm và xem phiếu lương.

### 2.4. Generate Reports
- **Mô tả**: Ca sử dụng này cho phép quản lý tạo các báo cáo tổng hợp về lương, giờ làm việc và doanh thu của nhân viên.
- **Tác nhân**: Quản lý.
- **Mục tiêu**: Cung cấp các báo cáo tài chính và nhân sự cho các cấp quản lý.
- **Tiến trình chính**:
    1. Quản lý đăng nhập vào hệ thống.
    2. Quản lý chọn loại báo cáo cần tạo (theo lương, theo giờ làm việc, theo doanh thu).
    3. Hệ thống tạo báo cáo và hiển thị cho quản lý.

### 2.5. Employee Information Management
- **Mô tả**: Ca sử dụng này cho phép quản lý và nhân viên thay đổi hoặc cập nhật thông tin cá nhân.
- **Tác nhân**: Nhân viên, Quản lý.
- **Mục tiêu**: Đảm bảo rằng thông tin cá nhân của nhân viên được cập nhật và chính xác.
- **Tiến trình chính**:
    1. Nhân viên hoặc quản lý đăng nhập vào hệ thống.
    2. Nhân viên hoặc quản lý chỉnh sửa thông tin cá nhân.
    3. Hệ thống xác nhận và lưu thay đổi.

## 3. Tài liệu giải thích lý do thiết kế

### 3.1. Maintain Timecard
- Đây là một ca sử dụng cơ bản trong hệ thống Payroll, đảm bảo rằng tất cả giờ làm việc của nhân viên được ghi nhận chính xác. Quản lý hoặc nhân viên có thể sửa đổi thời gian làm việc nếu có sự thay đổi (ví dụ: tăng ca hoặc nghỉ phép).

### 3.2. Generate Payroll
- Tính năng này rất quan trọng để đảm bảo phiếu lương được tạo tự động từ dữ liệu có sẵn mà không cần can thiệp thủ công. Nó giúp tiết kiệm thời gian và tránh sai sót khi tính toán lương.

### 3.3. View Payroll
- Cung cấp khả năng xem phiếu lương cho nhân viên và quản lý giúp tăng tính minh bạch trong hệ thống lương. Nhân viên có thể dễ dàng theo dõi thông tin lương của mình.

### 3.4. Generate Reports
- Báo cáo là yếu tố quan trọng trong việc ra quyết định quản lý, giúp đánh giá hiệu suất và chi phí. Ca sử dụng này cho phép tạo các báo cáo tài chính và nhân sự giúp quản lý nắm bắt thông tin quan trọng về lương và giờ làm việc.

### 3.5. Employee Information Management
- Việc quản lý thông tin nhân viên là cần thiết để hệ thống có thể xử lý đúng các yếu tố như tính lương, báo cáo, và các quyền lợi khác. Đây là một tính năng cơ bản và cần thiết trong hệ thống Payroll.

