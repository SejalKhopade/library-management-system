# library-management-system
import java.util.ArrayList;

class Book {
    private String title;
    private String author;
    private boolean isCheckedOut;

    public Book(String title, String author) {
        this.title = title;
        this.author = author;
        this.isCheckedOut = false;
    }

    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }

    public boolean isCheckedOut() {
        return isCheckedOut;
    }

    public void setCheckedOut(boolean checkedOut) {
        isCheckedOut = checkedOut;
    }
}

class LibraryCatalog {
    private ArrayList<Book> books;

    public LibraryCatalog() {
        this.books = new ArrayList<>();
    }

    public void addBook(Book book) {
        books.add(book);
    }

    public Book searchByTitle(String title) {
        for (Book book : books) {
            if (book.getTitle().equals(title)) {
                return book;
            }
        }
        return null;
    }

    public ArrayList<Book> searchByAuthor(String author) {
        ArrayList<Book> booksByAuthor = new ArrayList<>();
        for (Book book : books) {
            if (book.getAuthor().equals(author)) {
                booksByAuthor.add(book);
            }
        }
        return booksByAuthor;
    }

    public boolean checkOutBook(String title) {
        Book book = searchByTitle(title);
        if (book != null && !book.isCheckedOut()) {
            book.setCheckedOut(true);
            return true;
        }
        return false;
    }

    public void returnBook(String title) {
        Book book = searchByTitle(title);
        if (book != null && book.isCheckedOut()) {
            book.setCheckedOut(false);
        }
    }
}

class library{
    public static void main(String[] args) {
        LibraryCatalog library = new LibraryCatalog();

        // Adding books
        library.addBook(new Book("The Great Gatsby", "F. Scott Fitzgerald"));
        library.addBook(new Book("To Kill a Mockingbird", "Harper Lee"));

        // Searching for books
        Book bookByTitle = library.searchByTitle("The Great Gatsby");
        System.out.println("Book found by title: " + bookByTitle.getTitle());

        ArrayList<Book> booksByAuthor = library.searchByAuthor("Harper Lee");
        System.out.println("Books found by author: ");
        for (Book book : booksByAuthor) {
            System.out.println(book.getTitle());
        }

        // Checking out and returning books
        library.checkOutBook("The Great Gatsby");
        System.out.println("Is The Great Gatsby checked out? " + library.searchByTitle("The Great Gatsby").isCheckedOut());

        library.returnBook("The Great Gatsby");
        System.out.println("Is The Great Gatsby checked out now? " + library.searchByTitle("The Great Gatsby").isCheckedOut());
    }
}
