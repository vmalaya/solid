# I. Interface Segregation Principle

## Info
The principle was defined as:

“Clients should not be forced to depend upon interfaces that they do not use.”

The principle helps to reduce the side effects and frequency of required
changes by splitting the software into multiple, independent parts. So interfaces should be thin.

> ***NOTE***
>
>Violating the ISP also leads to violation of other principles like the Single Responsibility Principle.

**Code smells that indicate violation of the ISP:**
1. Unused dependencies (we should use as arg null or 0 to use this method).
2. Methods Throwing Exceptions.
## Pros 

1. Reusable code
2. Scalability
3. Easier maintenance, testing etc..

## Example 
**Violation**

We have an interface OrderService

````java
interface OrderService {
     void orderBurger(int quantity);
     void orderFries(int fries);
     void orderCombo(int quantity, int fries);
}
````

Also implementations like BurgerOrderService (the same for FriesOrderService, ComboOrderService except all methods are implemented as class name requires)

````java
class BurgerOrderService implements OrderService {
    @Override
    public void orderBurger(int quantity) {
        System.out.println("Received order of "+quantity+" burgers");
    }

    @Override
    public void orderFries(int fries) {
        throw new UnsupportedOperationException("No fries in burger only order");
    }

    @Override
    public void orderCombo(int quantity, int fries) {
        throw new UnsupportedOperationException("No combo in burger only order");
    }
}
````
 Obviously we have the ISP violation here: a lot of non-valuable code!
 
 TO FIX VIOLATION:
+ We can have additional separate interfaces
 ````java
 interface FriesOrderService {
      void orderFries(int fries);
 }
 ````
````java
 interface ComboOrderService {
      void orderCombo(int quantity, int fries);
 }
 ````
+ Use Adapter pattern
In case when we have an external dependency, we can use the adapter pattern to abstract away the unwanted methods.
It makes two incompatible interfaces compatible by using an adapter class.

Let’s say that OrderService is an external dependency that we can’t modify and needs to use to place an order.
We need to adapt OrderService to our target interface i.e. BurgerOrderService

````java
class OrderServiceObjectAdapter implements BurgerOrderService {
    private OrderService adaptee; // the reference to our dependency 
    public OrderServiceObjectAdapter(OrderService adaptee) {
        super();
        this.adaptee = adaptee;
    }

    @Override
    public void orderBurger(int quantity) {
        adaptee.orderBurger(quantity);
    }
}
 ````
Now when a client wants to use BurgerOrderService, we can use the OrderServiceObjectAdapter to wrap the external dependency:

````java
class Main{
    public static void main(String[] args){
        OrderService orderService = ...;
        BurgerOrderService burgerService = new OrderServiceObjectAdapter(new ComboOrderService());
        burgerService.orderBurger(4);
    }
}
 ````