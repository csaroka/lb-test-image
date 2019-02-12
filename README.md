# lb-test-webserver

Continer image with Apache and PHP that echos the running instance's current IP address on the main page.

#### Build in Docker or Pull Pre-Built Image
`docker build -t lb-test-webserver .` \
Alternatively, pull the pre-built image: \
`docker pull csaroka/showmeip:lts`

#### Run in Docker
`docker run -p 8080:80 -d lb-test-webserver`

#### Verify instance is reporting IP
`curl localhost:8080`

#### Stop the instance
`docker stop <Container-ID>`

#### Ship to a private registry
`docker tag lb-test-webserver harbor.lab.local/library/lb-test-webserver:v1` \
`docker push harbor.lab.local/library/lb-test-webserver:v1`

#### Create deployment on Kubernetes cluster
`kubectl run lb-test-webserver --image=harbor.lab.local/library/lb-test-webserver:v1 --replicas=4 --port=80`

#### Attach a LoadBalancer service to the deployment
`kubectl expose deployment lb-test-webserver --port=80 --type=LoadBalancer`

#### Get service External IP
`kubectl get svc`

#### Verify Load-balancing
`curl -w "\n" http://<External-IP>`
