 # finance_management_system
it helps us to make a track of our expenses 
// Main.java

import java.time.LocalDate;
import java.time.format.DateTimeParseException;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        ExpenseTracker tracker = new ExpenseTracker();
        Scanner scanner = new Scanner(System.in);

        int choice;
        do {
            System.out.println("\n--- Daily Expense Tracker ---");
            System.out.println("1. Add a new expense");
            System.out.println("2. View all expenses");
            System.out.println("3. View expenses by category");
            System.out.println("4. Get total expenses");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            try {
                choice = scanner.nextInt();
                scanner.nextLine(); // Consume newline

                switch (choice) {
                    case 1:
                        addExpense(tracker, scanner);
                        break;
                    case 2:
                        tracker.viewAllExpenses();
                        break;
                    case 3:
                        viewByCategory(tracker, scanner);
                        break;
                    case 4:
                        System.out.printf("Total Expenses: $%.2f%n", tracker.getTotalExpenses());
                        break;
                    case 5:
                        tracker.saveOnExit();
                        System.out.println("Exiting the application. Goodbye!");
                        break;
                    default:
                        System.out.println("Invalid choice. Please enter a number between 1 and 5.");
                }
            } catch (DateTimeParseException e) {
                System.out.println("Invalid date format. Please use YYYY-MM-DD.");
                choice = 0; // Keep the loop running
            } catch (Exception e) {
                System.out.println("Invalid input. Please try again.");
                scanner.nextLine(); // Clear the invalid input
                choice = 0; // Keep the loop running
            }

        } while (choice != 5);

        scanner.close();
    }

    private static void addExpense(ExpenseTracker tracker, Scanner scanner) {
        System.out.print("Enter date (YYYY-MM-DD): ");
        LocalDate date = LocalDate.parse(scanner.nextLine());

        System.out.print("Enter description: ");
        String description = scanner.nextLine();

        System.out.print("Enter amount: ");
        double amount = scanner.nextDouble();
        scanner.nextLine(); // Consume newline

        System.out.print("Enter category: ");
        String category = scanner.nextLine();

        tracker.addExpense(description, amount, date, category);
    }

    private static void viewByCategory(ExpenseTracker tracker, Scanner scanner) {
        System.out.print("Enter category to view: ");
        String category = scanner.nextLine();
        tracker.viewExpensesByCategory(category);
    
}
