# Hotel Inventory API
### Overview:

This project is a Hotel Inventory RESTful API designed to create hotels and associated reservations. The user can create a hotel, search for available hotels, search for all hotels within the database, all reservations within the database, make reservations to a specific hotel, delete reservations as well as hotels. Necessary validation is incorporated within the API that prevents illogical operations from occurring such as making an overlapping reservation to a hotel or deleting a hotel that contains reservations.

The Hotel-Inventory-API follows a standard "User <-> Controller <-> Validator (Only interacts with Controller) <-> Service <-> Repository <-> Database" API schema. Where the data flows down from the User to the database and then back to the User. 

### Detailed Overview:

#### Valid API Calls: 

##### Use Case: Create Hotel/Inventory 

#####  Use Case: Update a hotel inventory object
 
#####  Use Case: Get a user specific hotel inventory object


#####  Use Case: Get all existing hotel inventories 
 
#####  Use Case: Delete a user specified hotel inventory
 

#####  Use Case: Create a reservation

#####  Use Case: Get all reservations

#####  Use Case: Get a specified hotel reservation
 
#####  Use Case: Delete a user specified reservation
 
#####  Use Case: Get all available hotel inventories
 
#### Database
  The relational database I used for this project was created using SQL using mySQL. The database structure contains two tables, an Inventory table that contains the hotel inventory object and a Reservations table. The Reservations table contains reservations objects and is associated with the Inventory table through the Inventory table's Id by storing it as a foreign key in its "Inventory Id" value. The table structures and values are as follows: 
 
  - Inventory 
    - Id: Integer (Primary Key) 
    - Name: VarChar
    - Type: VarChar
    - Description: VarChar
    - Availiable From: Date 
    - Available To: Date 
    - Status: Boolean 
  - Reservations 
    -  Id: Integer (Primary Key) 
    -  Inventory Id: Integer (Foreign Key) 
    -  Check in Date: Date 
    -  Check out Date: Date
    -  Number of Guests: Integer 
    -  Status: Boolean 
  
  The database was created with the commands as follows: 
  
```sql
DROP TABLE INVENTORY IF EXISTS;
DROP TABLE RESERVATION IF EXISTS;
 
CREATE TABLE INVENTORY (
    id INT AUTO_INCREMENT PRIMARY KEY,
    NAME VARCHAR(30) NOT NULL,
    TYPE VARCHAR (10) NOT NULL,
    DESCRIPTION VARCHAR(255),
    DT_AVAILABLE_FROM DATE,
    DT_AVAILABLE_TO DATE,
    STATUS BOOLEAN
)  ENGINE=INNODB;
 
CREATE TABLE RESERVATION (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    DT_CHECK_IN DATE NOT NULL,
    DT_CHECK_OUT DATE NOT NULL,
    GUESTS INT default 1,
    STATUS BOOLEAN,
    INVENTORY_ID INT,
    FOREIGN KEY (INVENTORY_ID) REFERENCES INVENTORY (ID)
) ENGINE=INNODB;
 
ALTER TABLE RESERVATION
ADD CONSTRAINT unique_reservation
UNIQUE (INVENTORY_ID, DT_CHECK_IN, DT_CHECK_OUT, STATUS);
```
  
