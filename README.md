# CST8915 – Lab 4 Submission (Full-stack Cloud-native Development)

## Student
- Name: Ilyas Zazai
- Course: CST8915 – Full-stack Cloud-native Development
- Lab: Lab 4

---

## Demo Video
- 

---

## GitHub Repositories
- Order Service (Node.js): https://github.com/Ilyzazai/order-service
- Product Service (Python FastAPI): https://github.com/Ilyzazai/product-service
- Store Front (Vue): https://github.com/Ilyzazai/store-front

---

## Live Azure URLs
### Order Service (Azure App Service)
- https://ilyas-order-service-d9fmb3eefrbfdydt.eastus-01.azurewebsites.net

### Product Service (Azure App Service)
- https://ilyaswebsite-hggsc8ejfeafdndr.eastus-01.azurewebsites.net

### Store Front (Azure Static Web Apps)
- https://delightful-rock-01cad6e1e.1.azurestaticapps.net

---

## Architecture Overview
This lab deploys a simple full-stack microservices application:

- **store-front (Vue)** is deployed to **Azure Static Web Apps**
- **order-service (Node.js)** is deployed to **Azure App Service**
  - publishes order messages to RabbitMQ
- **product-service (Python FastAPI)** is deployed to **Azure App Service**
  - returns product list via HTTP API
- **RabbitMQ** runs on an **Azure VM** and is accessed on:
  - `5672` (AMQP – required for apps)
  - `15672` (Management UI – optional)

---

## Configuration (Environment Variables)

### Order Service (Azure App Service)
Added in Azure Portal → App Service → **Environment variables** → **Application settings**:

- `RABBITMQ_CONNECTION_STRING=amqp://guest:guest@<RABBITMQ_VM_PUBLIC_IP>:5672/`

### Store Front (Build-time env)
Configured to call the deployed APIs (either in `.env.production` or GitHub Actions build env):

- `VUE_APP_ORDER_SERVICE_URL=https://ilyas-order-service-d9fmb3eefrbfdydt.eastus-01.azurewebsites.net`
- `VUE_APP_PRODUCT_SERVICE_URL=https://ilyaswebsite-hggsc8ejfeafdndr.eastus-01.azurewebsites.net`

---

## API Endpoints Used

### Product Service
- `GET /products`
  - returns a JSON list of products

### Order Service
- `POST /orders`
  - publishes an order message to RabbitMQ (`order_queue`)

---

## How to Run / Test (End-to-End)
1. Start the RabbitMQ VM in Azure.
2. Confirm RabbitMQ container is running:
   - `sudo docker ps`
3. Confirm VM NSG inbound rules allow:
   - TCP `5672` (required)
   - TCP `15672` (optional dashboard)
4. Ensure `RABBITMQ_CONNECTION_STRING` is set in the **order-service** App Service.
5. Open the Store Front URL and confirm:
   - Products load successfully from product-service
   - Placing an order calls order-service successfully
6. (Optional) Open RabbitMQ UI:
   - `http://<RABBITMQ_VM_PUBLIC_IP>:15672` (guest/guest)
   - verify queue/messages activity

---

## Notes / Reflection
- The main deployment steps were:
  - Deploy both APIs on Azure App Service
  - Deploy UI on Azure Static Web Apps
  - Use environment variables to connect services
  - Verify messaging integration through RabbitMQ
    
*AI is used for product services-service code and .md documentation*
