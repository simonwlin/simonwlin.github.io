---
layout: project
type: project
image: img/hotel.PNG
title: "Hotel Management System"
date: 2023
published: true
labels:
  - Coding
  - C/C++
summary: "A basic hotel management system where users can perform various operations."
---

# <img width="250px"  src="/img/hotel.PNG" >

## Hotel Management System Project

As our final project/exam for ICS 212, students were tasked to create a hotel management system as a group. As a group of six people, we divided the project into parts for each member to work on. The hotel management system included seven features:

1. Manage Rooms: add new rooms, search rooms, and delete rooms.
2. Check-In Room: check-in guests.
3. Available Rooms: displays a list of available rooms
4. Search Customer: searches the guest's information
5. Check-Out Room: check-out guests
6. Guest Summary Report: generates a summary of guests that are checked in. 
7. Exit: exits the system

Since this project was divided into different parts for each member to work on, I was responsible for writing the searchCustomer(), checkOutRoom(), and guestSummaryReport() functions. While working on these fucntions, I did come across some problems. For example, we needed to create additional helper functions and call them correctly. Additionally, we had to use consistent variable names and data structures across all modules otherwise we would come across an error. In the end, we managed to get the code to work by communicating with each other and helping each other out. 

As a result of this project, I have significantly improved my coding skills in C++. This project has taught me that there are multiple ways of approaching a problem, and communication is important when working in a group. I hope to apply these skills when it comes to software engineering because it would be helpful. In the future, I aim to participate in more group projects to further enhance my coding skills. 

Here is the 'searchCustomer()', 'checkOutRoom()', and 'guestSummaryReport()' function:
```cpp
//Iterate through the guests and find if the guest's name matches the inputed name or an error if there is no match found 
void searchCustomer(const vector<Customer>& guests) {
    string userName;
    cout << "Enter Customer Name: ";
    cin.ignore();  // Ignore newline character left in the buffer
    getline(cin, userName);

      for(int i = 0; i < guests.size(); i++){
        if(userName == guests[i].getName()){
          guests[i].displayCustomerDetails();
          return;
        }
      }
      cout << "Customer not found" << endl;
}
//Checks a guest out of a room by iterating through the guest and room vectors to find if the correct guest and room, then removes the guest from the room and marks the room as available
void checkOutRoom(vector<Customer>& guests, vector<Room>& rooms) {
    int roomNumber, numDays, roomIndex = -1, guestIndex = -1;
    cout << "Enter Room Number: ";
    cin >> roomNumber;
  //checks to see if room number matches the guest's room number and the rooms room number
    for(int i = 0; i < guests.size(); i++){
      if(roomNumber == guests[i].getRoomNumber()){
        guestIndex = i;
        break;
      }
    }
    for(int j = 0; j < rooms.size(); j++){
      if(rooms[j].getNumber() == roomNumber){
        roomIndex = j;
      }
    }
        cout << "Enter length of stay: ";
        cin >> numDays;
      //displays the customer's information and amount due
        guests[guestIndex].displayCheckOutDetails(rooms[roomIndex].getRent() * numDays);

        // Mark the room as available
        rooms[roomIndex].unbook();
}
//Lists all the guests with their information as displayed by the displayCustomerDetails() function
void guestSummaryReport(const vector<Customer>& guests) {
    cout << "##### Guest Summary Report #####" << endl;
    for(int i = 0; i < guests.size(); i++) {
        guests[i].displayCustomerDetails();
        cout << "--------------------------" << endl;
    }
}
```
