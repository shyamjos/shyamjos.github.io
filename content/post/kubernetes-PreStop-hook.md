---
date: 2021-09-31
title: "HPA - How to gracefully scale down pods with PreStop hooks"
description: "Kubernetes provides container lifecycle hook framework to run code triggered by events during their management lifecycle called PostStart and PreStop hooks"
images:
- /assets/img/featured.jpg
tags: [ "kubernetes","container"]
keywords: ["kubernetes", "PreStop hook", "hpa", "scaling"]
---
One of our application running in kubernetes have a background job feature (which is a bad practice and against stateless architecture) and recently we noticed some of these background jobs were killed in midway due to pod scale-down done by horizontal pod autoscaler. Our assumption was Kubernetes will only terminate pods with less utilization but we were wrong! and its a random selection. 

In order to handle this issue we found out that we can use prestop hook feature in kubernetes to check for any background process running in container and wait for it to complete before sending termination signal.

## How PreStop hooks works in kubernetes
Kubernetes provides container lifecycle hook framework to run code triggered by events during their management lifecycle called PostStart and PreStop hooks. A PreStop hook is called immediately before sending termination signal and kubernetes will wait until the PreStop hook to complete or until it exceed the `terminationGracePeriodSeconds` value, Only after this kubernetes will sent the termination signal to the container.


## Our solution
Our solution was to use a bash script for PreStop hook which will check for `.lock` files created by the background process, if it finds a `.lock` file the script will wait for the `.lock` file to be removed and when the file is removed the script will exit then the container will receive termination signal. If the PreStop hook takes more time than `terminationGracePeriodSeconds` value then container will be terminated immediately once this value is crossed.

### PreStop hook bash script
```
#PreStop Script for checking background php tasks 
SECONDS=0
while true
do	
if [ -z "$(ls -A /app/demo-web/public/lock/*.lock 2> /dev/null)" ]; then
   echo "No lock files found!, container is safe to terminate [Time Elapsed: ${SECONDS}s]."
   exit 0
else
   echo "Lock files found!, waiting for backgound process to complete [Time Elapsed: ${SECONDS}s]."
   sleep 10
fi
done > /proc/1/fd/1 # sent outputs to conatiner's stdout
```

### Final deployment yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-web
  namespace: production
spec:
  progressDeadlineSeconds: 300
  revisionHistoryLimit: 5
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 5
      maxUnavailable: 0
  selector:
    matchLabels:
      app: demo-web
      tier: web
      environment: production 
  template:
    metadata:
      labels:
        app: demo-web
        tier: web
        environment: production
    spec:
      terminationGracePeriodSeconds: 300
      containers:
      - name: demo-web
        image: demo/demoweb:v1
        lifecycle:
          preStop :
             exec:
               command: ["bash", "/app/scripts/prestop.sh"]           
        imagePullPolicy: Always
        resources:
          requests:
            cpu: 50m
            memory: 150Mi
          limits:
            memory: "650Mi" 
        ports:
        - containerPort: 80
        readinessProbe:
         httpGet:
          path: /healthz
          port: 80
         initialDelaySeconds: 2
         periodSeconds: 5
         successThreshold: 1
         failureThreshold: 2
         timeoutSeconds: 2
        env:
         - name: HOST 
           value: "demo.app.com"
```
