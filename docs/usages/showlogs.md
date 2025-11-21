---
sidebar_position: 6
---

# showLogs();
Method allows you to display the ConnectLib logs during the request steps.

---

You can display the logs of a request this way.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void initApiFactoryVoid() {
    
        connectLib.Logger().showLogs();

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