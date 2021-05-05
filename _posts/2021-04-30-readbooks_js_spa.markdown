---
layout: post
title:      "ReadBooks JS SPA"
date:       2021-04-30 20:15:45 -0400
permalink:  readbooks_js_spa
---


**ReadBooks** is JavaScript single page application inspired by the requirement for my son who need to track his reading regularly. This application allows a user to add a book, with a title , image and remarks under three categories "To Read", "Reading" and "Finished". The Books may be viewed and/or deleted. The user can choose to view the books under a category.


Its been a humbling experience while working on developing ReadBooks , I have gained knowledge and fixed my mistakes, during the office hours . 


Looks like , I have just scratched the surface and found few gems to share:


**FRONTEND & BACKEND**
JavaScript lets us have access to data more quickly than a pure Ruby application, we have the ability to use the clarity of structure of object-orientation and RESTful routes in the backend while enhancing the user experience in the frontend. To communicate between the frontend and backend, JavaScript uses fetch requests.


```
class BookApi{

    static baseURL = "http://localhost:3000/books"
    
    static fetchBooks() {
        
        fetch(BookApi.baseURL)
        .then(response => response.json())
        .then(data => {
            data["data"].forEach(book => {
                    const newBook = new Book({id: book.id, ...book.attributes})
                    newBook.renderBook()
            });
           
                     
        })
    }
```


**Static methods** are useful ways to create utility methods for your data. If you have operation that you need do perform on a batch of data (say, find a particular book in an array), static methods are your go-to tool. Static methods  are called on the class but don't have access to individual objects, they are somewhat limited in their scope, but can be very powerful in the correct application. They are Class level methods and can not invoke on an instance .Often used in ‘utility’ classes: classes that encapsulate a set of related methods but dont need to be made into instances

```
static formHandler() {
         
        const title = document.querySelector("#input-title").value 
        const image_url = document.querySelector("#input-image").value
        const remarks = document.querySelector("#input-remarks").value
        const categoryId = parseInt(document.querySelector("#categories").value)
        
        BookApi.createBook(title, image_url, remarks, categoryId)
        
       
    }
```

A **constructor** enables you to provide any custom initialization that must be done before any other methods can be called on an instantiated object. It is used to initialize class properties when new instance is created. The constructor method is a special method of a class for creating and initializing an object of that class.

```
class Book {

    static all = []

    static list = document.querySelector("#List-of-Books")

    constructor(book){
        this.id = book.id
        this.title = book.title
        this.image_url = book.image_url
        this.remarks = book.remarks
        this.category_id = book.category_id

        Book.all.push(this)
    }

```




**Functions** are one of the most important parts of JavaScript. Its a way to group together related bits of code.
Function are objects which can be called or invoked multiple times. They can be treated as any other variable , can be stored in data structiure or can be passed as an argument to another function .To invoke a function, ( ) must be added, Functions must be declared before trying to call Parameters.


```
const form = document.querySelector("#create-book-form")
form.addEventListener("submit", handleFormSubmit)


function handleFormSubmit(e) {
    e.preventDefault()  
    BookApi.formHandler() 
    form.reset()       
}

```


**Events** are "something that happens", triggers call back function. JavaScript  has the ability to 'listen' for things that happen inside the browser like mouse click, key press, form submission. When JavaScript recognizes an event that applies to an"event handler" that has been setup, it will execute that handlers work, which is stored in a callback function.

Happy Reading !!


