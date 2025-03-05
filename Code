#include <iostream>
#include <vector>
#include <string>
#include <fstream>
#include <cstdlib>
#include <ctime>
#include <algorithm>

using namespace std;

class Book {
public:
    string title, author, isbn, description;
    double price;
    int quantity, quantitySold;

    Book(string t, string a, string i, double p, int q, string desc) 
        : title(t), author(a), isbn(i), price(p), quantity(q), quantitySold(0), description(desc) {}

    void display() const {
        cout << "Title: " << title << " | Author: " << author << " | ISBN: " << isbn 
             << " | Price: " << price << " RON | Quantity: " << quantity << endl;
    }

    void displayDetails() const {
        cout << "\nTitle: " << title 
             << "\nAuthor: " << author 
             << "\nISBN: " << isbn 
             << "\nPrice: " << price << " RON" 
             << "\nQuantity in stock: " << quantity 
             << "\nDescription: " << description 
             << "\nQuantity Sold This Month: " << quantitySold << endl;
    }
};

class Library {
private:
    vector<Book> books;
    const string filename = "library.txt";
    const string monthFile = "month_sales.txt";

    void loadFromFile() {
        ifstream file(filename);
        if (!file) return;

        string title, author, isbn, description;
        double price;
        int quantity;
        while (getline(file, title) && getline(file, author) && getline(file, isbn) && file >> price >> quantity) {
            file.ignore();
            getline(file, description);
            books.emplace_back(title, author, isbn, price, quantity, description);
        }
        file.close();
    }

    void saveToFile() const {
        ofstream file(filename);
        for (const auto& book : books) {
            file << book.title << "\n" << book.author << "\n" << book.isbn << "\n" << book.price << "\n" << book.quantity << "\n" << book.description << "\n";
        }
        file.close();
    }

    void saveSalesData() const {
        ofstream file(monthFile);
        for (const auto& book : books) {
            file << book.isbn << "\n" << book.quantitySold << "\n";
        }
        file.close();
    }

public:
    Library() { loadFromFile(); }

    void addBook(const string& title, const string& author, const string& isbn, int quantity, const string& description) {
        double price = (rand() % 91) + 10;
        books.emplace_back(title, author, isbn, price, quantity, description);
        saveToFile();
        cout << "Book added successfully! Price: " << price << " RON, Quantity: " << quantity << endl;
    }

    void displayBooksOfTheMonth() const {
        cout << "\nBooks of the Month:\n";
        for (int i = 0; i < 10; ++i) {
            cout << i + 1 << ". " << books[i].title << " by " << books[i].author << endl;
        }
    }

    void showBookDetails(int index) const {
        if (index >= 0 && index < books.size()) {
            books[index].displayDetails();
        } else {
            cout << "Invalid book selection.\n";
        }
    }

    void buyBook(const string& isbn, int quantityToBuy) {
        auto it = find_if(books.begin(), books.end(), [&](const Book& book) { return book.isbn == isbn; });
        if (it != books.end()) {
            if (it->quantity >= quantityToBuy) {
                cout << "You bought " << quantityToBuy << " copies of the book: " << it->title << " for " 
                     << it->price * quantityToBuy << " RON." << endl;
                it->quantity -= quantityToBuy;
                it->quantitySold += quantityToBuy;
                saveToFile();
                saveSalesData();
            } else {
                cout << "Not enough stock. Only " << it->quantity << " copies available.\n";
            }
        } else {
            cout << "Book not found.\n";
        }
    }

    void searchByTitle(const string& title) const {
        for (const auto& book : books) {
            if (book.title.find(title) != string::npos) {
                book.display();
            }
        }
    }

    void searchByAuthor(const string& author) const {
        for (const auto& book : books) {
            if (book.author.find(author) != string::npos) {
                book.display();
            }
        }
    }

    void displayAllBooks() const {
        if (books.empty()) {
            cout << "No books in the library.\n";
            return;
        }
        for (const auto& book : books) {
            book.display();
        }
    }
};

void showMainMenu() {
    cout << "\nBookStore Management System";
    cout << "\n1. Add Book";
    cout << "\n2. Search by Title";
    cout << "\n3. Search by Author";
    cout << "\n4. Display All Books";
    cout << "\n5. Buy Book";
    cout << "\n6. Books of the Month";
    cout << "\n7. Exit";
    cout << "\nEnter your choice: ";
}

int main() {
    srand(time(0));

    Library library;
    int choice;
    string title, author, isbn, description;
    int quantity, quantityToBuy, bookChoice;

    vector<Book> booksOfTheMonth = {
    Book("Romeo and Juliet", "William Shakespeare", "978-0143128562", 20, 50, "A tragic love story between Romeo and Juliet, two young lovers from feuding families."),
    Book("Moby Dick", "Herman Melville", "978-1503280786", 25, 30, "The journey of Captain Ahab as he pursues the white whale Moby Dick."),
    Book("1984", "George Orwell", "978-0451524935", 15, 100, "A dystopian novel set in a totalitarian society controlled by the Party and Big Brother."),
    Book("To Kill a Mockingbird", "Harper Lee", "978-0061120084", 18, 75, "A story of racial injustice and the loss of innocence in the American South."),
    Book("The Great Gatsby", "F. Scott Fitzgerald", "978-0743273565", 22, 60, "A novel about the American Dream and the tragic life of Jay Gatsby."),
    Book("Pride and Prejudice", "Jane Austen", "978-1503290563", 20, 80, "A romantic novel that critiques social class and marriage in 19th-century England."),
    Book("War and Peace", "Leo Tolstoy", "978-1400079988", 30, 20, "A historical novel that follows the lives of aristocratic families during the Napoleonic wars."),
    Book("The Catcher in the Rye", "J.D. Salinger", "978-0316769488", 15, 50, "A young man\"s journey of self-discovery as he struggles with growing up."),
    Book("The Hobbit", "J.R.R. Tolkien", "978-0345339683", 12, 40, "The adventure of Bilbo Baggins, a hobbit who embarks on a quest with dwarves and a wizard."),
    Book("The Lord of the Rings", "J.R.R. Tolkien", "978-0618640157", 35, 90, "An epic fantasy trilogy following the journey to destroy the One Ring.")
};
 vector<Book> books1123 = {
   Book("The Alchemist", "Paulo Coelho", "978-0061122415", 22, 50, "A young shepherd's journey to discover his personal legend and find treasure."),
Book("The Catcher in the Rye", "J.D. Salinger", "978-0316769488", 15, 60, "A disillusioned teen's perspective on life and growing up."),
Book("The Road", "Cormac McCarthy", "978-0307387899", 28, 45, "A father and son navigate a post-apocalyptic world, struggling to survive."),
Book("Brave New World", "Aldous Huxley", "978-0060850524", 20, 75, "A dystopian society where individuals are conditioned to conform to societal norms."),
Book("The Great Gatsby", "F. Scott Fitzgerald", "978-0743273565", 22, 60, "The tragic tale of Jay Gatsby's pursuit of the American Dream."),
Book("To Kill a Mockingbird", "Harper Lee", "978-0061120084", 18, 85, "A young girl's coming-of-age story in the racially segregated South."),
Book("1984", "George Orwell", "978-0451524935", 15, 90, "A bleak look at a totalitarian regime where freedom of thought is forbidden."),
Book("The Hobbit", "J.R.R. Tolkien", "978-0345339683", 12, 40, "Bilbo Baggins embarks on a quest with dwarves to reclaim a lost treasure."),
Book("The Shining", "Stephen King", "978-0307743657", 30, 50, "A family trapped in a haunted hotel, with terrifying and supernatural events."),
Book("Frankenstein", "Mary Shelley", "978-0486282114", 25, 55, "A scientist creates a monster and suffers the consequences of his ambition.")
};

    for (const auto& book : booksOfTheMonth) {
        library.addBook(book.title, book.author, book.isbn, book.quantity, book.description);
    }
 for (const auto& book : books1123) {
        library.addBook(book.title, book.author, book.isbn, book.quantity, book.description);
    }

    do {
        showMainMenu();
        cin >> choice;
        cin.ignore();

        switch (choice) {
            case 1:
                cout << "Enter title: "; getline(cin, title);
                cout << "Enter author: "; getline(cin, author);
                cout << "Enter ISBN: "; getline(cin, isbn);
                cout << "Enter quantity: "; cin >> quantity;
                cin.ignore();
                cout << "Enter description: "; getline(cin, description);
                library.addBook(title, author, isbn, quantity, description);
                break;
            case 2:
                cout << "Enter title to search: "; getline(cin, title);
                library.searchByTitle(title);
                break;
            case 3:
                cout << "Enter author to search: "; getline(cin, author);
                library.searchByAuthor(author);
                break;
            case 4:
                library.displayAllBooks();
                break;
            case 5:
                cout << "Enter ISBN of the book you want to buy: "; getline(cin, isbn);
                cout << "Enter quantity to buy: "; cin >> quantityToBuy;
                library.buyBook(isbn, quantityToBuy);
                break;
            case 6:
                library.displayBooksOfTheMonth();
                cout << "Select a book to see details (1-10): ";
                cin >> bookChoice;
                cin.ignore();
                library.showBookDetails(bookChoice - 1);
                break;
            case 7:
                cout << "Exiting...\n";
                break;
            default:
                cout << "Invalid choice. Try again!\n";
        }
    } while (choice != 7);
    
    return 0;
}
