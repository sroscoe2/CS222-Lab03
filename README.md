# Programming II

## Lab 3.0 - Classes & Constructors

An introduction to using classes and constructors in the Java programming language.

This is a lab assignment based on one used in Computer Science II (CSCE 156 & 156H) in the School of Computing
at the University of Nebraska-Lincoln. 
Originally written by Chris Bourke. Revised and modified by Sarah Roscoe for CS222 at [Saint Mary's College of California](https://www.stmarys-ca.edu/) in Fall 2024. 

## Overview

### Resources

Prior to lab you should read/review the following resources.

-   Java constructor tutorial:  
    https://docs.oracle.com/javase/tutorial/java/javaOO/constructors.html

-   Object Creation tutorial:  
    http://download.oracle.com/javase/tutorial/java/javaOO/objectcreation.html


### Lab Objectives & Topics

Following the lab, you should be able to:

-   Use Classes and objects to write Java programs

-   Understand and use constructors

-   Understand the visibility of a class's methods and how to use them


### Pair Programming

You may work on this lab with a partner. You may work on one piece of code, but both of you should submit the work. You may send your partner a copy of the file and therefore turn in identical copies. You should also indicate on Canvas who you worked with. **Both of you should indicate your partner in a submission comment**. 

In pair programming, one person is the *driver* and the other is the *navigator*. The driver is responsible for the computer keyboard and mouse. The navigator is responsible for figuring out what should be done, and telling the driver what to do. Neither role is "in charge", but both are responsible for coming up with solutions together. 

Each week, you should try to alternate: if you were the driver last week, you should be navigator this week, or vice versa. Any conflicts should be resolved in your group. 


## 1. Getting Started

Clone this project code for this lab from GitHub in VS Code using the
URL: https://github.com/sroscoe2/CS222-Lab03.git. Refer to Lab 1.0 for
instructions on how to clone a project from GitHub.

## 2. Classes & Constructors 

Java is a class-based Object Oriented Programming Language meaning that
it realizes the concept of objects by allowing you to define classes
which have member methods and variables. Instances of classes are
*instantiated* through a constructor; a method with the same name as a
class and called using the keyword `new`. This lab will familiarize you with
how classes and their constructors are defined and used. In addition,
you will be introduced to some ways that Java supports other Object
Oriented Principles: Encapsulation and Abstraction.

-   *Encapsulation* is a mechanism by which objects group data and the
    methods/functions that act on that data. It is also the means by
    which a class's data is protected from the outside world (outside of
    the object). Java achieves this by allowing you to define member
    methods and variables and to specify the visibility of these fields
    using the keywords `private`, `protected`, and `public`.

-   *Abstraction* refers to the means by which an object exposes a
    public interface to the outside world while hiding the inner
    workings (the internal representation or the implementation
    details). Java's main mechanism for supporting this is the same as
    with encapsulation though it does provide other means (interfaces,
    abstract classes, etc.).

-   *Class Signaling* refers to invoking methods on an instance of a
    class. Java uses the dot (or period) operator to signal a class.

## 3. Activities 

We have provided a Java project that simulates a library collections
system. It has several classes already defined to model authors, books,
a library (a collection of books) and a text-based interface which
allows you to search the collection, add books to the collection, and
list the collection.

### 3.1 Creating Constructors

1.  Run the library program to familiarize yourself with its
    functionality. Note that printing the collection is not fully
    operational

2.  Complete each of the accessor (getter) methods in the `Book` class. Best
    Practice Tip: always use the `this` keyword to disambiguate the scope of
    variables and prevent potential problems when subclassing.

3.  Observe that the `Book` class does not have a constructor defined. Examine
    the `addBook()` code and determine how it is possible to create instances 
    of the `Book` class without a constructor.

4.  Modify the `Book` class by adding and implementing the following
    constructor.  

    ```java
    public Book(String title, Author author, String isbn, String publishDate) {
      //TODO: your code here
    }
    ```

5.  Adding this constructor will cause syntax errors in other parts of
    the program. Think about why and then fix these problems by
    modifying the code appropriately.

### 3.2 Enforcing Good Encapsulation

The `Book` class is well-designed: it logically groups data and methods
together that semantically define what a book is and how you can use it.
The `Author` class however, is not well-designed.  Its data members are publicly
exposed and it has no methods at all.

1.  Redesign the `Author` class and make its member variables private.

2.  Create and use getter methods to make the members accessible to the
    outside world. Use these methods where appropriate.

3.  Create setter methods (also called mutator methods) to enable code
    outside of the `Author` class to change the member variables. Add some data
    validation: for example, do not allow "invalid" values for member
    variables.

4.  Add and make use of an appropriate constructor to this class.

5.  Add a method to return a `String` that is the author's last name/first name
    separated by a comma and then utilize it where appropriate (modify
    the `printBooks()` method to use this new method instead of formatting the last
    name/first name directly).

### 3.3 Adding and Using Methods 

The `printBooks()` method prints out the title, author, and ISBN in a formatted manner
one per line. In this activity, you will modify it to output additional
information: the year of its publication and its age (the number of
years since its publication date).

1.  Modify the `printBooks()` method in the `LibraryDemo` class to output 
    the publication year of each book in another column. Note that the `Book`
    class has a `getPublishDate()` method already implemented for you.

2.  To add the "age" column, you will need to add code (*somewhere*) to compute
    the number of years between the publish date and today.  Well-designed
    encapsulation means that code that operates on the data of a class belongs
    *inside the class*.  Bad encapsulation would mean you locate this code
    *outside the class*.  
    
    For example: you *could* write code in the `printBooks()` method that 
    extracted the publish date from the class and calculated the age.  This
    would be an example of *bad encapsulation* as it locates code acting on 
    a class's data (`publishDate`) outside the class.  
    
    Instead, do this correctly using *good encapsulation* by adding a new
    method to the `Book` class that returns the number of years between the 
    publish date and today. Name your method `getAge()`.  You may find the following code 
    snippet useful (it utilizes the date/time library provided by Java 8):  
    
    `int years = Period.between(this.publishDate, LocalDate.now()).getYears();`

## 4. Testing, Submitting & Grading

* Test your programs using the provided JUnit test suite(s).  Fix any
errors and completely debug your programs.
* Compress your Lab 03 project to a zip file and name it `CS222-Lab03smc1` where `smc1` is YOUR SMC username.
* Submit the zip file to Canvas.

  
### Advanced Activity (Optional) 

1.  The `printBooks()` method prints books in the order in which they appear in the
    list. This isn't as useful as if they were sorted in some manner.
    Read Oracle's tutorial on Object ordering,
    <http://docs.oracle.com/javase/tutorial/collections/interfaces/order.html>.
    Write code to use the `Collections.sort()` method along with an anonymous 
    `Comparator<Book>` instance to sort the collection according to the book's title.

2.  Composition is when a class owns instance(s) of other classes (the
    `Book` class owns an instance of the `Author` class). If different 
    instances of a class, say *A* and *B* are given references to the 
    same object $C$, and changes are made to $C$, the changes will be 
    apparent to both *A* and *B*. Sometimes this behavior is desired. 
    Sometimes it is not.  One common technique to prevent this is to define 
    a *copy constructor* which takes an instance of the class and performs a
    *deep copy* of an object by copying each of its fields to the new
    instance. For example, the copy constructor for the `Author` class may look
    something like this:  

    ```java
    public Author(Author author) {
      this.firstName = new String(author.firstName);
      this.lastName = new String(author.lastName);
    }
    ```

    Design and implement a copy constructor for the `Book` class and the 
    `Library` class. How do different fields need to be copied?
