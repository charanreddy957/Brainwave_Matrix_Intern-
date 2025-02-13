import java.util.*;

class ATM {
    private double balance;
    private String userPin;

    public ATM(String pin, double initialBalance) {
        this.userPin = pin;
        this.balance = initialBalance;
    }

    public boolean authenticate(String pin) {
        return Objects.equals(pin, this.userPin);
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposit successful. Your new balance is: $" + balance);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawal successful. Your new balance is: $" + balance);
        } else {
            System.out.println("Insufficient funds or invalid amount.");
        }
    }
}

public class ATM1 {
    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        ATM atm = new ATM("1234", 1000.0); 

        System.out.print("Enter your PIN: ");
        String enteredPin = scanner.nextLine();

        if (!atm.authenticate(enteredPin)) {
            System.out.println("Invalid PIN");
            return;
        }

        while (true) {
            System.out.println("\nWelcome to the ATM ");
            System.out.println("1. Check Balance");
            System.out.println("2. Deposit");
            System.out.println("3. Withdraw");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");

            int choice = scanner.nextInt();
            switch (choice) {
                case 1:
                    System.out.println("Your current balance is: $" + atm.getBalance());
                    break;
                case 2:
                    System.out.print("Enter deposit amount: ");
                    double depositAmount = scanner.nextDouble();
                    atm.deposit(depositAmount);
                    break;
                case 3:
                    System.out.print("Enter withdrawal amount: ");
                    double withdrawalAmount = scanner.nextDouble();
                    atm.withdraw(withdrawalAmount);
                    break;
                case 4:
                    System.out.println("Thank you for using the ATM. Goodbye!");
                    return;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }
}
