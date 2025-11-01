---
sidebar_position: 2
---

# Initialisation

Here you can see the different ways to initialize your library

---

:::danger Danger

For information, it is necessary to create only one instance of ConnectLib.

It is possible to create a Getter to retrieve this same and only instance in other classes.

:::

```java 
public class Example {

    // Instance of ConnectLib
    private final static ConnectLib connectLib = new ConnectLib();


    // Getter of ConnectLib
    public ConnectLib connectLibInstance() {
        return connectLib;
    }
}
```

---

#1 This example is the simplet initialization without an enumeration class

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();

    public void initWithoutEnum() {

        /**
         * You can initialize the library without an enumeration;
         * the enumeration allows you to orchestrate the requests.
         * Without this option, you have to list them manually in infos.yml.
         */
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.ENGLISH);
    }

}
```

--- 

#2 Here you see the different types of resources possible for initializing the lib according to the purpose

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();
    
    public void initWithResources() {

        /**
         * There are three types of directories.
         *
         * MAIN RESOURCES
         * TEST RESOURCES and MC_RESOURCES
         */

        /**
         * MAIN_RESOURCES is used for production code.
         */
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.ENGLISH);

        /**
         * TEST_RESOURCES is used for test code.
         * Most for developers who want to test the library.
         */
        connectLib.Init(ResourceType.TEST_RESOURCES, LangType.ENGLISH);

        /**
         * MC_RESOURCES is used for Minecraft Mod/Plugin developers.
         * It contains specific methods for this type of project.
         */
        connectLib.Init(ResourceType.MC_RESOURCES, LangType.ENGLISH);
    }

}
```

---

#3 Following this, with LangType you can choose the preferred language with LangType.ENGLISH or LangType.FRENCH and many others currently unavailable.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();
    
    public void initWithLang() {

        /**
         * Following this, with LangType you can choose the preferred language.
         * LangType.ENGLISH or LangType.FRENCH and many others currently unavailable.
         */

        
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.ENGLISH);
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.FRENCH);
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.SPANISH);
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.GERMAN);
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.ITALIAN);
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.PORTUGUESE);
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.RUSSIAN);
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.CHINESE);
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.JAPANESE);
    }

}
```

--- 

:::tip Tip

Recommended method!

:::

#4 To initilize the library in the most optimized way possible, use an enumeration class. First, we will create an enumeration class and then add it to the line that initializes the library.

```java
public enum EnumExample implements RouteImport {

    /**
     * This is a route, you give a name to the route, for example "Example"
     * and between the quotes you put the logical route, example:
     *
     * localhost:8080/api -/example-
     * What is between the dashes is the route that must be specified between the quotes.
     *
     * Between braces it's a parameter and between $ it's a query.
     * For the body it's another way that we will see later.
     */

    EXAMPLE("/example"),
    HELLO("/hello"),
    WORLD("/world{args}"),
    GREET("/greet$query$"),
    ;

    private final String route;

    EnumExample(String route) {
        this.route = route;
    }

    @Override
    public String getRoute() {
        return route;
    }
}

```

Now we will add the enumeration class to the initialization line.

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();
    
    public void initWithEnum() {

        /**
         * You can initialize the library with an enumeration;
         * the enumeration allows you to orchestrate the requests.
         * 
         * By specifying EnumExample.class, 
         * it will then register the existing routes from the enumeration in the infos.yml file.
         */
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.ENGLISH, EnumExample.class);
    }

}
```

--- 

:::tip Tip

Now you know how to initialize the library perfectly.

:::

--- 

## Settings...

After learning how to initialize the library, you must configure the lib before being able to use it.

```
If you selected MAIN_RESOURCES, the infos.yml file is located in "src/main/data"
If you selected TEST_RESOURCES, the infos.yml file is located in "src/test/resources"

If you selected MC_RESOURCES, the infos.yml file is located in your plugin folder "namePlugin/data/infos.yml"
```

Here is an example infos.yml and what need to be modified. (Before have it, you need to start your project to generate the infos.yml file)

```
# properties ConnectLib By Sandro642

# You need to change the urlPath to communicate with your Rest API
urlPath: "http://localhost:8080/api"

routes:
  #info: "/info/version"
  #ping: "/ping"
  #status: "/status"

  #Here are the routes that we specified in the enumeration class.
  greet: "/greet$query$"
  hello: "/hello"
  example: "/example"
  world: "/world{args}"


# Logs
enableLogs: true # The enableLogs boolean allows you to create a .log file that explains the error in detail if you encountered an error.

```

---

You can now use the Web Implementation Service of ConnectLib to see a lot of informations about ConnectLib and your requests.

Here is an example of the Web Implementation Service:

```java
public class Example {

    /**
     * Instance of ConnectLib
     */
    private final static ConnectLib connectLib = new ConnectLib();
    
    public void initWithEnum() {

        /**
         * You can initialize the library with an enumeration;
         * the enumeration allows you to orchestrate the requests.
         * 
         * By specifying EnumExample.class, 
         * it will then register the existing routes from the enumeration in the infos.yml file.
         * 
         * The webServices(); method enables the Web Implementation Service.
         */
        connectLib.Init(ResourceType.MAIN_RESOURCES, LangType.ENGLISH, EnumExample.class)
                .webServices(); // Enable the Web Implementation Service
    }

}
```

---

## Some screenshots of the Web Implementation Service

<div style={{ textAlign: 'center' }}>
  <img
    src="/img/connectlibdash.jpeg"
    alt="ConnectLib dashboard"
    style={{ borderRadius: 12, maxWidth: '90%', height: 'auto' }}
  />
</div>

<br/>

<div style={{ textAlign: 'center' }}>
  <img
    src="/img/connectlibdash-2.jpeg"
    alt="ConnectLib dashboard"
    style={{ borderRadius: 12, maxWidth: '90%', height: 'auto' }}
  />
</div>

<br/>

<div style={{ textAlign: 'center' }}>
  <img
    src="/img/connectlibdash-3.jpeg"
    alt="ConnectLib dashboard"
    style={{ borderRadius: 12, maxWidth: '90%', height: 'auto' }}
  />
</div>

