# Lab 3: Identify Design Elements

## Xác định các phần tử thiết kế của hệ thống “Payroll System”

Hệ thống "Payroll System" có cấu trúc phân tầng rõ ràng với các thành phần tương tác với nhau để cung cấp các chức năng quản lý thẻ chấm công, tính lương, và báo cáo cho nhân viên. Để mô tả các phần tử thiết kế của hệ thống này, chúng ta cần thực hiện các bước sau:

### Subsystem Context Diagrams
#### Hệ thống con và biểu đồ ngữ cảnh

Hệ thống Payroll System được chia thành các hệ thống con sau:

- **Timecard Management System** (Quản lý Thẻ Chấm Công): Quản lý thông tin về giờ làm việc của nhân viên.
- **Paycheck Generation System** (Tạo Phiếu Lương): Tính toán và tạo phiếu lương cho nhân viên.
- **Employee Report System** (Báo Cáo Nhân Viên): Cung cấp báo cáo về công việc và lương của nhân viên.
- **Bank System** (Hệ thống Ngân Hàng): Xử lý thanh toán lương qua ngân hàng.
- **Project Management Database** (Cơ sở dữ liệu Quản lý Dự án): Lưu trữ thông tin dự án và giờ làm việc của nhân viên.

#### Biểu đồ ngữ cảnh hệ thống con "Bank System"

Biểu đồ ngữ cảnh của hệ thống con "Bank System" có thể được vẽ như sau:
![](https://www.planttext.com/api/plantuml/png/d5912i8m4Bpt5SMJ7lo01ocqe63fnI1wN6980dLJsYnKn9Tvy4b-mQYeDQOUp64FkpEpEqCkftFIMAWjxSg8bz0qyM0kc38eSt9b41-Y-FOawOsW58WfGCKCu73qcA1hi1fGkedkJe_HKt5D-NwcmMIQgvTYwvh_YALcQJBAjQ120iwXSsJRsVDKv50L2kpT4jF8G2-KB-a0kD82NqASKAPGXKbUGEFnr7Su2SVbeUx4a9l9LpP1M72n3OKNMlnfee_uJkR7jVrf9GAtjvzr1G00__y30000)


**Mô tả hệ thống con:**

- **Bank System** (Hệ thống Ngân Hàng): Hệ thống này chịu trách nhiệm xử lý thanh toán tiền lương cho nhân viên thông qua chuyển khoản vào tài khoản ngân hàng của họ.
**Payroll System** sẽ gửi yêu cầu thanh toán vào 
**Bank System**,**Bank System** sẽ thực hiện các giao dịch thanh toán, cập nhật trạng thái thanh toán và trả kết quả về cho **Payroll System**.

- **Interface của hệ thống con**: **Bank System** nhận thông tin thanh toán từ **Payroll System** và phản hồi lại kết quả giao dịch.


### Analysis Class to Design Element Map
#### Ánh xạ các lớp phân tích đến các phần tử thiết kế

Các lớp phân tích trong hệ thống Payroll System có thể được ánh xạ vào các phần tử thiết kế như sau:

| Lớp phân tích   | Phần tử thiết kế tương ứng |
|-----------------|---------------------------|
| Timecard        | TimecardService (Service Layer) |
| Paycheck        | PaycheckService (Service Layer) |
| EmployeeReport  | EmployeeReportService (Service Layer) |
| BankTransaction | BankPaymentService (Integration Layer) |

- **Service Layer**: Lớp dịch vụ này chứa các logic xử lý nghiệp vụ chính cho từng chức năng của hệ thống như quản lý thẻ chấm công, tính phiếu lương, và tạo báo cáo.
- **Integration Layer**: Lớp này xử lý các giao tiếp giữa hệ thống Payroll và các hệ thống bên ngoài như ngân hàng.

### Design Element to Owning Package Map
#### Ánh xạ các phần tử thiết kế vào các gói

Các phần tử thiết kế của hệ thống Payroll System sẽ được nhóm vào các gói (packages) như sau:

| Phần tử thiết kế       | Gói chứa                   |
|-----------------------|----------------------------|
| TimecardService       | com.payroll.timecard       |
| PaycheckService       | com.payroll.paycheck       |
| EmployeeReportService | com.payroll.report         |
| BankPaymentService    | com.payroll.integration    |

Mỗi gói sẽ chịu trách nhiệm quản lý các chức năng của từng phần tử thiết kế tương ứng, đồng thời giao tiếp với các gói khác khi cần thiết.

### Architectural Layers and Their Dependencies
#### Mô tả các lớp trong kiến trúc hệ thống và các mối quan hệ giữa chúng

Hệ thống Payroll System sử dụng kiến trúc phân tầng với các lớp chính như sau:

1. **Presentation Layer** (Lớp Giao Diện): Chịu trách nhiệm tương tác với người dùng (quản lý, nhân viên). Lớp này bao gồm các form nhập liệu, báo cáo và thông tin hiển thị.
2. **Service Layer** (Lớp Dịch Vụ): Chứa các logic xử lý nghiệp vụ chính, bao gồm các lớp như TimecardService, PaycheckService, và EmployeeReportService.
3. **Data Access Layer** (Lớp Truy Cập Dữ Liệu): Xử lý các truy vấn và thao tác với cơ sở dữ liệu, bao gồm các lớp DAO (Data Access Object).
4. **Integration Layer** (Lớp Tích Hợp): Chịu trách nhiệm giao tiếp với các hệ thống bên ngoài như hệ thống ngân hàng và cơ sở dữ liệu quản lý dự án.

#### Biểu đồ các lớp và các mối quan hệ giữa chúng:
![](https://www.planttext.com/api/plantuml/png/X991IWD154JtVOfFzia1N4Xm0d4X8M08ICYYx0pTZTF_3t6-4iJBv1ekN7WWh-2VmOr9gxteHLNremhwy-rz-jXXtsbkN0l_W53Jo4kUj3ZifMacNKGE2HxP2uSHlJYoivab7zUwCdEUK25NPcxTgoj3sfXgRRG0W2nxxqR_V7yFyH2EuATKymdZ2b915cQkpVmTqbawIdi-WUDAm8lmSUHhVDSe3wJnJfvvV5ckJnTa0WqA3P8hvqufvnKCDTT4TmQge3Gag8-uykX_YzqgpPI3aQI_4_-eEQrvr_-0Bm000F__0m00)
