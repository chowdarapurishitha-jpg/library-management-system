# library-management-system
The Library Management System is a Python-based application designed to automate and simplify the management of library operations. The system helps librarians maintain book records efficiently and reduces the manual effort involved in handling library activities.
def add_book():
    book = input("Enter Book Name: ")

    with open("books.txt", "a") as file:
        file.write(book + "\n")

    print("Book Added Successfully!")


def view_books():
    try:
        with open("books.txt", "r") as file:
            books = file.readlines()

        print("\nAvailable Books:")

        for book in books:
            print(book.strip())

    except FileNotFoundError:
        print("No books found.")


def search_book():
    search = input("Enter Book Name: ")

    try:
        with open("books.txt", "r") as file:
            books = file.readlines()

        found = False

        for book in books:
            if search.lower() in book.lower():
                print("Book Found:", book.strip())
                found = True

        if not found:
            print("Book Not Found")

    except FileNotFoundError:
        print("No books found.")


def issue_book():
    book_name = input("Enter Book Name to Issue: ")

    with open("books.txt", "r") as file:
        books = file.readlines()

    found = False

    with open("books.txt", "w") as file:
        for book in books:
            if book.strip().lower() != book_name.lower():
                file.write(book)
            else:
                found = True

    if found:
        with open("issued_books.txt", "a") as file:
            file.write(book_name + "\n")

        print("Book Issued Successfully!")
    else:
        print("Book Not Available")


def return_book():
    book_name = input("Enter Book Name to Return: ")

    with open("issued_books.txt", "r") as file:
        books = file.readlines()

    found = False

    with open("issued_books.txt", "w") as file:
        for book in books:
            if book.strip().lower() != book_name.lower():
                file.write(book)
            else:
                found = True

    if found:
        with open("books.txt", "a") as file:
            file.write(book_name + "\n")

        print("Book Returned Successfully!")
    else:
        print("Book not issued")


while True:
    print("\n===== Library Management System =====")
    print("1. Add Book")
    print("2. View Books")
    print("3. Search Book")
    print("4. Issue Book")
    print("5. Return Book")
    print("6. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":
        add_book()

    elif choice == "2":
        view_books()

    elif choice == "3":
        search_book()

    elif choice == "4":
        issue_book()

    elif choice == "5":
        return_book()

    elif choice == "6":
        print("Thank you!")
        break

    else:
        print("Invalid Choice")
