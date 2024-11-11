
## Phân tích các ca sử dụng trong hệ thống Payroll System
1. **Maintain Timecard (Quản lý Thẻ Chấm Công)**: 
   - Nhân viên có thể tạo, sửa, hoặc xóa thông tin thẻ chấm công để ghi lại giờ làm việc.
   - Hệ thống xác minh dữ liệu nhập, kiểm tra trùng lặp và cập nhật thông tin trong cơ sở dữ liệu.
     ![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO9VHc9UM6Pgda8rbm88v2R2HAmKWakAClFI8U8b60A9-I4PgSuPYRdE-Ndf6ddfYPLM2Yw99Qaw2kcP-LOAcNabcbOAI4guQhcWTY898gm52g9QW30HmY_ETuUQ2-5dPwRcXXGb8Zi2QA5JVdvEQc8UH4boOW7GDoNEmIu-8Bco_CmKa2lWVbOoL5BGrLLGCj3Jqr92SPQLGc7fmrsBy-9p3k_bSaZDIm6560000F__0m00)
   \
2. **Generate Paycheck (Tạo Phiếu Lương)**:
   - Tầng xử lý nghiệp vụ chính, bao gồm tính lương và quản lý logic liên quan.
   - Thao tác này bao gồm tính các khoản khấu trừ, thuế, và lợi ích.
     ![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO97QaX6VbwwJocGKAZcKW21aiJyW8pCr5Ame4PUHc9UM6PgdfM27vIbQQM0aEUgvO8Q1PE66PERw0VN6bnIb0bK2p4UNI2tD1bib9L2Mav-OWd2H8Gj23CHOgY6v824tFEJOOQ01RCpyXFpl3CIIqEAIb4amAf3CagJGKv4aId9pCk0wj3Gn93nGTQ7a0Uw62KWbGoL57Hr5PGCzFIqb92zOQLGyd3NmdmkU5ZXKPcNyN3NsZmkXzIy551y0G000F__0m00)
3. **View Paycheck (Xem Phiếu Lương)**:
   - Nhân viên có thể xem phiếu lương chi tiết của mình trong hệ thống.
   - Hệ thống cung cấp chi tiết về các khoản lương, khấu trừ, và tổng số thanh toán.
     ![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO9VHc9UM6Pgda8rbm88v2R2HAmKWakAClFI8U8bw08LgRa16PcffJwb-Ndf6ffM2WWULoqNr7I46C9yX1YgWJaW8VVyP2k5j9pyn1A8O7P6VcAUTqPYQKXHAOe4M7L8HcaooBceCecLpXcP8Pcf9N2dGQq1EWlkNIL39GLTNGKb0pqzBILaTrg1VCRba9gN0Wea00000F__0m00)

4. **Access Employee Reports (Truy Cập Báo Cáo Nhân Viên)**:
   - Quản lý có thể xem các báo cáo chi tiết theo từng nhân viên.
   - Bao gồm báo cáo về giờ làm việc, doanh số, và phiếu lương.
     ![](https://www.planttext.com/api/plantuml/png/T56nRi8m4Dtz5QTCj188Lay8rWYr0h6Yg-F6bf8xbDYLKDMlw7TqwbQ63lqIlg2_G8ATH23XwUxTUtVlpl_7ttdji7A-B8GgiAxXsIEb1tWNqBuIGovXxIfBUK2TfXkWyeSbxXV8I-ILGTfQJIEAWOGEUf0GEE93n7bTQPYuwcNtPlRYq6oGXlnQc5jEiMmQAWcMN00pHZ8RuoMy5emHLCPkh7QfPyebF1ch_IME1f13-r6pnHlRhBKHhvNC4XYF8PbE9ez9vqfUph9Jfv-llUZNl4DLVzyY9jUCmKR3Ua7UvQVZPodcchBsqyu0003__mC0)
5. **Integration with Project Management DB2 (Tích Hợp với Cơ Sở Dữ Liệu Quản Lý Dự Án)**:
   - Hệ thống tự động kết nối với cơ sở dữ liệu DB2 để lấy thông tin dự án và giờ làm việc.
   - Quản lý thời gian và tài nguyên được phối hợp từ dữ liệu này để đảm bảo tính chính xác.
     ![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO97QaX6VbwwJocGKAZcKW21aipa38_y0XSd8mrDAuMo_CmKhbekg7hdO1UVmDB4F9zAbrB7FA0IcARSH920bK9mIL5cNZfCp2yZCIyiCnLDF3qptoSn5oYURAMGcLS24Sn9h0Gx9IGp3sGIo6ge7g3bACvKCbHIqDK5KvZEiL8eERmsEIC-u-7knGLS3gbvAI3F0W000F__0m00)

## code Java mô phỏng ca sử dụng Maintain Timecard.
```java
import java.util.ArrayList;
import java.util.List;
import java.time.LocalDate;

class Timecard {
    private int employeeId;
    private LocalDate date;
    private double hoursWorked;
    
    public Timecard(int employeeId, LocalDate date, double hoursWorked) {
        this.employeeId = employeeId;
        this.date = date;
        this.hoursWorked = hoursWorked;
    }
    
    public int getEmployeeId() { return employeeId; }
    public LocalDate getDate() { return date; }
    public double getHoursWorked() { return hoursWorked; }

    public void setDate(LocalDate date) { this.date = date; }
    public void setHoursWorked(double hoursWorked) { this.hoursWorked = hoursWorked; }

    @Override
    public String toString() {
        return "Timecard{" + "employeeId=" + employeeId + ", date=" + date + ", hoursWorked=" + hoursWorked + '}';
    }
}

class PayrollSystem {
    private List<Timecard> timecards = new ArrayList<>();
    
    // Add a new timecard
    public void addTimecard(Timecard timecard) {
        timecards.add(timecard);
        System.out.println("Added: " + timecard);
    }
    
    // Update an existing timecard
    public void updateTimecard(int employeeId, LocalDate date, double newHoursWorked) {
        for (Timecard timecard : timecards) {
            if (timecard.getEmployeeId() == employeeId && timecard.getDate().equals(date)) {
                timecard.setHoursWorked(newHoursWorked);
                System.out.println("Updated: " + timecard);
                return;
            }
        }
        System.out.println("Timecard not found for employeeId: " + employeeId + " on date: " + date);
    }
    
    // Delete a timecard
    public void deleteTimecard(int employeeId, LocalDate date) {
        timecards.removeIf(tc -> tc.getEmployeeId() == employeeId && tc.getDate().equals(date));
        System.out.println("Deleted timecard for employeeId: " + employeeId + " on date: " + date);
    }
    
    // Display all timecards
    public void displayTimecards() {
        for (Timecard timecard : timecards) {
            System.out.println(timecard);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        PayrollSystem payrollSystem = new PayrollSystem();
        
        // Adding timecards
        payrollSystem.addTimecard(new Timecard(1, LocalDate.of(2024, 11, 5), 8.0));
        payrollSystem.addTimecard(new Timecard(1, LocalDate.of(2024, 11, 6), 7.5));
        
        // Updating a timecard
        payrollSystem.updateTimecard(1, LocalDate.of(2024, 11, 5), 9.0);
        
        // Deleting a timecard
        payrollSystem.deleteTimecard(1, LocalDate.of(2024, 11, 6));
        
        // Displaying all timecards
        payrollSystem.displayTimecards();
    }
}

}
