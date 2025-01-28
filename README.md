FastAPI AWS Lambda Deployment 🚀
This project demonstrates how to deploy a FastAPI application to AWS Lambda using an S3 bucket for deployment artifacts. It integrates API Gateway to expose the FastAPI endpoints.

📋 Features
FastAPI Framework: A lightweight and modern Python web framework.
AWS Lambda: A serverless architecture to handle requests.
AWS API Gateway: To expose the Lambda function to the web.
S3 Bucket: To store and deploy the application artifact.
🛠️ Prerequisites
Make sure you have the following installed and configured:

Python 3.9 or higher
AWS CLI (configured with AdministratorAccess)
Zip utility (for packaging)
FastAPI and uvicorn installed via pip:
bash
Copy
pip install fastapi uvicorn
🚀 Setup and Deployment
1️⃣ Create a FastAPI Application
Create a main.py file with the following code:

python
Copy
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello from FastAPI on Lambda!"}
2️⃣ Package the Application
Ensure the file structure is correct:

css
Copy
.
├── main.py
Create a zip file:

bash
Copy
zip -r api.zip main.py
3️⃣ Upload to S3
Use the AWS CLI to upload the zip file to your S3 bucket:

bash
Copy
aws s3 cp api.zip s3://<your-bucket-name>/api.zip
Replace <your-bucket-name> with the name of your S3 bucket.

4️⃣ Update the Lambda Function
Run the following command to update your Lambda function:

bash
Copy
aws lambda update-function-code \
    --function-name <lambda-function-name> \
    --s3-bucket <your-bucket-name> \
    --s3-key api.zip
Replace <lambda-function-name> with your Lambda function's name and <your-bucket-name> with the name of your S3 bucket.

5️⃣ Test the Function
Test the Lambda function using the AWS Management Console or AWS CLI.

Example:

bash
Copy
aws lambda invoke --function-name <lambda-function-name> response.json
Check the response.json file for the result.

🧪 Troubleshooting
Error: Unable to import module 'main': No module named 'main'

Ensure the main.py file exists at the root of your zip file.
Ensure the Lambda function handler is set to main.handler.
Error: Internal Server Error

Check the CloudWatch logs for detailed error messages.
🛡️ Permissions
Ensure your Lambda function has the correct IAM role with the following permissions:

AWSLambdaBasicExecutionRole
S3ReadAccess (if using an S3 bucket for artifacts)
📖 References
FastAPI Documentation
AWS Lambda Documentation
AWS CLI Documentation
📝 License
This project is licensed under the MIT License.

