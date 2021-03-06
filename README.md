                                              BOOKS STORE APPLICATION
---

**Requirements**

**as a**

- **USER** and  **PUBLISHER**

    - I should get an error message if the username and password are wrong
    - I should be able to list books
    - Search specific book (pagination support)
    - See the details of book and author (GET)

- **USER**
    - I should be able to list all books published by specific publisher
    - I should be able to register with a valid email (bonus)

- **PUBLISHER**
    -  I should be able to login to the system when a valid username and password supplied
    - I should be able to list books
    - I should be able to add new book to the book list
    - I should be able update a specific book details that has been published by me
---


- **Database Diagram**

![link](https://i.postimg.cc/Xq43Lmfy/Screenshot-7.png)

---

- **Publishers** table


![link](https://i.postimg.cc/NjdX05Dy/publishers-tablee.png)

---

- **Authors** table

![link](https://i.postimg.cc/kG9JPvkk/authors.png)


---


- **Books** table

![link](https://i.postimg.cc/g08bc6qd/books-tableee.png)

---


- **authors_books** table

![link](https://i.postimg.cc/nh96TQW7/autho-books-table.png)

---

- **Users** table


[![users-table.png](https://i.postimg.cc/Jz0mT9KL/users-table.png)](https://postimg.cc/Yh5J0DJn)


--- - -


- **Roles** table

[![roles-table.png](https://i.postimg.cc/TwG4sbGD/roles-table.png)](https://postimg.cc/5H7gY6X4)

---

- **users_roles** table

[![users-roles-table.png](https://i.postimg.cc/8P3nS9ND/users-roles-table.png)](https://postimg.cc/hfL08CX3) 
---


- **SIGN IN**
   - **POST**

      http://127.0.0.1:8088/v1/auth/login  





- **REFRESH EXPIRED TOKEN**
     - **GET**
 
        http://127.0.0.1:8088/v1/auth/token/refresh

  You need to enter the refresh token as in the picture

![link](https://i.postimg.cc/9Qx1J9S0/Inked-Screenshot-2-LI.jpg)






- *Authorization*

- ![link](https://i.postimg.cc/4d9BDrtx/Screenshot-2.png)

AS **PUBLISHER**

![link](https://i.postimg.cc/s2DCq5wh/publisher.png)

AS **USER**

![link](https://i.postimg.cc/7LQdRd5F/user.png)
---
-  For all requests you need to send the token in the header as shown in the picture except registration as user

![link](https://i.postimg.cc/YqMJP1Xz/Screenshot-3.png)


- As a **USER** and **PUBLISHER** to search specific book (pagination support)
   - **GET**
     
      http://127.0.0.1:8088/v1/books?count=10&name=somename&page=0

-- -

-  As a **USER** and **PUBLISHER**  Get all books
     - **GET**
      
       http://127.0.0.1:8088/v1/books?count=10&page=0

----
- As a **USER** and **PUBLISHER**  to see the details of book and author
  - **GET**
      
     http://127.0.0.1:8088/v1/authors/{id} (1-38)

- ----
- As a **USER**, I should be able to list all books published by specific publisher
   - **GET**
      
      http://127.0.0.1:8088/v1/publishers/{id}  (1-13)

----
- As a **USER**, I should be able to register with a valid email
   - **POST**

     http://127.0.0.1:8088/v1/users (without authentication)

Request  Body
```json
{
  "firstName" :"firstName",
  "lastName": "lastname",
  "age" : 20,
  "username" : "username",
  "password" : "password",
  "email": "email@gmail.com"
}
```

Validation

```java
    @NotNull
    @NotBlank
    private String firstName;

    @NotBlank
    @NotNull
    private String lastName;

    @NotNull
    @Min(value = 12)
    @Max(value = 80)
    private Integer age;

    @NotNull
    @NotBlank
    @Size(min = 6, max = 16)
    private String username; (unique)
    
    @NotNull
    @NotBlank
    @Size(min = 6, max = 16)
    private String password;
    
    @Email
    @Size(min = 14, max = 26)
    @NotNull
    private String email; (unique)
```
------

- As a **PUBLISHER**, I should be able to add new book to the book list
  - **POST**
   
      http://127.0.0.1:8088/v1/publishers/{id}  id (1-13)


Request Body
```json
 {
  "genre": "TRAVEL",                                                
  "name": "bookName",  
  "pageCount": 150,
  "publishingYear": 2002
}

```
Validation
```java

    @NotBlank
    @NotNull
    @Size(min = 4)
    private String name;   (unique)

    @Min(value = 1940)
    @Max(value = 2022)
    private Integer publishingYear;

    @Min(value = 100)
    @Max(value = 800)
    private Integer pageCount;

    @NotNull
    private Genre genre;

}
```
-----

- As a **PUBLISHER**, I should be able update a specific book details that has been published by me publisher
  - **PUT**

      http://127.0.0.1:8088/v1/books/{bookId}/publishers/{publisherId}
   
      success case  (1-1, 2-2, 35-9)


Request Body
```json
{
  "genre": "PROGRAMMING",                                          
  "name": "bookName",
  "pageCount": 150,   
  "publishingYear": 2002
}       

```
Validation
```java

    @NotBlank
    @NotNull
    @Size(min = 4)
    private String name;   (unique)

    @Min(value = 1940)
    @Max(value = 2022)
    private Integer publishingYear;

    @Min(value = 100)
    @Max(value = 800)
    private Integer pageCount;

    @NotNull
    private Genre genre;

}
```
