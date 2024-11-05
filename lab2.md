```java
import java.time.LocalDate;
import java.util.ArrayList;
import java.util.List;

class Timecard {
    private LocalDate date;
    private double hoursWorked;

    public Timecard(LocalDate date, double hoursWorked) {
        this.date = date;
        this.hoursWorked = hoursWorked;
    }

    public LocalDate getDate() {
        return date;
    }

    public double getHoursWorked() {
        return hoursWorked;
    }

    public double calculatePay(double hourlyRate) {
        double regularHours = Math.min(hoursWorked, 8);
        double overtimeHours = Math.max(0, hoursWorked - 8);
        return (regularHours * hourlyRate) + (overtimeHours * hourlyRate * 1.5);
    }

    @Override
    public String toString() {
        return "Date: " + date + ", Hours Worked: " + hoursWorked;
    }
}

class Employee {
    private String employeeId;
    private List<Timecard> timecards;

    public Employee(String employeeId) {
        this.employeeId = employeeId;
        this.timecards = new ArrayList<>();
    }

    public void addTimecard(LocalDate date, double hoursWorked) {
        Timecard timecard = new Timecard(date, hoursWorked);
        timecards.add(timecard);
    }

    public void updateTimecard(LocalDate date, double hoursWorked) {
        for (Timecard timecard : timecards) {
            if (timecard.getDate().equals(date)) {
                timecards.remove(timecard);
                timecards.add(new Timecard(date, hoursWorked));
                System.out.println("Timecard updated: " + timecard);
                return;
            }
        }
        System.out.println("Timecard not found for date: " + date);
    }

    public void displayTimecards() {
        System.out.println("Timecards for Employee ID: " + employeeId);
        for (Timecard timecard : timecards) {
            System.out.println(timecard);
        }
    }
}

public class PayrollSystem {
    public static void main(String[] args) {
        Employee employee = new Employee("E001");

        // Nhập timecard mới
        employee.addTimecard(LocalDate.of(2024, 11, 1), 8);
        employee.addTimecard(LocalDate.of(2024, 11, 2), 10);

        // Hiển thị các timecard
        employee.displayTimecards();

        // Cập nhật timecard cho một ngày cụ thể
        employee.updateTimecard(LocalDate.of(2024, 11, 1), 9);

        // Hiển thị các timecard sau khi cập nhật
        employee.displayTimecards();
    }
}

}
