# O. Open/Closed principle

## Info

 Classes should be open for extension, but closed for modification.
 
 That's why we shouldn't modify existing code. 
 
 To apply this principle you can use:
 - Class Inheritance (Ok)
 - Decorator Pattern (it is the best solution):  The Decorator Pattern acts as a wrapper around our existing entity,
  and implementing the additional properties and methods within it.

## Pros

- No potential new bugs in existing already tested code

## Example

We have a class Book

````java
public class Book {
 
    private String name;
    private String author;
    private String text;

}
````
We want to make a Book with custom cover. It might be tempting to just open up the Book class and add a custom cover – but who knows what errors that might throw up in our application.

Instead, let's stick to the open-closed principle and simply extend our Book class:
````java
public class BookWithCustomCover extends Book {
 
    private String customCover;
}
````
