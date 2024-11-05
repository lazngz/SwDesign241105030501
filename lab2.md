
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
