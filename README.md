import java.util.Scanner;

class Product {
    private String name;
    private double price;

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }
}

class VendingMachine {
    private Product chips;
    private Product soda;
    private Product candy;

    public VendingMachine() {
        chips = new Product("Chips", 1.50);
        soda = new Product("Soda", 1.00);
        candy = new Product("Candy", 0.75);
    }

    public void showMenu() {
        System.out.println("---- VENDING MACHINE ----");
        System.out.printf("1. %s - $%.2f%n", chips.getName(), chips.getPrice());
        System.out.printf("2. %s - $%.2f%n", soda.getName(), soda.getPrice());
        System.out.printf("3. %s - $%.2f%n", candy.getName(), candy.getPrice());
    }

    public Product getProduct(int choice) {
        if (choice == 1) return chips;
        if (choice == 2) return soda;
        if (choice == 3) return candy;
        return null;
    }

    public double processPurchase(Product selected, double balance) {
        if (selected == null) {
            System.out.println("Invalid selection.");
            return balance;
        }

        if (balance < selected.getPrice()) {
            System.out.println("Insufficient balance.");
            return balance;
        }

        balance -= selected.getPrice();
        System.out.println("You bought: " + selected.getName());
        System.out.printf("Remaining balance: $%.2f%n", balance);

        return balance;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        VendingMachine machine = new VendingMachine();

        System.out.println("Insert money (Only $5 or $10 bills accepted): ");
        int bill = input.nextInt();

        if (bill != 5 && bill != 10) {
            System.out.println("Invalid bill. Machine only accepts $5 or $10.");
            input.close();
            return;
        }

        double balance = bill;

        machine.showMenu();

        System.out.print("Select item: ");
        int choice = input.nextInt();

        Product selected = machine.getProduct(choice);
        balance = machine.processPurchase(selected, balance);

        System.out.printf("Change returned: $%.2f%n", balance);

        input.close();
    }
}
