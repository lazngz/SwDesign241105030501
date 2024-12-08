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
![](https://www.planttext.com/api/plantuml/png/b5L1Rjim4Bph5GjVQXTnq5w58WXI5qY050tY03tJujPcIv42IQKrYhwWbzxxWhx1XrxoaRmWNmX5aHGbAmvoq-uETtPdbzJ3xl-fDaIPkkJPAxZxSx_xBJOWrfkxVmJu_Uvl1H_AYiijObPmedKquMS6C0T6SrWQnSJQcOAKs7DGkSfXGGmwgvAQ6IP53w899sfhKLYmad3dCwp4WYYgSxXashoxyVP9PiC0XDBWcGPe3i4ro-5MCkgG1U55pIt_qh5CPoaFm1fDQ6Y1XZ2k6qGi3g2kQ7TOuFTblzYKokQwylqbINvbNhXGdHSEFUr5Ny26BH5i8skbFqlr3MbV87cBgkdyl07qGtQWfjOnQojOLIbx98gMrgtmAnPcD1JL--JfhiYUXBfUbMpyk5LawOePqyEcKfBpmtACxORiQYbHcC7Ya1yBf7NHRbaQ4NOy94drP8DDqc6J4NUJvDzV9e7AOdndGocy-z2U3I2jatep3vA5l4Cfhx6IodX1gzRNt1v_Xppgn8MLmowwRUjrq6PwKGCsVXrpEcNQ7GRumhX1rGRFjYxitfoE_0XGqCwS3GkEZTeeMH6D7uaWQrI-rK8AWNxYx-DtDhpWPziBEktUAyiIdpQtnoIv7uSVbGOQXknrtXjEDzJ0CWqxtX6F2-pLVxb8yMsUl9t0V0wJDyV7hoVTovF3XkYdKE4-vd4BT1PyeqY_RYb-E9_-kKYSG-a0pnr82jT6gcVnNGiUdfrQpPf_soC0003__mC0)
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
![](https://www.planttext.com/api/plantuml/png/b5DBJiCm4Dtx5BFZ8_K2NQ1Mm89TLB53A1hiAHZv4zcJIZqR2ux45N2SZv8q5MNdUPzvut7oy_MzYOo1Qsl45JpGNZi2_Y18A5C4T0eue8kQjNSHzZx0ixOaCIZnSliAgzNT09G5EQNTkn1pP2hRLbNm1rAm1coFFNLzyuTrHvyaELj3FewSuZHWQRfaZVMRrRmKElI_r7acDAtcJDE6kNZL1Hw3DsROT5UNzu6IHman0wOYDB8soEtaigkeezFiIy9nWm9ri-YgBPjgPChalo_qQ2lZZqJ3ZNgWt4hM1n9Y1an5JmvRT0rCmMgNWdeopNQgMuZ8dqwcfsQnIQ_S_0U_0000__y30000)
## Biểu đồ lớp
![](https://www.planttext.com/api/plantuml/png/Z5JDQjmm4BxxAOOzRG8RsgieIsWsq41BInFeULOQ73MoP2GvT2bziXpoI7c5o5h9Apd9fZVDp3S_tpTZFpqydZkFrW-TQhX2v-2owvNP4S7V1c05KZ2uzbRgDfeQEweSmcmPRD1Jj7hZf9T6Ln272kqke8ZB3bNqUTaHHoiSWw_I-KytoLw7A00AaHtBZ6IGNISCxeqK4SbHyK65zjUnoVAaR0FGaizyDkHHAZSYqcp_caGv5qwKAMLSrTH5w59GlJM3TR-ClIDHKpFtPCUXluo0EXIazeChgWQgVMz3naIt96VfDt7_8ZJD_GDtrYXrVEpNrCyZXW8TQJzR3VxPa1ZuVezbH9CF6RN2qmA-rpNdcvXmDqNvb-lIP0Cc4NkJyK_gZVM9Tx_tZMUKZYcXrZ5i8tPJBk_GQ5-e4hsD9CVy8nSJ2k4M7Nr3ZItPD0atMbFIxM9wpm_ny-vAB0-VLQYU8n7fiBY6uyS_GhDKIGMM9IgacxxenSS5h5PhM7muEpjT7CwUmIswPZ9JE293nfJEO4lAwDQ1DwyN3Szya_kQsPfrhjV8G6gk1a4YF9gvjBFKOfek8jnx6GND_ymuSCW9pJbfCVuZdm400F__0m00)
## Biểu đồ thuộc tính
![](https://www.planttext.com/api/plantuml/png/Z9FFIiGm4CRlVOhGex07hqMMnJ-W8AkmWkTfCxh1_2d9PA68J-R1H_8LJ7VJxBQfOc_vPZBzVL-dtvzVAqTWoIjPD1ASOpUgbQP3PEy52y-2OHJkUCKsP8L-ZGKD2YSI1yA7bqjXQLknwt28Ed1kqRb9Txir6jTUrMWd5LGWv4JR2elzoD7WrZX1mkX9R_14Vlew1n9i5wuRNqiiFehe-4aeRC3ov9YYa3d-DOfzXXaSQfvfP0ZahV7MFHlxXZpX_0NkQoM8y7HQed-4pXef4tnxEF-VFLx8I6jmk1b75Wj6zuWZpUpGzh45cabbRpYNPuq658MQvcnU6TM2xfBDvd3Et4HzdU-cD0tChCgGIs2v5uukXlrVZkCPoZ7kPK-MVfNol6IB1IlFokCoLKo1XbTqist3LwkOnGR5BhGD3a-wqiqgOivs7MS9vtoOj0gBr__GFm000F__0m00)
## Biểu đồ phụ thuộc, quan hệ kết hợp
![](https://www.planttext.com/api/plantuml/png/Z5JBIiD05DtdAuPi124Bjq5AiGeAKeKAhc-IQpDq7d4UXI2k_GQN8lw4NNJXb_GB_0KdxIHj7efPX9bppxrppisTVA_MOsr06SjPa3BGcbpmWiaIaJm5n3qHGGzSPJ6P6KN5t0S4SEn06HYyUJYZokGnENSRZqEMATIwmovoAN1gUOAg4q4Eb7Mmd2giIhOA5r9JGwNeS9qdOxl7QM2WIfSkRS8mU0wyuplACGMLDOwD1tgEVst5jeSzSIYo7cQa0NOfhTBtKYqmQ-Jy9Tmcd1g3XzKQzRTGAibO8xxOxV-ltIVqb2QWSTPkcGz8KKbiONA9gcgRKzE9R0ttuK6ZJWf7OOPiJYGlG9IDpNItxxdn-BG_cqocC30gTL-SbckgpMaz_wDsU-gmR_UeKdP49bzlANcq84Y-MRsGnUPpRQhbUn47pKKAJq8IHIGy3lUZ5XCE0kQe1sdrDus9mXJfqj5g_mUi9ZFs9WPP-rfKQ-igzMKNxlr1J6utgzSq3kgCA1eTdf5XuGPQ4oc2niRlbB5RL3-L7m000F__0m00)


