# FastAPI AWS Lambda Deployment 🚀

This project demonstrates how to deploy a **FastAPI** application to **AWS Lambda** using an **S3 bucket** for deployment artifacts. It integrates **API Gateway** to expose the FastAPI endpoints.

---

## 📋 Features

- **FastAPI Framework**: A lightweight and modern Python web framework.
- **AWS Lambda**: A serverless architecture to handle requests.
- **AWS API Gateway**: To expose the Lambda function to the web.
- **S3 Bucket**: To store and deploy the application artifact.

---

## 🛠️ Prerequisites

Make sure you have the following installed and configured:

1. **Python 3.9 or higher**
2. **AWS CLI** (configured with `AdministratorAccess`)
3. **Zip utility** (for packaging your code)
4. Install required Python dependencies:
   ```bash
   pip install fastapi uvicorn


## 🚀 Setup and Deployment

1️⃣ Create a FastAPI Application
Create a main.py file with the following content:

python
Copy
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello from FastAPI on Lambda!"}

    
2️⃣ Package the Application
Ensure the file structure is as follows:

css
Copy
.
├── main.py
Package your code into a zip file:

bash
Copy
zip -r api.zip main.py


3️⃣ Upload the Package to S3
Use the AWS CLI to upload the zip file to your S3 bucket:

bash
Copy
aws s3 cp api.zip s3://<your-bucket-name>/api.zip
Replace <your-bucket-name> with the name of your S3 bucket.

4️⃣ Update the Lambda Function
Update your Lambda function code with the uploaded artifact:

bash
Copy
aws lambda update-function-code \
    --function-name <lambda-function-name> \
    --s3-bucket <your-bucket-name> \
    --s3-key api.zip
Replace <lambda-function-name> with the name of your Lambda function and <your-bucket-name> with your S3 bucket name.

5️⃣ Test the Lambda Function
Test the Lambda function using the AWS CLI:

bash
Copy
aws lambda invoke --function-name <lambda-function-name> response.json
The output will be stored in response.json.

🧪 Troubleshooting
Error: Unable to import module 'main': No module named 'main'

Ensure the main.py file is at the root of your zip file.
Ensure the Lambda function handler is set to main.handler.
Error: Internal Server Error

Check CloudWatch Logs for detailed error messages.
🛡️ IAM Permissions
Ensure your Lambda function is assigned an IAM role with the following permissions:

AWSLambdaBasicExecutionRole
S3ReadAccess (if using an S3 bucket for artifacts)
📖 References
FastAPI Documentation
AWS Lambda Documentation
AWS CLI Documentation
