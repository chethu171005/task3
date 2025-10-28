import java.util.ArrayList;
import java.util.Scanner;

class Book {
    int id;
    String title;
    boolean isIssued;

    Book(int id, String title) {
        this.id = id;
        this.title = title;
        this.isIssued = false;
    }
}

class User {
    int userId;
    String name;

    User(int userId, String name) {
        this.userId = userId;
        this.name = name;
    }
}

class Library {
    ArrayList<Book> books = new ArrayList<>();

    void addBook(Book b) {
        books.add(b);
        System.out.println("✅ Book added!");
    }

    void issueBook(int id) {
        for (Book b : books) {
            if (b.id == id && !b.isIssued) {
                b.isIssued = true;
                System.out.println("📖 Book issued successfully!");
                return;
            }
        }
        System.out.println("❌ Book not available!");
    }

    void returnBook(int id) {
        for (Book b : books) {
            if (b.id == id && b.isIssued) {
                b.isIssued = false;
                System.out.println("🔁 Book returned successfully!");
                return;
            }
        }
        System.out.println("❌ Invalid book ID or not issued!");
    }

    void showBooks() {
        System.out.println("\n--- Available Books ---");
        for (Book b : books) {
            System.out.println("ID: " + b.id + ", Title: " + b.title + ", Issued: " + b.isIssued);
        }
    }
}

public class LibrarySystem {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Library library = new Library();
        int choice;

        do {
            System.out.println("\n===== Library Management System =====");
            System.out.println("1. Add Book");
            System.out.println("2. Issue Book");
            System.out.println("3. Return Book");
            System.out.println("4. Show Books");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1 -> {
                    System.out.print("Enter Book ID: ");
                    int id = sc.nextInt();
                    sc.nextLine();
                    System.out.print("Enter Book Title: ");
                    String title = sc.nextLine();
                    library.addBook(new Book(id, title));
                }
                case 2 -> {
                    System.out.print("Enter Book ID to issue: ");
                    library.issueBook(sc.nextInt());
                }
                case 3 -> {
                    System.out.print("Enter Book ID to return: ");
                    library.returnBook(sc.nextInt());
                }
                case 4 -> library.showBooks();
                case 5 -> System.out.println("Exiting...");
                default -> System.out.println("Invalid choice!");
            }
        } while (choice != 5);

        sc.close();
    }
}
