# LAB1: PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG
## 1. Phân tích kiến trúc
## Đề Xuất Kiến Trúc
Hệ thống Payroll System sẽ được xây dựng theo **kiến trúc phân lớp (Layered Architecture)** với các tầng sau:
1. **Presentation Layer (UI Layer)**: 
   - Giao diện desktop Windows cho nhân viên.
   - Cung cấp khả năng nhập chấm công, quản lý đơn hàng, tùy chọn thanh toán và xem báo cáo.

2. **Business Logic Layer (Application Layer)**:
   - Tầng xử lý nghiệp vụ chính, bao gồm tính lương và quản lý logic liên quan.
   - Giúp tách biệt logic nghiệp vụ khỏi tầng giao diện và tầng dữ liệu.

3. **Data Access Layer**:
   - Tầng truy cập dữ liệu, thực hiện lấy và lưu trữ thông tin từ/đến cơ sở dữ liệu nội bộ.
   - Tương tác với DB2 của Project Management Database để truy xuất thông tin dự án và mã chi phí.

4. **External Integration Layer**:
   - Kết nối với hệ thống DB2 trên IBM mainframe.
   - Lấy thông tin dự án và mã chi phí mà không làm thay đổi dữ liệu, đảm bảo tính nhất quán.

### Lý Do Lựa Chọn Kiến Trúc Phân Lớp

Kiến trúc phân lớp có nhiều ưu điểm phù hợp cho Payroll System:
- **Dễ bảo trì và mở rộng**: Các tầng chức năng riêng biệt giúp hệ thống dễ dàng bảo trì khi có thay đổi trong từng tầng mà không ảnh hưởng đến các tầng khác.
- **Tính bảo mật và kiểm soát**: Chỉ có tầng dữ liệu mới trực tiếp làm việc với cơ sở dữ liệu, giúp hạn chế truy cập trái phép từ tầng giao diện.
- **Dễ kiểm thử**: Tầng business logic được tách biệt giúp việc kiểm thử dễ dàng và chính xác hơn.

## Biểu Đồ Package
![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bT1Od9sOdggWb90OcLHVawEGd1bSKbghf92DPU20X31v5rp2tBoArDJmUArN4WoC8qO4Y6PkQd9YKKfMBNafkQL-AQMPEHZaoxApqfDBl5Dp0FoG0ezyqfIquiIIpBpyw2gmMw3kyb6LnVc37HXc2EmA4Su0IW9ymLO3e_zNBLS3gbvAQ2W0m000F__0m00)

## 2. Cơ Chế Phân Tích

Trong hệ thống Payroll System, một số cơ chế quan trọng cần được triển khai để đáp ứng yêu cầu nghiệp vụ và đảm bảo hiệu quả hệ thống. Dưới đây là các cơ chế phân tích cần thiết và lý do chọn lựa:

1. **Cơ Chế Xử Lý Thanh Toán**:
   - Tự động tính toán và xử lý thanh toán dựa trên loại hình lương của nhân viên (lương giờ, lương cố định, hoa hồng).
   - Đảm bảo thanh toán đúng hạn vào thứ Sáu hàng tuần và ngày làm việc cuối cùng của tháng.
   - Lý do: Cơ chế này giúp đảm bảo độ chính xác và tự động hóa quá trình tính lương, tránh lỗi thủ công và tối ưu hóa thời gian.

2. **Cơ Chế Xác Thực Người Dùng và Kiểm Soát Truy Cập**:
   - Xác thực nhân viên khi đăng nhập để đảm bảo quyền truy cập phù hợp.
   - Chỉ cho phép nhân viên xem và chỉnh sửa thông tin của chính họ.
   - Lý do: Đảm bảo tính bảo mật và phân quyền cho hệ thống, tránh truy cập trái phép vào dữ liệu của người khác.

3. **Cơ Chế Quản Lý và Theo Dõi Chấm Công**:
   - Ghi lại giờ làm việc và mã chi phí của nhân viên dựa trên các bảng chấm công.
   - Tự động tính lương làm thêm giờ khi số giờ vượt quá quy định.
   - Lý do: Cơ chế này hỗ trợ việc ghi nhận chính xác thời gian làm việc và tính toán thêm giờ, giúp tính lương chính xác hơn cho nhân viên làm việc theo giờ.

4. **Cơ Chế Tích Hợp Hệ Thống DB2**:
   - Kết nối và truy xuất dữ liệu từ DB2 của Project Management Database.
   - Không thay đổi dữ liệu gốc mà chỉ truy xuất thông tin dự án và mã chi phí.
   - Lý do: Hỗ trợ tích hợp thông tin dự án mà không ảnh hưởng đến hệ thống cũ, giúp hệ thống Payroll lấy thông tin chính xác và đồng nhất.

5. **Cơ Chế Báo Cáo và Truy Vấn Dữ Liệu**:
   - Hỗ trợ nhân viên xem báo cáo như số giờ làm việc, tổng lương, số giờ theo mã chi phí, và số ngày nghỉ còn lại.
   - Lý do: Cung cấp cho nhân viên khả năng tự kiểm tra thông tin của họ, cải thiện minh bạch và giảm tải cho bộ phận nhân sự.

6. **Cơ Chế Lựa Chọn Phương Thức Thanh Toán**:
   - Cho phép nhân viên chọn cách nhận lương: chuyển khoản, qua bưu điện, hoặc nhận tại văn phòng.
   - Lý do: Tạo sự linh hoạt và đáp ứng nhu cầu đa dạng của nhân viên về phương thức thanh toán.
## 3. Phân Tích Ca Sử Dụng Payment

### Các Lớp Phân Tích Cho Ca Sử Dụng Payment

Trong ca sử dụng Payment, chúng ta xác định các lớp phân tích chính như sau:

1. **Nhân Viên (Employee)**: Đại diện cho nhân viên, bao gồm thông tin cá nhân và thông tin lương.
   - **Thuộc tính**: `mãNhânViên`, `tên`, `phươngThứcThanhToán`, `lươngTheoGiờ`, `lươngCốĐịnh`, `tỷLệHoaHồng`.
   - **Nhiệm vụ**: Lưu trữ và cung cấp thông tin cần thiết để tính toán lương.

2. **Bảng Lương (Payroll)**: Chịu trách nhiệm tính toán lương cho nhân viên.
   - **Thuộc tính**: `ngàyThanhToán`, `tổngLương`.
   - **Nhiệm vụ**: Tính toán tổng lương dựa trên thông tin từ lớp Nhân Viên.

3. **Phương Thức Thanh Toán (PaymentMethod)**: Đại diện cho các phương thức thanh toán mà nhân viên có thể chọn.
   - **Thuộc tính**: `loạiPhươngThức` (ví dụ: `ChuyểnKhoản`, `BưuĐiện`, `NhậnTạiVănPhòng`).
   - **Nhiệm vụ**: Quản lý các phương thức thanh toán cho nhân viên.

4. **Xử Lý Thanh Toán (PaymentProcessor)**: Thực hiện các bước thanh toán.
   - **Thuộc tính**: `mãGiaoDịch`, `trạngThái`.
   - **Nhiệm vụ**: Thực hiện giao dịch thanh toán và cập nhật trạng thái giao dịch.

### Biểu Đồ Sequence
![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aO9Vnk55UM6PXrVbSHK09JAJCmiIyqeKd1xkMfoNxdDimx65UUaeCX4FTw_rERmt92CnBoCa__12L7q16H0j8HaFTwzCHbB4XR18GTSErNmhXSh3gqgT7-vQNehGeQ79XQ88f0jXXfL2piDTIoj3CWvl0LgMcOUGmQOFbwkWfk2I1Xg5ImgB7qgAW7nKzTZSWX5-LWeLw490VHZASDW8jklmmapY0wu476PEXnVcX-3G3m000F__0m00)
### Biểu Đồ lớp
![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO9Vnk55UM6PXrVbALHpAIWev1vUZ12oKWWkAShCImT9bA3n2pAERJYsC2yz9EFXxfN98Hc9UHaX-OSN0jK4u901wSg1IQNcksS-t3tNIY4blpGf9nL9pldXxeb79ZpStPsNWInRyd3tTf-7kzizyXCz7kwUd9SEbwpbWlh5wU6knNdfFX1Z8Dx9Ip-ye1BPSIw99J3ZfiBLejXpU6rU1bHSGnFJ4bo-WzYNa_zmry9CL3NmK8ER4V5mzrgVmtlHDGF3tZqpCTy5wFVa39ImBmAQ2ZBkyC9CPF4AT7D03YxBpqm1MOKKixgwThXZ1JNKG4eHEh58OhYToo4rBmMKe000003__mC0)

## 4. Phân Tích Ca Sử Dụng Maintain Timecard

### Các Lớp Phân Tích Cho Ca Sử Dụng Maintain Timecard

Trong ca sử dụng Maintain Timecard, chúng ta xác định các lớp phân tích chính như sau:

1. **Nhân Viên (Employee)**: Đại diện cho nhân viên, bao gồm thông tin cá nhân và thông tin về các chấm công.
   - **Thuộc tính**: `mãNhânViên`, `tên`, `danhSáchChấmCông`.
   - **Nhiệm vụ**: Quản lý thông tin chấm công và cung cấp chức năng thêm, sửa, xóa chấm công.

2. **Chấm Công (Timecard)**: Chịu trách nhiệm lưu trữ thông tin chấm công của nhân viên.
   - **Thuộc tính**: `ngày`, `sốGiờ`, `mãChiPhí`.
   - **Nhiệm vụ**: Lưu trữ và xử lý thông tin về giờ làm việc của nhân viên.

3. **Quản Lý Chấm Công (TimecardManager)**: Thực hiện các thao tác quản lý chấm công cho nhân viên.
   - **Thuộc tính**: `danhSáchChấmCông`.
   - **Nhiệm vụ**: Cung cấp các phương thức để thêm, sửa, và xóa chấm công.

4. **Dữ Liệu Chấm Công (TimecardData)**: Tầng truy cập dữ liệu cho các thông tin chấm công.
   - **Thuộc tính**: `cơSởDữLiệu`.
   - **Nhiệm vụ**: Thực hiện các thao tác lưu trữ và truy xuất dữ liệu chấm công từ cơ sở dữ liệu.

### Biểu Đồ Sequence
![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aO9Vnk55UM6PXrVbSHK09JAJCmiIyqeK0aiVxbgSvtDuhtF6mrrBSvqFRybBHr60IzpbuUxrFfaFTxUN8glWGbYZe6k7rNGhXPACmwjoaKGqDBcmAGGPWAhluQw5-QZwq9JZiAy8A4gSVLXzPQMGSsn3AQe1M1NYTaB5uON9Va21jNa-GAFmE00HVk1m0eew7LwOx_rmr_uIi1QWLeVKl1HWl080003__mC0)
### Biểu Đồ lớp
![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO9Vnk55UM6PXrVbALHpAIWev1vUZ12oKWWkAShCImT9bA3nKnBpCe8FBqpESCvuk6jfhlFXBNdfLWe-cSKbDaWYTborN52Ra4GXLkMb7rvGQQNWabYI2k8MFzmzqJtpuUwvLWef-QL9EQbGvpXdP0Pa75uBjnjkO63fmrsBytmExyKmcLYtWRoLSNXLBfAWXgQLGbb-PWhKHMiJSSXL7DwCLGhkEfU7kzVx0BtJNehXlEHZ2uCVxfwFK84ShZd7DfJYiBEagBGo0kZffILe2h26EbBCwkhQ8GS_5zQG8reHLfznEQJcfO2I5G000F__0m00)


