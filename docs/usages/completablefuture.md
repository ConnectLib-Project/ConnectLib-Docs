---
sidebar_position: 5
---

# CompletableFuture;
The method that allows you to retrieve data from another Thread.

Here we move on to the part about how to declare ApiFactory to retrieve the data.

The first step is how to initialize ApiFactory with CompletableFuture.

Here is an example

```java
public class Example {

    public void initApiFactoryVoid() {
    
        /**
         * Here is an example of retrieving data from the request asynchronously.
         * With CompletableFuture<ApiFactory>();
         */
    
        CompletableFuture<ApiFactory> apiFactoryCompletableFuture;
    
    }

}
```

---

Now we will use the knowledge learned during the previous parts.
Now we have initialized ApiFactory asynchronously.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void initApiFactoryVoid() {
    
        /**
         * Here is an example of retrieving data from the request asynchronously.
         * With CompletableFuture<ApiFactory>();
         */
    
        CompletableFuture<ApiFactory> apiFactoryCompletableFuture = connectLib.JobGetInfos();
    
    }

}
```

---

Now that we know how to create a request and initialize ApiFactory, the most important thing is to retrieve the data.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void initApiFactoryVoid() {

        /**
         * Here is an example of retrieving data from the request asynchronously.
         * With CompletableFuture<ApiFactory>();
         */

        try {

            CompletableFuture<ApiFactory> apiFactoryCompletableFuture = connectLib.JobGetInfos()
                    .getRoutes(MethodType.GET, EnumExample.EXAMPLE)
                    .execute();
            
            
            // We must create a synchronous ApiFactory apiFactory instance
            // then initialize it with asynchronous apiFactory.

            // There are several methods to retrieve data from another
            // Thread but we will use "get();".
            
            ApiFactory apiFactory = apiFactoryCompletableFuture.get();
            
            // 0 Seconds
            apiFactory = apiFactoryCompletableFuture.get(0, TimeUnit.SECONDS);
            
            // 1 Seconds
            apiFactory = apiFactoryCompletableFuture.get(1000, TimeUnit.SECONDS);
            
            
            Differents Types : TimeUnit;
            
            TimeUnit.SECONDS;
            TimeUnit.MINUTES;
            TimeUnit.HOURS;
            TimeUnit.DAYS;
            TimeUnit.MILLISECONDS;
            TimeUnit.NANOSECONDS;
            TimeUnit.MICROSECONDS;

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

```
// There is either get(); empty without arguments or you can specify a
// Timeout according to the response speed of your request.
// By default, it's best to set a 2-second Timeout

// apiFactory = apiFactoryCompletableFuture.get(2000, TimeUnit.SECONDS);
```

---

After initializing ApiFactory with asynchronous ApiFactory, we can use our methods seen previously.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void initApiFactoryVoid() {

        /**
         * Here is an example of retrieving data from the request asynchronously.
         * With CompletableFuture<ApiFactory>();
         */

        try {

            CompletableFuture<ApiFactory> apiFactoryCompletableFuture = connectLib.JobGetInfos()
                    .getRoutes(MethodType.GET, EnumExample.EXAMPLE)
                    .execute();
            
            
            // We must create a synchronous ApiFactory apiFactory instance
            // then initialize it with asynchronous apiFactory.

            // There are several methods to retrieve data from another
            // Thread but we will use "get();".
            
            ApiFactory apiFactory = apiFactoryCompletableFuture.get(2000, TimeUnit.SECONDS);
            
            System.out.println(apiFactory.display());

            System.out.println(apiFactory.getStatusCode());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

---

Now you know how to create a request perfectly and retrieve the data from it.