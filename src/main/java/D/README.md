# D. Dependency Inversion Principle

## Info
The principle states that:

1. High-level modules should not depend on low-level modules. Both should depend on abstractions.
2. Abstractions should not depend on details. Details should depend on abstractions.

## Pros

1. Flexibility
2. Low coupling

## Example 
**Violation**

Given

````java
public class BackEndDev {
     public void writeJava();
}
````
````java
public class FrontEndDev {
     public void writeJavaScript();
}
````
When

````java
public class Project {
    private BackEndDev backEndDev = new BackEndDev();
    private FrontEndDev frontEndDev = new FrontEndDev();
    public void implement() {
        backEndDev.writeJava();
        backEndDev.writeJavaScript();
    };
}
````
It is a violation the DIP due to:
1. High-level module Project depends on low-level modules FrontEndDev and BackEndDev.
2. Also, by inspecting the implement function of Project.class,
we realize that the methods writeJava and writeJavascript are methods bound to the corresponding classes.
Regarding the project scope, those are details since, in both cases, they are forms of development.

**TO FIX VIOLATION**

````java
public interface Developer {
    void develop();
}
````
````java
public class BackEndDev implements Developer{

    @Override
    void develop(){
        writeJava();
    }

    private void writeJava();
}
````
````java
public class FrontEndDev implements Developer{
    @Override
    void develop(){
        writeJavaScript();
    }

    private void writeJavaScript();
}
````
````java
import java.util.List;
public class Project {
    private List<Developer> devs;

    public Project(List<Developer> devs){
        this.devs = devs;
    }
    public void implement() {
        devs.forEach(d -> d.develop());
    };
}
````
