---
layout: project
type: project
image: img/librarymanagment.png
title: "Library Management System"
date: 2023
published: true
labels:
  - C/C++
  - Coding
summary: "A basic library management system where users can perform various operations."
---
# <img width="250px"  src="/img/librarymanagment.png" >

## Library Management System Project

Another project for ICS 212, where students are tasked to create a library management system as a group. The library management system includes five features:

1. Add book: add a book to the system
2. Delete book: delete a book in the system
3. Search book: search for a book in the system
4. View all books: view all books in the system
5. Quit: quit the system

Since we divided the projects into parts for each member to work on, I was tasked with doing the main function. The purpose of the main is to print the menu screen for the user to pick what they want to do and it calls on the appropriate function for each action. Since I did not work on any of the functions, I had to coordinate with my teammates to ensure that all their functions worked.

By the end of this project, I had gotten used to the concept of creating functions to call in the main rather than having one giant block of code in the main function. Overall, this project has helped me improve my organizational and coding skills while also learning how to collaborate effectively in a team setting.

Here is the main function:
```cpp
int main() {
   int choice;
   Book book;
   vector<Book> books; //vector to store books
   History h;
   Science s;
   Biography b;
   Fantasy f;
   SciFi sf;

do {
   cout<<"\nLIBRARY MANAGEMENT SYSTEM" << endl;
   cout<<"[1]ADD BOOK" << endl;
   cout<<"[2]DELETE BOOK" << endl;
   cout<<"[3]EDIT BOOK" << endl;
   cout<<"[4]SEARCH BOOK" << endl;
   cout<<"[5]VIEW ALL BOOKS" << endl;
   cout<<"[6]QUIT" << endl;
 
   cout<<"ENTER CHOICE ";
   cin>>choice;
   string userTitle, userAuthor, userEdition, userPublication;
   int userIsbn, temp, deleteIsbn;
   
   switch(choice) {
   case 1: //add book
 
   cout << "ISBN: ";
   cin >> userIsbn;
 
   cout << "Enter Title: ";
   cin.ignore(); // Clear the buffer
   getline(cin, userTitle);

   cout << "Enter Author: ";
   getline(cin, userAuthor);

   cout << "Enter Edition: ";
   getline(cin, userEdition);

   cout << "Enter Publication: ";
   getline(cin, userPublication);
   cout << "Choose: \n[1]Nonfiction \n[2]Fiction\n";
   cin>>temp;
   if(temp==1){
       cout << "Select Genre:\n[1]History\n[2]Science\n[3]Biography\n";
       cin>>temp;
       switch(temp){
           case 1:
           h.setIsbn(userIsbn);
           h.setAuthor(userAuthor);
           h.setEdition(userEdition);
           h.setPublication(userPublication);
           h.setTitle(userTitle);
           h.setGenre("History");
           books.push_back(h); //add to vector
           break;
           case 2:
           s.setIsbn(userIsbn);
           s.setAuthor(userAuthor);
           s.setEdition(userEdition);
           s.setPublication(userPublication);
           s.setTitle(userTitle);
           s.setGenre("Science");
           books.push_back(s);
           break;
           case 3:
           b.setIsbn(userIsbn);
           b.setAuthor(userAuthor);
           b.setEdition(userEdition);
           b.setPublication(userPublication);
           b.setTitle(userTitle);
           b.setGenre("Biography");
           books.push_back(b);
           break;
       }
   } else{
       cout << "Select Genre: \n[1]Fantasy\n[2]SciFi\n";
       cin>>temp;
       if(temp == 1){
           f.setIsbn(userIsbn);
           f.setAuthor(userAuthor);
           f.setEdition(userEdition);
           f.setPublication(userPublication);
           f.setTitle(userTitle);
           f.setGenre("Fiction");
           books.push_back(f);
       } else{
           sf.setIsbn(userIsbn);
           sf.setAuthor(userAuthor);
           sf.setEdition(userEdition);
           sf.setPublication(userPublication);
           sf.setTitle(userTitle);
           sf.setGenre("SciFi");
           books.push_back(sf);
       }
   }
   cout << "Book added successfully!" << endl;
   break;

   case 2: //delete Book
 
   cout << "Enter ISBN of the book to delete: ";
   cin >> deleteIsbn;

   for(int i = 0; i < books.size(); i++){
       if(books[i].getIsbn() == deleteIsbn){
           books.erase(books.begin()+i);
           break;
       }
   }
   cout << "\nBook deleted\n";
   break;
 
   case 3: //edit book
   cout << "Enter ISBN of the book to edit: ";
   cin >> userIsbn;
   int index;
   for(int j = 0; j < books.size(); j++){
       if(books[j].getIsbn() == userIsbn){
           index = j;
           break;
       }
   }
   cout << "\nCurrent ISBN: " << books[index].getIsbn() << "\nEnter new ISBN: ";
   int newIsbn;
   cin>>newIsbn;
   books[index].setIsbn(newIsbn);

   cout << "\nCurrent Title: " << books[index].getTitle() << "\nEnter new Title: ";
   getline(cin, userTitle);
   books[index].setTitle(userTitle);

   cout << "\nCurrent Author: " << books[index].getAuthor() << "\nEnter new Author: ";
   getline(cin, userAuthor);
   books[index].setAuthor(userAuthor);

   cout << "\nCurrent Edition: " << books[index].getEdition() << "\nEnter new Edition: ";
   getline(cin, userEdition);
   books[index].setEdition(userEdition);

   cout << "\nCurrent Publication: " << books[index].getPublication() << "\nEnter new Publication: ";
   getline(cin, userPublication);
   books[index].setPublication(userPublication);

   cout << "Book details updated successfully!" << endl;
   break;
 
   case 4: //search book
       int searchIsbn;
       cout << "Enter ISBN of the book to search: ";
       cin >> searchIsbn;
       for(int k = 0; k < books.size(); k++){
           if(books[k].getIsbn() == searchIsbn){
               cout << "\nTitle: "<<books[k].getTitle();
               cout << "\nAuthor: "<<books[k].getAuthor();
               cout << "\nEdition: "<<books[k].getEdition();
               cout << "\nPublication: "<<books[k].getPublication();
               cout << "\nGenre: " << books[k].getGenre() << endl;
           }
       }
   break;
 
   case 5: //view all books                                   
       if (books.empty()) { //if the vector is empty
           cout << "No books in the library." << endl;
       break;
       }
       else {
           for(int l = 0; l < books.size(); l++){
               cout << "\nISBN: "<<books[l].getIsbn();
               cout << "\nTitle: "<<books[l].getTitle();
               cout << "\nAuthor: "<<books[l].getAuthor();
               cout << "\nEdition: "<<books[l].getEdition();
               cout << "\nPublication: "<<books[l].getPublication();
               cout << "\nGenre: " << books[l].getGenre() << endl;
           }
   }
   break;
 
   case 6: //quit
   cout << "Exiting..." << endl;
   break;
 
   default:
   cout << "Please pick a number from 1-6" << endl;
     }
   }
while (choice != 6);
return 0;
}
```



