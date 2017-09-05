# listener-chain
ListenerChain for TestNG

**Selenium Foundation** relies on **TestNG Foundation** for basic flow control. At the heart of it all is `ListenerChain`. To provide consistent behavior, we recommend that you activate `ListenerChain` via the **ServiceLoader** as described in the [TestNG documentation](http://testng.org/doc/documentation-main.html#listeners-service-loader "Specifying listeners with ServiceLoader"):

#### org.testng.ITestNGListener
```
com.nordstrom.automation.testng.ListenerChain
```
In a Maven project, the preceding file is stored in the `src/main/resources` package:

[![org.testng.ITestNGListener](src/main/resources/META-INF.png "org.testng.ITestNGListener")](src/main/resources/META-INF/services/org.testng.ITestNGListener)

Once this file is added to your project, `ListenerChain` will be loaded automatically whenever you run your tests. To link listeners into the chain, mark your test class with the <span style="color:blue">LinkedListeners</span> annotation:

###### LinkedListeners annotation
```java
package com.nordstrom.example;
 
import com.nordstrom.automation.selenium.listeners.DriverManager;
import com.nordstrom.automation.testng.ExecutionFlowController;
import com.nordstrom.automation.testng.LinkedListeners;
import com.nordstrom.automation.testng.ListenerChain;
 
@LinkedListeners({DriverManager.class, ExecutionFlowController.class})
public class ExampleTest {
     
    ...
  
}
```

As shown above, we use the **`@LinkedListeners`** annotation to attach <span style="color:blue">DriverManager</span> and <span style="color:blue">ExecutionFlowController</span>. The order in which listener methods are invoked is determined by the order in which listener objects are added to the chain. Listener _before_ methods are invoked in <span style="color:yellowgreen">last-added-first-called</span> order. Listener _after_ methods are invoked in <span style="color:yellowgreen">first-added-first-called</span> order. Only one instance of any given listener class will be included in the chain.
