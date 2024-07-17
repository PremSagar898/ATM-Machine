# ATM-Machine

import java.util.ArrayList;
import java.util.Scanner;
class ATM 
{
    private int pin;
    private double balance;
    private ArrayList<String> transactions;
    public ATM(int pin,double initialBalance) 
    {
        this.pin=pin;
        this.balance=initialBalance;
        this.transactions=new ArrayList<>();
    }
    public boolean checkPin(int inputPin) {
        return inputPin == this.pin;
    }
    public void changePin(int oldPin, int newPin) 
    {
        if (checkPin(oldPin)) 
        {
            this.pin=newPin;
            System.out.println("PIN changed successfully.");
        } else 
        {
            System.out.println("Incorrect PIN. Please try again.");
        }
    }
    public void balanceInquiry(int inputPin) 
    {
        if (checkPin(inputPin))
        {
            System.out.println("Your current balance is: $" + this.balance);
        } else 
        {
            System.out.println("Incorrect PIN. Please try again.");
        }
    }
    public void deposit(int inputPin, double amount) 
    {
        if (checkPin(inputPin))
        {
            this.balance += amount;
            this.transactions.add("Deposited $" + amount);
            System.out.println("$" + amount + " deposited successfully.");
        } else 
        {
            System.out.println("Incorrect PIN. Please try again.");
        }
    }
    public void withdraw(int inputPin, double amount) 
    {
        if (checkPin(inputPin))
        {
            if (amount <= this.balance) 
            {
                this.balance -= amount;
                this.transactions.add("Withdrew $" + amount);
                System.out.println("$" + amount + " withdrawn successfully.");
            } else
            {
                System.out.println("Insufficient balance.");
            }
        } else
        {
            System.out.println("Incorrect PIN. Please try again.");
        }
    }
    public void transactionHistory(int inputPin)
    {
        if (checkPin(inputPin)) 
        {
            if (this.transactions.isEmpty())
            {
                System.out.println("No transactions found.");
            } else 
            {
                System.out.println("Transaction History:");
                for (String transaction : this.transactions)
                {
                    System.out.println(transaction);
                }
            }
        } else
        {
            System.out.println("Incorrect PIN. Please try again.");
        }
    }
    public static void main(String[] args)
    {
        Scanner scanner = new Scanner(System.in);
        ATM atm = new ATM(1234, 10000);
        while (true)
        {
            System.out.println("\nATM Machine");
            System.out.println("1. Balance Inquiry");
            System.out.println("2. Deposit");
            System.out.println("3. Withdraw");
            System.out.println("4. Change PIN");
            System.out.println("5. Transaction History");
            System.out.println("6. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();
            switch (choice) 
            {
                case 1:
                    System.out.print("Enter PIN: ");
                    int pin = scanner.nextInt();
                    atm.balanceInquiry(pin);
                    break;
                case 2:
                    System.out.print("Enter PIN: ");
                    pin = scanner.nextInt();
                    System.out.print("Enter amount to deposit: ");
                    double depositAmount = scanner.nextDouble();
                    atm.deposit(pin, depositAmount);
                    break;
                case 3:
                    System.out.print("Enter PIN: ");
                    pin = scanner.nextInt();
                    System.out.print("Enter amount to withdraw: ");
                    double withdrawAmount = scanner.nextDouble();
                    atm.withdraw(pin, withdrawAmount);
                    break;
                case 4:
                    System.out.print("Enter current PIN: ");
                    int oldPin = scanner.nextInt();
                    System.out.print("Enter new PIN: ");
                    int newPin = scanner.nextInt();
                    atm.changePin(oldPin, newPin);
                    break;
                case 5:
                    System.out.print("Enter PIN: ");
                    pin = scanner.nextInt();
                    atm.transactionHistory(pin);
                    break;
                case 6:
                    System.out.println("Thank you for using the ATM. Goodbye!");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }
}

