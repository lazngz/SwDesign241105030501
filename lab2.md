
## Phân tích các ca sử dụng trong hệ thống Payroll System
1. **Maintain Timecard (Quản lý Thẻ Chấm Công)**: 
   - Nhân viên có thể tạo, sửa, hoặc xóa thông tin thẻ chấm công để ghi lại giờ làm việc.
   - Hệ thống xác minh dữ liệu nhập, kiểm tra trùng lặp và cập nhật thông tin trong cơ sở dữ liệu.

2. **Generate Paycheck (Tạo Phiếu Lương)**:
   - Tầng xử lý nghiệp vụ chính, bao gồm tính lương và quản lý logic liên quan.
   - Thao tác này bao gồm tính các khoản khấu trừ, thuế, và lợi ích.
3. **View Paycheck (Xem Phiếu Lương)**:
   - Nhân viên có thể xem phiếu lương chi tiết của mình trong hệ thống.
   - Hệ thống cung cấp chi tiết về các khoản lương, khấu trừ, và tổng số thanh toán.

4. **Access Employee Reports (Truy Cập Báo Cáo Nhân Viên)**:
   - Quản lý có thể xem các báo cáo chi tiết theo từng nhân viên.
   - Bao gồm báo cáo về giờ làm việc, doanh số, và phiếu lương.
5. **Integration with Project Management DB2 (Tích Hợp với Cơ Sở Dữ Liệu Quản Lý Dự Án)**:
   - Hệ thống tự động kết nối với cơ sở dữ liệu DB2 để lấy thông tin dự án và giờ làm việc.
   - Quản lý thời gian và tài nguyên được phối hợp từ dữ liệu này để đảm bảo tính chính xác.

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
