---
sidebar_position: 3
---

# urlBranch(); Method
You can change the URL of the API here if you want to use another URL than the one in the config file.

Since version **_0.3.8-STABLE_**, it is possible to specify multiple endpoints (URLPath) by first creating an enumeration class and then implementing UrlProvider.

Then specify it using urlBranch();

```java
public class Example {

    /**
     * Example of URL branches, you can add multiple branches if you have multiple environments (dev, prod, etc.)
     */
    public enum ExampleUrlBranch implements URLProvider {
        LOCALHOST("http://localhost:8080"),
        PROD("https://prod-api.connectlib.xyz"),
        ;

        private final String url;

        ExampleUrlBranch(String url) {
            this.url = url;
        }

        @Override
        public String getURL() {
            return url;
        }
    }

}
```

After that

:::warning Warning 

For information, it is not mandatory to call urlBranch if you don't have any other endpoints.

:::

```java
public class Example {

    public void ExampleUrlBranch() {
        connectLib.Init(ResourceType.TEST_RESOURCES, LangType.ENGLISH, TestRoutes.class);

        connectLib.Logger().showLogs();

        try {
            CompletableFuture<ApiFactory> factoryCompletableFuture = connectLib.JobGetInfos()
                    .getRoutes(MethodType.GET, TestRoutes.HELLO)

                    /**
                     * You can change the URL of the API here if you want to use another URL than the one in the config file.
                     */
                    .urlBranch(ExampleUrlBranch.LOCALHOST)
                    
                    // Or
                    
                    .urlBranch(ExampleUrlBranch.PROD)
                    
                    .execute();

            ApiFactory response = factoryCompletableFuture.get(5, TimeUnit.SECONDS);

            System.out.println("Response: " + response.display());
            System.out.println("Status Code: " + response.getStatusCode());

        } catch (Exception e) {
            e.printStackTrace();
        }
    
}
```

