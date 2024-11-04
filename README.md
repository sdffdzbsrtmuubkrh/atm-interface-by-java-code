import java.util.Scanner;

// ATM Interface
interface ATM {
    void checkBalance();
    void deposit(double amount);
    void withdraw(double amount);
}

// ATM Implementation Class
class ATMImplementation implements ATM {
    private double balance;

    public ATMImplementation() {
        this.balance = 0.0; // Initial balance
    }

    @Override
    public void checkBalance() {
        System.out.printf("Current balance: $%.2f%n", balance);
    }

    @Override
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.printf("Deposited: $%.2f%n", amount);
        } else {
            System.out.println("Deposit amount must be positive.");
        }
    }

    @Override
    public void withdraw(double amount) {
        if (amount <= 0) {
            System.out.println("Withdrawal amount must be positive.");
        } else if (amount > balance) {
            System.out.printf("Insufficient funds. Your balance is: $%.2f%n", balance);
        } else {
            balance -= amount;
            System.out.printf("Withdrew: $%.2f%n", amount);
        }
    }
}

// Main Class
public class ATMInterfaceDemo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ATM atm = new ATMImplementation();

        int choice;
        do {
            System.out.println("\nATM Menu:");
            System.out.println("1. Check Balance");
            System.out.println("2. Deposit Money");
            System.out.println("3. Withdraw Money");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    atm.checkBalance();
                    break;
                case 2:
                    System.out.print("Enter amount to deposit: ");
                    double depositAmount = scanner.nextDouble();
                    atm.deposit(depositAmount);
                    break;
                case 3:
                    System.out.print("Enter amount to withdraw: ");
                    double withdrawAmount = scanner.nextDouble();
                    atm.withdraw(withdrawAmount);
                    break;
                case 4:
                    System.out.println("Thank you for using the ATM!");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 4);

        scanner.close();
    }
}
