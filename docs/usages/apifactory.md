---
sidebar_position: 4
---

# ApiFactory.class
Differents method to retrieve data.

:::info Information

In a future part we will see how to declare ApiFactory, but for now we will only cover the methods to learn and understand how it works.

:::

---

Here is a presentation of all the ApiFactory methods and we will go into detail on each method, how it is used and why it is used.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();
    
    public void retrieveData() {
        try {

            /**
             * Here is an example of retrieving data from the request.
             * With ApiFactory();
             */
            ApiFactory apiFactory;

            apiFactory.getData("data");
            
            apiFactory.getSpecData("data", "value");
            
            apiFactory.display();
            
            apiFactory.getStatusCode();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

---

So we will look at getData();

Here is an example with a clear and precise explanation of this method.
The O Type field allows you to select a data category from the response.

Here is an example.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void getDataVoid() {

        /**
         * Here is an example of retrieving data from the request.
         * With ApiFactory();
         */

        try {

            ApiFactory apiFactory;

            apiFactory.getData("data")
            
            // msg: "example response",
            // err: false,
            // code: 200
            // data: {
            //        key1: "value",
            //        key2: "value2"
            // }
            
            // getData will then retrieve the content of the data category:
            
            //        key1: "value",
            //        key2: "value2"

        } catch (Exception e) {
            e.printStackTrace();
    }

}
```

---

The second method is getSpecData(O Type, K value);

It allows you to select a key from a category of the response.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void getDataVoid() {

        /**
         * Here is an example of retrieving data from the request.
         * With ApiFactory();
         */

        try {

            ApiFactory apiFactory;

            apiFactory.getSpecData("data", "key1");
            
            // msg: "example response",
            // err: false,
            // code: 200
            // data: {
            //        key1: "value",
            //        key2: "value2"
            // }
            
            // getSpecData will then retrieve the content of the key1 value:
            
            //        return "value",


        } catch (Exception e) {
            e.printStackTrace();
    }

}
```

---

The getDisplay method displays the raw response from the request response.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void getDataVoid() {

        /**
         * Here is an example of retrieving data from the request.
         * With ApiFactory();
         */

        try {

            ApiFactory apiFactory;

            apiFactory.getDisplay();
            
            // msg: "example response",
            // err: false,
            // code: 200
            // data: {
            //        key1: "value",
            //        key2: "value2"
            // }
            
            // getDisplay will then retrieve the response:
            
            // return :
            
            // msg: "example response",
            // err: false,
            // code: 200
            // data: {
            //        key1: "value",
            //        key2: "value2"
            // }       


        } catch (Exception e) {
            e.printStackTrace();
    }

}
```

---

The last method is getStatusCode, it allows you to retrieve the response code from the request.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void getDataVoid() {

        /**
         * Here is an example of retrieving data from the request.
         * With ApiFactory();
         */

        try {

            ApiFactory apiFactory;

            apiFactory.getStatusCode();
            
            // msg: "example response",
            // err: false,
            // code: 200
            // data: {
            //        key1: "value",
            //        key2: "value2"
            // }  
            
            // It will return the status code 
            
            // return 
            
            // 200


        } catch (Exception e) {
            e.printStackTrace();
    }

}
```

---

Now you know how to use the ApiFactory methods, we will learn how to make a complete request. Since ConnectLib makes asynchronous requests, the request is made on another Thread so we must retrieve it with a particular function, here's how to do it.

---

:::tip Tip

To continue, click below to go to the next page.

:::