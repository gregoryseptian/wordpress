<h1> How to deploy docker image </h1>

<b>Pre-requisite step:</b>
- Install docker and kubectl binary 
- Install kubernetes cluster

1. Pull the repository
2. Go to inside folder MySQL and change the below parameter
   MYSQL_USER=mysql \
   MYSQL_PASSWORD=xxxxx \
3. Build MySQL Dockerfile
   docker build -t "mysql" .
4. Deploy MySQL Dockerfile
   docker run --name mysql-db -d mysql
5. Go to inside folder Wordpress and change the below parameter
   WORDPRESS_DB_HOST=127.0.0.1 \
   WORDPRESS_DB_USER=wpuser \
   WORDPRESS_DB_PASSWORD=xxxx \
6. Build Wordpress Image
   docker build -t "wp-image" .
7. deploy docker image to dockerhub
   docker push docker-hub/wp-image
8. Go to inside Kubernetes folder and change the below parameter
   image: docker-hub/wp-image
10. Deploy the image into kubernetes cluster
    kubectl apply -f deploy-wp.yaml
11. Ensure the service is running
    kubectl get svc
12. Create auto scaller for the application
    kubectl apply -f autoscale-wp.yaml
