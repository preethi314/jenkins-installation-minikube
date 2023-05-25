# jenkins-installation-minikube

minikube start


apiVersion: apps/v1
kind: Deployment
metadata:
  name: jenkins
  labels:
    app: jenkins
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jenkins
  template:
    metadata:
      labels:
        app: jenkins
    spec:
      volumes:
        - name: jenkins-data
          hostPath:
            path: /opt
      containers:
        - name: jenkins
          image: jenkins/jenkins:lts
          ports:
            - containerPort: 8080
          volumeMounts:
            - name: jenkins-data
              mountPath: /var/jenkins_home


kubectl apply -f jenkins-deployment.yaml


kubectl expose deployment jenkins --type=NodePort --port=8080



kubectl get service jenkins


kubectl exec -it <jenkins-pod-name> -- /bin/bash
