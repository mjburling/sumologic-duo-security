# sumologic-duo-security
Serverless collection solution to collect Duo security logs in to Sumo logic 

### Sumo Logic App for Duo Security
Duo provides two-factor authentication, endpoint remediation, and secure single sign-on tools. The Sumo Logic App for Duo Security helps you monitor your Duo account’s authentication logs, administrator logs, and telephony logs. The dashboards provide insight into failed and successful authentications, events breakdown by applications, factors, and users, geo-location of events, admin activities, outliers, threat analysis of authentication, and administrator events.

### Log Types
Sumo Logic App for Duo Security uses following logs. See Duo's [documentation](https://duo.com/docs/adminapi#logs) for details of the log schema.

- Authentication Logs
- Administrator Logs
- Telephony Logs

### Collect Logs for Duo Security Via AWS Lambda
1. Create an HTTP Logs and Metrics Source.
2. Download the Lambda Function code, and upload it to AWS Lambda Console and create a Lambda function.
3. Define Environment Variables for the Lambda Function.
4. Add a time-based trigger for the Lambda function.

### Collect Logs for Duo Security Via CronJob task deployed at Kubernetes Cluster
1. Deploy the secret `duocreds` using following kubectl cmd, and replace S_KEY, I_KEY, HOST with [Duo Admin API Creds](https://duo.com/docs/adminapi#logs). Replace COLL_ENDPOINT with Sumo Logic HTTP URL

```
kubectl create secret generic duocreds --from-literal=S_KEY=<REPLACE> --from-literal=I_KEY=<REPLACE> --from-literal=HOST=<REPLACE> --from-literal=COLL_ENDPOINT=<REPLACE> --from-literal=SCAN_INTERVAL_IN_SEC=300
```

2. Run following cmd, this will create 5 mins cronjob to fetch Duo logs and send to Sumo Logic HTTP URL

```kubectl apply -f https://sumologic-app-data.s3.amazonaws.com/Duo/hw_dep.yaml```

3. Verify 

```
   kubectl get pods  | grep duo
   kubectl get jobs
````
 

Detailed instructions [here](https://help.sumologic.com/07Sumo-Logic-Apps/22Security_and_Threat_Detection/Duo_Security/Collect_Logs_for_Duo_Security).

### Install the Duo Security App and View the Dashboards
Login in to your Sumo Logic account and install the App from App Catalog
