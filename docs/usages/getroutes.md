---
sidebar_position: 2
---

# getRoutes(); Method
Differents Types.

As the first parameter we have VersionType. We can either use the enumeration class offering 5 versions or use a character string, here are the two examples

The versionType allows you to avoid making reading complicated and manage your requests if you have a large project, which makes it easier to navigate.

Your REST API must integrate versions into its route.

:::warning Warning

For information, if you don't have a route with a versionType, you are not required to specify a versionType.

:::

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();
    
    public void makeFirstRequest() {
        try {

            /**
             * Here is an example of a request.
             * In this case we are requesting the V1_BRANCH version.
             * The route is /example as specified in the enumeration.
             *
             * The full URL will be:
             * localhost:8080/api/v1 -/example-
             *
             * The response will be a String.
             */
            connectLib.JobGetInfos()
                    .getRoutes(VersionType.V1_BRANCH)
                    .getRoutes(VersionType.V2_BRANCH)
                    .getRoutes(VersionType.V3_BRANCH)
                    .getRoutes(VersionType.V4_BRANCH)
                    .getRoutes(VersionType.V5_BRANCH);
            
            /**
             * You can also specify the version as a String.
             * In this case "v1" is specified.
             */
            connectLib.JobGetInfos()
                    .getRoutes("v1");
            
            
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

---

Since version **_0.3.6-STABLE_**, we can now use a CustomVersionType

First, you need to create an enumeration class.

Since version **_0.3.6-STABLE_**, getRoutes has been modified and now uses a VersionProvider which is an interface.

Here's an example.

```java
public enum VersionExample implements VersionProvider {

    /**
     * This is an example of how to use custom versions.
     * You can create your own enum that implements VersionProvider
     * and add your versions there.
     */

    ALPHA_BRANCH("alpha"),
    V2("v2"),
    DEV_BRANCH("dev"),
    ;

    private final String version;

    VersionExample(String version) {
        this.version = version;
    }

    @Override
    public String getVersion() {
        return version;
    }
}
```

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();
    
    public void useCustomVersion() {

        /**
         * You can use custom versions like this:
         * For example, if you want to use the alpha version of v2, you can.
         */
        connectLib.JobGetInfos()
                .getRoutes(VersionExample.ALPHA_BRANCH)
                .getRoutes(VersionExample.V2)
                .getRoutes(VersionExample.DEV_BRANCH)
    }

}
```

--- 

As the second parameter is the MethodType, it is available as a character string and also as an Enumeration, but it is recommended to use the enumeration unless your REST API supports methods not supported by the library.

Here is an example.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void makeFirstRequest() {

        /**
         * Here is an example of a request.
         * The request can be made with methodType as a string or as an enum.
         * 
         * You can also use MethodType.GET, MethodType.POST, MethodType.PUT, MethodType.DELETE, MethodType.PATCH
         */
        try {

            connectLib.JobGetInfos()
                    .getRoutes("version", "get")

                    .getRoutes("version", MethodType.GET)
                    .getRoutes("version", MethodType.POST)
                    .getRoutes("version", MethodType.PUT)
                    .getRoutes("version", MethodType.DELETE)
                    .getRoutes("version", MethodType.PATCH)


        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

---

The third parameter you have is routeName, it is available with a character string, but if you remember we created an enumeration class that allows us to orchestrate our routes specified beforehand. So we can use this enumeration and specify the route.

Here is an example.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void makeFirstRequest() {

        /**
         * Here is an example of a request.
         * This example uses the enumeration to specify the route.
         * You can also specify the route directly as a string.
         */
        try {

            connectLib.JobGetInfos()
                    .getRoutes("version", "get", "hello")
                    .getRoutes("version", MethodType.GET, EnumExample.HELLO)


        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

---

The fourth parameter is the Body parameter, this parameter requires a Map.
I must specify my body value according to the requested key.

Here is an example.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void makeFirstRequest() {

        /**
         * Here is an example of a request.
         * 
         * You need to use a Map to specify the body of the request.
         * If there is no body, you can put null.
         */
        try {

            Map<String, Object> body = Map.of(
                    "key", "value"
            );
            
            connectLib.JobGetInfos()
                    .getRoutes(VersionType.V1_BRANCH, MethodType.GET, EnumExample.EXAMPLE)
                    .body(body);


        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

---

:::warning Warning

For information, if in your route you only want to specify a params or a query, you can put null for the desired argument.

:::

The fifth argument is the params, this argument requires a Map. Same principle as the body but these are parameters in the route, if you remember in the enumeration class the route with a parameter between braces, that's the params.

Here is an example.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void makeFirstRequest() {

        /**
         * Here is an example of a request.
         *
         * You need to use a Map to specify the params of the request.
         * If there is no params, you can put null.
         */
        try {

            Map<String, Object> params = Map.of(
                    "key", "value"
            );

            connectLib.JobGetInfos()
                    .getRoutes(VersionType.V1_BRANCH, MethodType.GET, EnumExample.EXAMPLE)
                    .params(params);


        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

---

The sixth argument is the query, this argument requires a Map. Same principle as the body but these are parameters in the route, if you remember in the enumeration class the route with a parameter between dollar signs ($), that's the query.

Here is an example.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void makeFirstRequest() {

        /**
         * Here is an example of a request.
         *
         * You need to use a Map to specify the query of the request.
         * If there is no query, you can put null.
         */
        try {

            Map<String, Object> query = Map.of(
                    "key", "value"
            );

            connectLib.JobGetInfos()
                    .getRoutes(VersionType.V1_BRANCH, MethodType.GET, EnumExample.EXAMPLE, null, null)
                    .query(query);


        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

---

Now you know how to use getRoutes() but the most important thing is getResponse();

Here is an example of a working request.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void makeFirstRequest() {

        /**
         * Here is an example of a request.
         * With getResponse();
         */
        try {

            Map<String, Object> body = Map.of(
                    "key", "value"
            );

            Map<String, Object> params = Map.of(
                    "key", "value"
            );

            Map<String, Object> query = Map.of(
                    "key", "value"
            );

            connectLib.JobGetInfos()
                    .getRoutes(VersionType.V1_BRANCH, MethodType.GET, EnumExample.EXAMPLE)
                    .body(body)
                    .params(params)
                    .query(query)
                    .execute();
                    
                    // getResponse(); allows you to send the request and retrieve the response data for the next step, 
                    // parsing the data.
                    
                    
            // Without VersionType        
            connectLib.JobGetInfos()
                    .getRoutes(MethodType.GET, EnumExample.EXAMPLE)
                    .body(body)
                    .params(params)
                    .query(query)
                    .execute();    


        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

---

:::tip Tip

To continue, click below to go to the next page.

:::