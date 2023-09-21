# How to run

Clone this git repository and change to the directory
```
git clone https://github.com/rolani/infra-team-test.git
cd infra-team-test
```

Deploy the infrastructure and applications to AWS EKS using pulumi
```
make deploy
```
This will install all the Python dependencies needed and deploy the AWS resources defined.

Alternatively run:
```
pip install -r requirements.txt
pulumi up -s production --yes
```
The above command will output the load-balancer url for the web ui that entered in a browser.

# Application Details

- All resources deployed on AWS have the following tags

  `project: infra-team-test`

  `owner: richard`
- The web API is deployed as a deployment on the EKS cluster on a node in a private subnet. 
- The web API service uses a `ClusterIP` and thus it cannot be accessed from outside the cluster.
- The UI is likewise deployed on a node in a private subnet on the EKS cluster.
- The UI is exposed to the public internet through a `LoadBalancer` service

The infrastructure diagram is shown below

 ![architecture diagram](/diagram/intra-team-test.png)

# Cleanup

Run the following command to clean up/destroy all the created resources:
```
make destroy
```
Alternatively run:
```
pulumi destroy -s production --yes
pulumi stack rm production 
```
