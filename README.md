## fox
[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.svg?v=102)](https://github.com/wenbo2018/fox/)


fox is a distributed, lightweight RPC framework which empowers applications with service import/export capabilities.

It contains three key parts, which include:

* **Remoting**: a network communication framework providing request-response messaging.

* **Registration**: a service directory framework for service registration and service event publish/subscription



## Quick Config
You only need to configure your zookeeper address in the appkeys file;

appkeys file address:

/data/app/appkeys.properties(Linux)

C:/data/app/appkeys.properties(WIN)

**Configuration format**:

```xml
fox.registry.adress="zk server ip"

fox.registry.type=zookeeper

fox.registry.ip="your rpc server ip"

```

## Quick Start
when you need invoke service ,you can just do as following:

```xml
         <bean id="helloService" class="ServiceProxy" init-method="init">
            <property name="iface" value="com.dianping.HelloService"/>
            <property name="serviceName" value="service.fox.com_helloTestService_helloService_1.0.0"/>
            <property name="serializer" value="protostuff"/>
         </bean>

```
or use spring schemas
```xml
    <fox:invoker id="helloService"
            iface="HelloService"
            serviceName="service.fox.com_helloTestService_helloService_1.0.0"
            serializer="hessian"/>
```

```xml
         <bean id="helloService" class="ServiceProxy" init-method="init">
            <property name="iface" value="com.dianping.HelloService"/>
            <property name="serviceName" value="service.fox.com_helloTestService_helloService_1.0.0"/>
            <property name="serializer" value="protostuff"/>
         </bean>

```

when you publish your services,you can just do as following:

```xml
        <bean id="helloService" class="com.dianping.HelloServiceImpl"/>

        <bean id="helloTestService" class="ServiceRegister" init-method="init">
            <property name="port" value="4080"/>
            <property name="services" >
                <map>
                    <entry key="service.fox.com_helloTestService_helloService_1.0.0" value-ref="helloService"/>
                </map>
            </property>
        </bean>
```
or use spring schemas

```xml
    <fox:server  id="server1" port="4019"/>
    <fox:service server="server1"
                 serviceName="service.fox.com_helloTestService_helloService_1.0.0"
                 ref="helloService"/>
    <fox:service server="server1"
                 serviceName="service.fox.com_helloTestService_userService_1.0.0"
                 ref="userService"/>
```

This framework refers to the design of Piegon,Dubbo,Motan

