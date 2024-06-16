Car Dealership Project

Overview
The Car Dealership System is a dynamic web application designed to facilitate the management of a car dealership's operations. It supports features such as user authentication, inventory management, customer reviews, and comprehensive search capabilities.

Setup Instructions

- Building the Client
Set up the frontend client which is presumably a React application.
bash


cd /home/project/xrwvm-fullstack_developer_capstone/server/frontend
npm install
npm run build

- Starting the Backend Server
   
Set up and start the Django backend server.

cd /home/project/xrwvm-fullstack_developer_capstone/server
pip install virtualenv
virtualenv djangoenv
source djangoenv/bin/activate
python3 -m pip install -U -r requirements.txt
python3 manage.py makemigrations
python3 manage.py migrate
python3 manage.py runserver

- Database Migrations

Perform database migrations for models.

python3 manage.py makemigrations
python3 manage.py migrate --run-syncdb

- Starting the Database
Build and start the database using Docker.

cd /home/project/xrwvm-fullstack_developer_capstone/server/database
docker build . -t nodeapp
docker-compose up

- Starting the Sentiment Analyzer
Build and deploy the sentiment analyzer microservice.

cd xrwvm-fullstack_developer_capstone/server/djangoapp/microservices
docker build . -t us.icr.io/${SN_ICR_NAMESPACE}/senti_analyzer
docker push us.icr.io/${SN_ICR_NAMESPACE}/senti_analyzer
ibmcloud ce application create --name sentianalyzer --image us.icr.io/${SN_ICR_NAMESPACE}/senti_analyzer --registry-secret icr-secret --port 5000

- Creating Kubernetes Deployment
Deploy the application using Kubernetes.

kubectl apply -f deployment.yaml
kubectl port-forward deployment.apps/dealership 8000:8000

- Troubleshooting
If the application is not working as expected, verify the environment variables and settings.
•	Check Django settings in djangoproj/settings.py.
•	Review .env file settings in djangoapp/.env.

Additional Information

Ensure that all configurations, such as database settings and external service credentials, are correctly set up according to the deployment environment.

