---
sidebar_position: 1
---

# Methods
The different methods to use to make a quality request.

We will cover the different useful methods for creating a request with ConnectLib.

:::tip Tip

In this part we will not cover the use of MC_RESOURCES, it will be mentionned in another part.

:::

---

#1 We have three important methods: one that allows access to the code for performing the request, and two others that allow creating the request and receiving the data.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void listMethods() {

        /**
         * Here are some methods that can be used.
         * You can see all the methods in the javadoc.
         */

        /**
         * jobGetInfos allows access to the concerned class.
         */
        connectLib.JobGetInfos();

        /**
         * getRoutes allows you to specify the necessary information to build the request.
         */
        connectLib.JobGetInfos().getRoutes();
        
        /**
         * You can change the URL of the API here if you want to use another URL than the one in the config file.
         */
        connectLib.JobGetInfos().urlBranch();

        /**
         * execute allows you to make a request and retrieve the response data from the request.
         */
        connectLib.JobGetInfos().execute();
        
        /**
         * body(); method allows you to put a body in your request.
         */
        connectLib.JobGetInfos().body();

        /**
         * params(); method allows you to put params in your request.
         */
        connectLib.JobGetInfos().params();

        /**
         * query(); method allows you tu put query in your request.
         */
        connectLib.JobGetInfos().query();

        /**
         * The showLogs(); method allows you to display the ConnectLib logs during the request steps.
         * This method is created if you want to display the logs of a request.
         */
        connectLib.Logger().showLogs();
    }

}
```

---

In a request there are several parameters that we will learn step by step.

:::tip Tip

To continue, click below to go to the next page.

:::