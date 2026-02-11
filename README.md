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

## Technical Explanations

### What challenges did you encounter when configuring environment variables in the GitHub Actions workflow?


[Your explanation here - 1-2 paragraphs]

### How does deploying microservices on Azure Web App Service differ from running them locally?

[Your explanation here - 1-2 paragraphs]

### Why is it important to use environment variables for configurations in a cloud environment?

[Your explanation here - 1-2 paragraphs]


---

## Challenges and Learnings (Optional)

1. Store-front moved from VM to Static Web App
	•	Browser blocked requests
	•	Needed:
	•	CORS in Flask
	•	Env vars baked into GitHub Actions
  understand build-time vs runtime config
2. Order-service failed
	•	Azure Log Stream showed almost nothing
	•	Needed Kudu + env inspection + network tests

---

## Acknowledgments

During troubleshooting, I used documentation and AI-assisted tools to interpret error messages and explore possible causes, which helped narrow down configuration issues related to environment variables and service connectivity.
