# CST8915 Lab 3: Azure Web App and Azure Static Web Apps

**Student Name**: Xinyi Zhao
**Student ID**: 040953633
**Course**: CST8915 Full-stack Cloud-native Development
**Semester**: Winter 2026

---

## Demo Video

🎥 https://youtu.be/bO3Yg8l1lQw

---

## Link of Repo

- order-service:  https://github.com/XinyiZhao-cloud/order-service  
- product-service:  https://github.com/XinyiZhao-cloud/product-service-python  
- store-front:  https://github.com/XinyiZhao-cloud/store-front  


### What challenges did you encounter when configuring environment variables in the GitHub Actions workflow?

One major challenge I encountered was an environment variable mismatch between my Azure App Service configuration and the order-service code. The application originally expected RABBITMQ_CONNECTION_STRING, but in Azure, I had configured RABBITMQ_URL. Because of this mismatch, the service fell back to amqp://localhost, which caused HTTP 500 errors when placing orders. RabbitMQ showed no active connections, even though the VM and ports were correctly configured. I identified this issue by inspecting environment variables through Kudu and reviewing the application logs. I resolved it by modifying the code to support RABBITMQ_URL with a backward-compatible fallback and redeploying the service.

### How does deploying microservices on Azure Web App Service differ from running them locally?

When running the services locally, the configuration was straightforward because I used a .env file and localhost for service communication. Everything ran within the same environment, and debugging was immediate since logs were visible directly in the terminal. In Azure Web App Service, however, services run in isolated cloud environments and must communicate using public URLs or VM IP addresses. This introduced additional complexity, such as verifying network security rules, confirming that RabbitMQ ports were open, and ensuring that environment variables were correctly configured in the Azure portal.

Another difference was debugging visibility. When the order-service failed in Azure, the Log Stream did not immediately show detailed error information. I had to enable logging, inspect environment variables through Kudu, and test port connectivity from inside the container. Additionally, during a GitHub Actions re-run, I mistakenly opened the default domain while deployment was still in progress, which confused whether the failure was related to the configuration or the incomplete deployment. These experiences highlighted the operational differences between local development and cloud deployment.

### Why is it important to use environment variables for configurations in a cloud environment?

During this lab, I experienced firsthand why environment variables are essential in cloud deployments. When services moved from VMs to Azure Web App Service and Static Web Apps, hard-coded values such as localhost or fixed connection strings no longer worked. Using environment variables allowed the same application code to adapt to different deployment environments without modification, which aligns directly with the Twelve-Factor App principle of separating configuration from code.

Additionally, separating configuration from code improved flexibility and security. RabbitMQ credentials and service URLs were stored in Azure App Service settings rather than inside the repository. This approach makes the application more portable, more secure, and easier to maintain across different environments.

---

## Challenges and Learnings (Optional)

- 1. Frontend migration to Azure Static Web Apps  
After moving the store-front from a VM to Azure Static Web Apps, browser requests were initially blocked due to CORS restrictions. This required enabling CORS in the backend and injecting backend URLs through GitHub Actions during the build process. This helped me understand the difference between build-time and runtime configuration.  
- 2. Cloud debugging and environment validation   
When the order-service failed in Azure, Log Stream did not immediately show detailed errors. I used Kudu to inspect environment variables inside the running container and tested connectivity to RabbitMQ. This experience demonstrated how cloud debugging differs from local development and reinforced the importance of correct environment configuration.  

---

## Acknowledgments

## Acknowledgments

During troubleshooting, I consulted official documentation and used AI-assisted tools to better interpret error messages and explore potential causes. These tools helped guide my investigation of configuration issues related to environment variables and service connectivity. All implementation, deployment, and verification steps were performed and validated by me.
