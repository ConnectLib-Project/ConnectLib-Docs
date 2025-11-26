---
sidebar_position: 8
---

# AtomicFactory.class
Method allows you to make a custom Factory class from Physx of ApiFactory.class

---

## Make CustomFactory with AtomicFactory.class

Now we will see how make a custom Factory with AtomicFactory.

Here is an example

```java
public class ExampleFactory extends AtomicFactory {
    
    public ExampleFactory(ApiFactory apiFactory) {
        getPhysx(apiFactory);
    }
    
    // Here you can create your own methods to get specific informations from ApiFactory
    public Object getInfo() {
        return rawPhysx().get("info");
    }
    
    public Object getData() {
        return rawPhysx().get("data");
    }
    
}
```

Now you know how to make your own Factory Class. And then you need to import it when you create a request.

---

## Use CustomFactory with Request

Here is an example of how to use your CustomFactory with a Request

```java
public class Example {


    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();
    
    public void makeARequest() {
        try {
            connectLib.init(ResourceType.TEST_RESOURCES, LangType.ENGLISH, TestRoutes.class);

            // You need to change in CompletableFuture<YourCustomFactoryClass> 
            CompletableFuture<ExampleFactory> apiFactoryCompletableFuture = connectLib.JobGetInfos()
                    .getRoutes(MethodType.GET, TestRoutes.HELLO)
                    .execute()
                    
                    // Here you need to use thenApply to convert ApiFactory to YourCustomFactoryClass
                    .thenApply(ExampleFactory::new);
            
            ExampleFactory exampleFactory = apiFactoryCompletableFuture.get(5, TimeUnit.SECONDS);

            System.out.println("Response: " + exampleFactory.getInfo());
            System.out.println("Data: " + exampleFactory.getData());
            
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

And now you know how to make a request with your own CustomFactory Class using AtomicFactory.

---

:::tip Tip

To continue, click below to go to the next page.

:::