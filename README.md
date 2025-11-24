import java.util.*;

class Book {
    private int id;
    private String title;
    private String author;
    private boolean isBorrowed;

    public Book(int id, String title, String author) {
        this.id = id;
        this.title = title;
        this.author = author;
        this.isBorrowed = false;
    }

    public int getId() { return id; }
    public String getTitle() { return title; }
    public String getAuthor() { return author; }
    public boolean isBorrowed() { return isBorrowed; }

    public void borrowBook() { this.isBorrowed = true; }
    public void returnBook() { this.isBorrowed = false; }

    @Override
    public String toString() {
        return String.format("ID: %d | Title: %s | Author: %s | %s",
                id, title, author, (isBorrowed ? "Borrowed" : "Available"));
    }
}

class Library {
    private List<Book> books = new ArrayList<>();

    public void addBook(Book book) {
        books.add(book);
        System.out.println("✅ Book added successfully!");
    }

    public void viewBooks() {
        if (books.isEmpty()) {
            System.out.println("📚 No books available.");
            return;
        }
        System.out.println("\n----- Library Books -----");
        for (Book book : books) {
            System.out.println(book);
        }
    }

    public void borrowBook(int bookId) {
        for (Book book : books) {
            if (book.getId() == bookId) {
                if (!book.isBorrowed()) {
                    book.borrowBook();
                    System.out.println("📖 You borrowed: " + book.getTitle());
                } else {
                    System.out.println("❌ Book is already borrowed.");
                }
                return;
            }
        }
        System.out.println("❌ Book not found.");
    }

    public void returnBook(int bookId) {
        for (Book book : books) {
            if (book.getId() == bookId) {
                if (book.isBorrowed()) {
                    book.returnBook();
                    System.out.println("✅ Book returned successfully!");
                } else {
                    System.out.println("❌ Book was not borrowed.");
                }
                return;
            }
        }
        System.out.println("❌ Book not found.");
    }
}

public class LibraryManagementSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Library library = new Library();

        while (true) {
            System.out.println("\n===== ONLINE LIBRARY MANAGEMENT SYSTEM =====");
            System.out.println("1. Add Book");
            System.out.println("2. View Books");
            System.out.println("3. Borrow Book");
            System.out.println("4. Return Book");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter Book ID: ");
                    int id = scanner.nextInt();
                    scanner.nextLine();
                    System.out.print("Enter Book Title: ");
                    String title = scanner.nextLine();
                    System.out.print("Enter Author Name: ");
                    String author = scanner.nextLine();

                    library.addBook(new Book(id, title, author));
                    break;

                case 2:
                    library.viewBooks();
                    break;

                case 3:
                    System.out.print("Enter Book ID to borrow: ");
                    int borrowId = scanner.nextInt();
                    library.borrowBook(borrowId);
                    break;

                case 4:
                    System.out.print("Enter Book ID to return: ");
                    int returnId = scanner.nextInt();
                    library.returnBook(returnId);
                    break;

                case 5:
                    System.out.println("👋 Thank you for using the system!");
                    scanner.close();
                    System.exit(0);
                    break;

                default:
                    System.out.println("❌ Invalid choice. Try again.");
            }
        }
    }
}
