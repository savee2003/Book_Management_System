# Book_Management_System
package com.hexaware.entities;

import java.util.*;

class Book {
    int bookId;
    String title;
    String author;
    double price;
    boolean isAvailable;

    public Book(int bookId, String title, String author, double price) {
        this.bookId = bookId;
        this.title = title;
        this.author = author;
        this.price = price;
        this.isAvailable = true; 
    }

    public void displayBook() {
        System.out.println(" Book ID: " + bookId + ", Title: " + title + ", Author: " + author +
                ", Price: $" + price + ", Available: " + (isAvailable ? "Yes" : "No"));
    }
}

class Member {
    int memberId;
    String name;
    String membershipType;

    public Member(int memberId, String name, String membershipType) {
        this.memberId = memberId;
        this.name = name;
        this.membershipType = membershipType;
    }

    public void displayMember() {
        System.out.println("👤 Member ID: " + memberId + ", Name: " + name + ", Type: " + membershipType);
    }
}

class RegularMember extends Member {
    public RegularMember(int memberId, String name) {
        super(memberId, name, "Regular");
    }
}

class PremiumMember extends Member {
    public PremiumMember(int memberId, String name) {
        super(memberId, name, "Premium");
    }
}

class Transaction {
    int transactionId;
    int bookId;
    int memberId;
    String borrowDate;

    public Transaction(int transactionId, int bookId, int memberId, String borrowDate) {
        this.transactionId = transactionId;
        this.bookId = bookId;
        this.memberId = memberId;
        this.borrowDate = borrowDate;
    }

    public void displayTransaction() {
        System.out.println(" Transaction ID: " + transactionId + ", Book ID: " + bookId +
                ", Member ID: " + memberId + ", Date: " + borrowDate);
    }
}

public class Final {
    static Scanner sc = new Scanner(System.in);
    static List<Book> books = new ArrayList<>();
    static List<Member> members = new ArrayList<>();
    static List<Transaction> transactions = new ArrayList<>();
    static int bookCounter = 1, memberCounter = 1, transactionCounter = 1;

    public static void main(String[] args) {
        while (true) {
            System.out.println("\n Library Management System");
            System.out.println("1. Book Management");
            System.out.println("2. Member Management");
            System.out.println("3. Borrowing Transactions");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    bookManagement();
                    break;
                case 2:
                    memberManagement();
                    break;
                case 3:
                    borrowingManagement();
                    break;
                case 4:
                    System.out.println("Exiting... Thank you!");
                    return;
                default:
                    System.out.println(" Invalid choice, please try again.");
            }
        }
    }

    public static void bookManagement() {
        while (true) {
            System.out.println("\n Book Management");
            System.out.println("1. Add Book");
            System.out.println("2. Display Books");
            System.out.println("3. Update Availability");
            System.out.println("4. Back to Main Menu");
            System.out.print("Choose an option: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    addBook();
                    break;
                case 2:
                    displayBooks();
                    break;
                case 3:
                    updateBook();
                    break;
                case 4:
                    return;
                default:
                    System.out.println(" Invalid choice!");
            }
        }
    }

    public static void memberManagement() {
        while (true) {
            System.out.println("\n Member Management");
            System.out.println("1. Add Member");
            System.out.println("2. Display Members");
            System.out.println("3. Back to Main Menu");
            System.out.print("Choose an option: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    addMember();
                    break;
                case 2:
                    displayMembers();
                    break;
                case 3:
                    return;
                default:
                    System.out.println("❌ Invalid choice!");
            }
        }
    }

    public static void borrowingManagement() {
        while (true) {
            System.out.println("\n Borrowing Management");
            System.out.println("1. Borrow a Book");
            System.out.println("2. Display Transactions");
            System.out.println("3. Back to Main Menu");
            System.out.print("Choose an option: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    borrowBook();
                    break;
                case 2:
                    displayTransactions();
                    break;
                case 3:
                    return;
                default:
                    System.out.println(" Invalid choice!");
            }
        }
    }

    public static void addBook() {
        System.out.print(" Enter book title: ");
        sc.nextLine();
        String title = sc.nextLine();
        System.out.print(" Enter author: ");
        String author = sc.nextLine();
        System.out.print(" Enter price: ");
        double price = sc.nextDouble();

        books.add(new Book(bookCounter++, title, author, price));
        System.out.println(" Book added successfully!");
    }

    public static void displayBooks() {
        if (books.isEmpty()) {
            System.out.println(" No books available.");
            return;
        }
        for (Book book : books) {
            book.displayBook();
        }
    }

    public static void updateBook() {
        System.out.print(" Enter Book ID to update availability: ");
        int id = sc.nextInt();
        for (Book book : books) {
            if (book.bookId == id) {
                //book.isAvailable = !book.isAvailable;
                System.out.println(" Availability updated!");
                return;
            }
        }
        System.out.println(" Book not found!");
    }

    public static void addMember() {
        System.out.print(" Enter member name: ");
        sc.nextLine();
        String name = sc.nextLine();
        System.out.print(" Enter membership type (Regular/Premium): ");
        String type = sc.nextLine();

        if (type.equalsIgnoreCase("Regular")) {
            members.add(new RegularMember(memberCounter++, name));
        } else {
            members.add(new PremiumMember(memberCounter++, name));
        }
        System.out.println(" Member added successfully!");
    }

    public static void displayMembers() {
        if (members.isEmpty()) {
            System.out.println(" No members available.");
            return;
        }
        for (Member member : members) {
            member.displayMember();
        }
    }

    public static void borrowBook() {
        System.out.print("Enter Book ID to borrow: ");
        int bookId = sc.nextInt();
        System.out.print(" Enter Member ID: ");
        int memberId = sc.nextInt();
        sc.nextLine();
        System.out.print(" Enter Borrow Date: ");
        String date = sc.nextLine();

        for (Book book : books) {
            if (book.bookId == bookId && book.isAvailable) {
               // book.isAvailable = false;
                transactions.add(new Transaction(transactionCounter++, bookId, memberId, date));
                System.out.println(" Book borrowed successfully!");
                return;
            }
        }
        System.out.println(" Book not available!");
    }

    public static void displayTransactions() {
        if (transactions.isEmpty()) {
            System.out.println(" No transactions found.");
            return;
        }
        for (Transaction t : transactions) {
            t.displayTransaction();
        }
    }
}
