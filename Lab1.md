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

1. **NhanVien (Employee)**: Đại diện cho nhân viên, bao gồm thông tin cá nhân và thông tin lương.
   - **Thuộc tính**: `maNhanVien`, `ten`, `phuongThucThanhToan`, `luongTheoGio`, `luongCoDinh`, `tyLeHoaHong`.
   - **Nhiệm vụ**: Lưu trữ và cung cấp thông tin cần thiết để tính toán lương.

2. **BangLuong (Payroll)**: Chịu trách nhiệm tính toán lương cho nhân viên.
   - **Thuộc tính**: `ngayThanhToan`, `tongLuong`.
   - **Nhiệm vụ**: Tính toán tổng lương dựa trên thông tin từ lớp NhanVien.

3. **PhuongThucThanhToan (PaymentMethod)**: Đại diện cho các phương thức thanh toán mà nhân viên có thể chọn.
   - **Thuộc tính**: `loaiPhuongThuc` (ví dụ: `ChuyenKhoan`, `BuuDien`, `NhanTaiVanPhong`).
   - **Nhiệm vụ**: Quản lý các phương thức thanh toán cho nhân viên.

4. **XuLyThanhToan (PaymentProcessor)**: Thực hiện các bước thanh toán.
   - **Thuộc tính**: `maGiaoDich`, `trangThai`.
   - **Nhiệm vụ**: Thực hiện giao dịch thanh toán và cập nhật trạng thái giao dịch.


### Biểu Đồ Sequence
![](https://www.planttext.com/api/plantuml/png/V55DIiD05DxFARuBU84ifBGkYnGQf5qEqo4paBx4T4ReihWKGH0F44H48U0wit0HwJtU2Ro22P9AjBZztlVB-mpleusJXVFhL3ZhKesnvN3jyN77uHvpVUarAOs9n9n3XJCEJvHW9hThJKu8gLnMuDn8kh2QHDvQMMLpIGuBFzt6xS74cHnUnfAIgSye6Q0pqq6nyUf79Nfdd9mE3ICicrSFnVMpX-jGkAmfIGnOdUoG5Y5kgfu7n-6XNPBkt_Pbs-J0Ef8K5rm_ueh3xhVgJzYH4H4cXiCj8JVVghOkXnVrV-j-U8H5KogGuReY95PcM76uKKQ8aQPLzxSl0000__y30000)
### Biểu Đồ lớp
![](https://www.planttext.com/api/plantuml/png/R5AnRSCm4EmvnI_W1Lm4XYt4BfJ0W8N0xKCcH2BIqv1UXH2ayW81KgPEcGbOfCaYd20hX894MRB2ylxk_kx1N_kzgXXBhejSLC-Qe3IL5Amvbx3Mpbvg-7bpzXrYPp_Ei44uEFi5aREVbC4Ucq8I2v7cM5Nmg92Uj2Hu4T2-0WEoX0ENch8EvrlWh6f3MQBgDF42bHZqXDxyGR8ofuwNTpHfjjeiuJutoAF1naIQr0Jd9fOxWpi_3VXhIBj6ok9M5-9IXireVuGiUnVJCsSU-tdmuEQ9-ZeU-WxIOnqtCr61Mus-HgfkBbPYwuDwx3ESUx6ukxQPmly45DFDBIj8X5X9Elc_y0S00F__0m00)

# 4. Phân Tích Ca Sử Dụng Maintain Timecard

### Các Lớp Phân Tích Cho Ca Sử Dụng Maintain Timecard

Trong ca sử dụng Maintain Timecard, chúng ta xác định các lớp phân tích chính như sau:

1. **NhanVien (Employee)**: Đại diện cho nhân viên, bao gồm thông tin cá nhân và thông tin về các chấm công.
   - **Thuộc tính**: `maNhanVien`, `ten`, `danhSachChamCong`.
   - **Nhiệm vụ**: Quản lý thông tin chấm công và cung cấp chức năng thêm, sửa, xóa chấm công.

2. **ChamCong (Timecard)**: Chịu trách nhiệm lưu trữ thông tin chấm công của nhân viên.
   - **Thuộc tính**: `ngay`, `soGio`, `maChiPhi`.
   - **Nhiệm vụ**: Lưu trữ và xử lý thông tin về giờ làm việc của nhân viên.

3. **QuanLyChamCong (TimecardManager)**: Thực hiện các thao tác quản lý chấm công cho nhân viên.
   - **Thuộc tính**: `danhSachChamCong`.
   - **Nhiệm vụ**: Cung cấp các phương thức để thêm, sửa, và xóa chấm công.

4. **DuLieuChamCong (TimecardData)**: Tầng truy cập dữ liệu cho các thông tin chấm công.
   - **Thuộc tính**: `coSoDuLieu`.
   - **Nhiệm vụ**: Thực hiện các thao tác lưu trữ và truy xuất dữ liệu chấm công từ cơ sở dữ liệu.
### Biểu Đồ Sequence
![](https://www.planttext.com/api/plantuml/png/T94nJWCn44Lxds8km0LIe8XDkI2XH8XsSAnufFLiMCO5TIuGYPA656cG8b5GnGM54VVm2RW2taX1E5eAovBd_J__oz_XO_mWs8btZHAIni05fR3oyBbEuGccvjuRrWOgX6aAEvYaiEK5N2Anv0CpSaPZDrSAjRGTN5da6pAibjcKD2sH1QuzSlrOMNHLoujYDF4r6Jyu-drKHrCuEp_n6i7CnbS7sgRzDb_nFVCbqel-u6c_QGiSN0hFD20geusW_dhpvQAI64ft6pSQE6js34sl5njVsFuRzDZqqAiFTnTpN3bqBAHgR7ZUVzeF0000__y30000)
### Biểu Đồ lớp
![](https://www.planttext.com/api/plantuml/png/X991IiL038RtSueiBVWkKEJni4KtLPIAk0tjq0csCzB9W4LSUG71fMkNdc0MRhn8J-0LV5AdprQn0rdaJqY-9FFXtpQMiMNNrC9UauRMM2cOk9PmIBr_SF3-sFido7h_V0C9GjxxLqXx_w8hE47Il3Mue4OMs9P253LQ2wSAzIL93NS2lbw3GOaXvvPqDUWy5qhKAiT29GgRnEWgXemi7mHtBUv3Yo255hh2BeOKMGw-DSTaOZYg3NA0I1ITAHexZhNE7UgicrTSP1b6KB89qbunfWOf-gPnk9nqQtP9lpUs_sF4QCUUkeoacxCN9ZT3PBhVshbb3cvTT-MG_u69_ZhCUFNLQZtM5BFbJc8p-4bCRAGkj__o4m00__y30000)
## 5. Hợp Nhất Kết Quả Phân Tích

## 1. Tóm Tắt

Trong hệ thống Payroll System, chúng ta đã phân tích hai ca sử dụng chính: **Payment** và **Maintain Timecard**. Mỗi ca sử dụng này có các lớp phân tích riêng, nhưng cũng có sự liên kết chặt chẽ giữa chúng để đảm bảo tính đồng bộ trong việc quản lý thông tin nhân viên và quy trình thanh toán.

## 2. Các Ca Sử Dụng

### 2.1 Ca Sử Dụng Payment

- **Mục tiêu**: Tính toán và xử lý thanh toán cho nhân viên dựa trên thông tin lương và phương thức thanh toán đã chọn.
- **Các lớp phân tích**:
  1. **NhanVien (Employee)**
     - **Thuộc tính**: `maNhanVien`, `ten`, `phuongThucThanhToan`, `luongTheoGio`, `luongCoDinh`, `tyLeHoaHong`.
     - **Nhiệm vụ**: Cung cấp thông tin cần thiết để tính toán lương.
  
  2. **BangLuong (Payroll)**
     - **Thuộc tính**: `ngayThanhToan`, `tongLuong`.
     - **Nhiệm vụ**: Tính toán tổng lương dựa trên thông tin từ lớp Nhân Viên.
  
  3. **PhuongThucThanhToan (PaymentMethod)**
     - **Thuộc tính**: `loaiPhuongThuc`.
     - **Nhiệm vụ**: Quản lý các phương thức thanh toán cho nhân viên.
  
  4. **XuLyThanhToan (PaymentProcessor)**
     - **Thuộc tính**: `maGiaoDich`, `trangThai`.
     - **Nhiệm vụ**: Thực hiện giao dịch thanh toán và cập nhật trạng thái giao dịch.

### 2.2 Ca Sử Dụng Maintain Timecard

- **Mục tiêu**: Quản lý thông tin chấm công của nhân viên, bao gồm việc thêm, sửa và xóa chấm công.
- **Các lớp phân tích**:
  1. **NhanVien (Employee)**
     - **Thuộc tính**: `maNhanVien`, `ten`, `danhSachChamCong`.
     - **Nhiệm vụ**: Quản lý thông tin chấm công và cung cấp chức năng thêm, sửa, xóa chấm công.
  
  2. **ChamCong (Timecard)**
     - **Thuộc tính**: `ngay`, `soGio`, `maChiPhi`.
     - **Nhiệm vụ**: Lưu trữ và xử lý thông tin về giờ làm việc của nhân viên.
  
  3. **QuanLyChamCong (TimecardManager)**
     - **Thuộc tính**: `danhSachChamCong`.
     - **Nhiệm vụ**: Cung cấp các phương thức để thêm, sửa, và xóa chấm công.
  
  4. **DuLieuChamCong (TimecardData)**
     - **Thuộc tính**: `coSoDuLieu`.
     - **Nhiệm vụ**: Thực hiện các thao tác lưu trữ và truy xuất dữ liệu chấm công từ cơ sở dữ liệu.

## 3. Mối Quan Hệ Giữa Các Ca Sử Dụng

Hai ca sử dụng này liên kết với nhau qua lớp **NhanVien (Employee)**. Trong ca sử dụng Payment, thông tin về lương của nhân viên được tính toán dựa trên các chấm công mà lớp **ChamCong (Timecard)** lưu trữ. Do đó, việc quản lý thông tin chấm công thông qua ca sử dụng Maintain Timecard sẽ ảnh hưởng trực tiếp đến quá trình thanh toán trong ca sử dụng Payment.

### 3.1 Sơ Đồ Tương Tác Giữa Các Lớp

![](https://www.planttext.com/api/plantuml/png/V97DIiGm58NtUOhBxFi68eCTS1DbP8AulMH26wQz7PfaKTHt45owwiAbw3uB5qhV8q_WAzWAanhyMGIIxnxkEOTy-DUbiTXQLrVCx3H1snZ5hBQLWitGm_jTyFSWXfUXfmB4Mo_XL0V_Z91FTnxymvwnFSeT5WeMES8c-2TO1VyuwjVOrOhi0guPWApG63WlaIwreWXEa0hk6YeYMPVJKvHEYb5SYWPdzPNZtKnl_xO-GqrsF21qhIIsstz3v2NM-VSC5mw9Tp_mod6jNCIZ_s4L7DrasRmuje8iEvxnBzLIGT8l7HrSKve6_Ph5U6dQTCQMYhRJhxDF0000__y30000)
