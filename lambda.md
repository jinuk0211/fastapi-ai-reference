py -3 -m venv venv

venv/Scripts/activate.bat

postgresql zip파일

pip install aws-psycopg2 -t.
psycopg2==2.9.1

SQLAlchemy==1.4.23

pydantic==1.8.2

requests==2.26.0

fastapi==0.68.0


  step 2 Build and package the Docker image:
---------------------------
docker build -t fastapi-login-service .
docker run --rm -v $(pwd):/var/task lambci/lambda:build-python3.9 pip install -r requirements.txt -t python
zip -r fastapi-login-service.zip .

Step 3: Deploy to AWS Lambda
----------------------
aws s3 mb s3://fastapi-login-service-bucket
aws s3 cp fastapi-login-service.zip s3://fastapi-login-service-bucket/
aws lambda create-function \
  --function-name fastapi-login-service \
  --runtime python3.9 \
  --role arn:aws:iam::your-account-id:role/your-lambda-execution-role \
  --handler main.handler \
  --code S3Bucket=fastapi-login-service-bucket,S3Key=fastapi-login-service.zip \
  --timeout 60 \
  --memory-size 128

Step 4: Set Up API Gateway
-----------
aws apigateway create-rest-api --name "FastAPI Login Service"
aws apigateway get-rest-apis
aws apigateway create-resource --rest-api-id <api-id> --parent-id <parent-resource-id> --path-part "{proxy+}"
aws apigateway put-method --rest-api-id <api-id> --resource-id <resource-id> --http-method ANY --authorization-type NONE
aws apigateway put-integration \
  --rest-api-id <api-id> \
  --resource-id <resource-id> \
  --http-method ANY \
  --type AWS_PROXY \
  --integration-http-method POST \
  --uri "arn:aws:apigateway:<region>:lambda:path/2015-03-31/functions/arn:aws:lambda:<region>:<account-id>:function:fastapi-login-service/invocations"
aws apigateway create-deployment --rest-api-id <api-id> --stage-name prod
aws lambda add-permission \
  --function-name fastapi-login-service \
  --statement-id apigateway-test-2 \
  --action "lambda:InvokeFunction" \
  --principal apigateway.amazonaws.com \
  --source-arn "arn:aws:execute-api:<region>:<account-id>:<api-id>/*/*/{proxy+}"

