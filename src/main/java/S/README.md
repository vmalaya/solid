# S. Single responsibility principle

## Info

 The principle states that a class should only have one responsibility. So it should only have _*one reason*_ to change.

> **_NOTE:_** 
> This principle not only to separate, but to gather together as well.
>
> **Separate** those things that change for different reasons
>
> **Gather** together the things that change for the same reasons.
>
> Please use YAGNI to understand what you need 

## Pros 

Testing -> Easy to test class with one responsibility

Lower coupling -> Class will have fewer dependencies

## Example 

We have a class Book

````java
public class Book {
 
    private String name;
    private String author;
    private String text;
 
    public boolean isWordInText(String word){
        return text.contains(word);
    }

    public void printTextToConsole(){
        // our code for formatting and printing the text
    }
}
````
The method 'printTextToConsole()' violates the single responsibility principle, so to fix it a separate class should be implemented:

````java
public class BookPrinter {
 
    void printTextToConsole(String text){
        //our code for formatting and printing the text
    }
}
````
 