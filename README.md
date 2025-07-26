import java.util.ArrayList;

public class Account {
    private String accountNumber;
    private String holderName;
    private double balance;
    private ArrayList<String> transactions;

    public Account(String accountNumber, String holderName, double initialDeposit) {
        this.accountNumber = accountNumber;
        this.holderName = holderName;
        this.balance = initialDeposit;
        this.transactions = new ArrayList<>();
        transactions.add("Account created with balance: ₹" + initialDeposit);
    }

    public String getAccountNumber() {
        return accountNumber;
    }

    public String getHolderName() {
        return holderName;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        balance += amount;
        transactions.add("Deposited: ₹" + amount);
    }

    public void withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
            transactions.add("Withdrawn: ₹" + amount);
        } else {
            transactions.add("Failed Withdrawal: ₹" + amount + " (Insufficient Balance)");
        }
    }

    public ArrayList<String> getTransactions() {
        return transactions;
    }

    public String toFileString() {
        return accountNumber + "," + holderName + "," + balance;
    }

    public static Account fromFileString(String line) {
        String[] parts = line.split(",");
        return new Account(parts[0], parts[1], Double.parseDouble(parts[2]));
    }
}
