## Started services
1. Run Eureka server: 
    ```bash
    ./gradlew :registration:bootRun
    ```
   ![registration](https://user-images.githubusercontent.com/45805074/147889906-421265b1-868e-461b-9fa3-a5d301aff16e.png)
2. Run account service and register on Eureka server
   ```bash
   ./gradlew :accounts:bootRun
   ```
   ![accounts](https://user-images.githubusercontent.com/45805074/147889985-51e0ea78-7070-449e-9ffb-868347dc7453.png)
3. Run web service and register on Eureka server
   ```bash
   ./gradlew :web:bootRun
   ```
   ![web](https://user-images.githubusercontent.com/45805074/147890020-c9f6b2aa-6907-4ba0-bbb3-4a0bd5da9ba6.png)

## Registered services dashboard
In the below image we can see two registered services:
- account service running on 2222 port
- web service running on 3333 port.  

![dashboard](https://user-images.githubusercontent.com/45805074/147890096-e0dc7fbb-770c-4063-9b4b-8710afd858fd.png)

## Second account service
We must first change the account service default port in ``/src/main/resources/application.yml`` file  
to 4444. This will avoid a conflict with the currently account service running.
After that, we can run the second account service and register on Eureka server.
![accounts2](https://user-images.githubusercontent.com/45805074/147890279-bb9f93a5-e177-47cb-b3eb-fb44939eb973.png)

The dashboard has been updated too and we can see this new service registered:  
![dashboard2](https://user-images.githubusercontent.com/45805074/147890316-e93965d1-a67b-4fc8-82e9-234eb84d994e.png)

## Kill first account service and request to web
When I kill the first account service I can observe that 
this service (port:2222) has dissapear from dashboard:
![dashboard3](https://user-images.githubusercontent.com/45805074/147890344-477578f8-b25b-4e3c-ab06-33b1d69d10cb.png)  

When I access to the account service through web service I can see
a successful html web.
![finalResult](https://user-images.githubusercontent.com/45805074/147890378-bffa9161-46d3-4576-b6dc-c86b30a74e98.png)  

This happends because web service asks to Eureka server about the real location of the logical URI ``https://ACCOUNTS-SERVICE``.  
After that, Eureka server responses with the real location of the second 
accounts service and now web service is able to ask to the second accounts service.
