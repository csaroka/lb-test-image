# showmeip-webserver

Continer image with Apache and PHP that echos the running instance's current IP address on the main page.

#### Build in Docker or Pull Pre-Built Image
`docker build -t showmeip-server .` \
Alternatively, pull the pre-built image: \
`docker pull csaroka/showmeip:lts`

#### Run in Docker
`docker run -p 8080:80 -d showmeip-server`

#### Verify instance is reporting IP
`curl localhost:8080`

#### Stop the instance
`docker stop <Container-ID>`

#### Ship to a private registry
`docker tag showmeip-server harbor.lab.local/library/showmeip-server:v1` \
`docker push harbor.lab.local/library/showmeip-server:v1`

#### Create deployment on Kubernetes cluster
`kubectl run showmeip --image=harbor.lab.local/library/showmeip-server:v1 --replicas=4 --port=80`

#### Attach a LoadBalancer service to the deployment
`kubectl expose deployment showmeip --port=80 --type=LoadBalancer`

#### Get service External IP
`kubectl get svc`

#### Verify Load-balancing
`curl -w "\n" http://<External-IP>`
