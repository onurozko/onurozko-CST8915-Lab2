# CST8915 Lab 2

**Student Name:** Tahir Onur Ozkoral  
**Student ID:** 041122154

**Course:** CST8915 Full-stack Cloud-native Development  
**Semester:** Fall 2026  

---

## Demo Video

[Watch Demo Video](https://youtu.be/0MNMGoclkIA)

## Service Repositories

- [Order Service](https://github.com/onurozko/order-service)
- [Product Service](https://github.com/onurozko/product-service)
- [Store Front](https://github.com/onurozko/store-front)

## Reflection Questions

### 1. What changes did you make to the order-service and product-service to comply with the Configurations and Backing Services factors of the 12-Factor App methodology?

For the order-service, I moved the RabbitMQ connection string and the service port into environment variables instead of keeping them directly in the code. I also used dotenv so the application can load these values from a local .env file. For the product-service, I moved the port configuration into an environment variable and added the dotenv dependency in Cargo. RabbitMQ was also treated as an external backing service that the order-service connects to through configuration rather than being tightly coupled to the application.

### 2. Why is it important to use environment variables instead of hard-coding configurations in your application?

It is much easier to change environment variables when configuration needs to change, and we can also use things like GitHub Secrets for sensitive values. When I first started development, avoiding hard-coded configuration was one of the first things my seniors told me about. After dealing with different environments, deployments, and emergency changes, I personally understood why it is important as well.

### 3. Why is it important to have separate repositories for each microservice? How does this help maintain independence and scalability of each service?

It allows different teams to work on different services simultaneously and independently. Each service can also be updated, tested, deployed, or scaled without directly affecting the others, which makes the overall system easier to maintain.

## Deployment Note

The original lab architecture uses four separate Azure VMs. My Azure for Students subscription was limited to three public IP addresses and six regional vCPUs. Following the instructor's guidance, RabbitMQ was installed on the same VM as the Product Service. The Store Front and Order Service remained on their own separate VMs.

The final deployment used:

- Store Front VM
- Order Service VM
- Product Service + RabbitMQ VM

The full application flow was tested successfully, including loading products, placing an order, and confirming that the RabbitMQ queue message count increased.
