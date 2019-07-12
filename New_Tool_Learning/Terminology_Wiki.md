## Terminology Wiki

### Ground Rules
* Would be great to follow definition -> own explanation -> example -> citation

### What is `RPC`
* Originated from distributed system
* Server A has `main` but wanted to do `Calculator.add()` but only Server B has `CalculatorImp` with `add()`
* It's not in the same RAM!
* Use `@Reference` 来获得一个代理，然后注入

* RPC 面向过程，Restful面向资源
* Register, Server, Client
  * Server 在 Register 注册服务
  * Client 在 注册中心获取服务信息
  * Client 调用 Server的服务
```java
Compute engine = new ComputeEngine();
Compute stub = (Compute) UnicastRemoteObject.exportObject(engine, 0); 
Registry registry = LocateRegistry.createRegistry(1099); //1099 is port
registry.bind(name, stub);

// Client
Registry registry = LocateRegistry.getRegistry("127.0.0.1", 1099);
Compute comp = (Compute) registry.lookup(name);
comp.executeTask(task);
```

https://www.zhihu.com/question/40609661