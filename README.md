[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![](https://img.shields.io/maintenance/yes/2020.svg)
# AWS NeptuneDB

## What this nested stack does

* Creates a Neptune cluster inside of an existing VPC including a NeptuneDB instance that you can query the NeptuneDB Cluster with running Gremlin/Sparql (with the option of creating a read-only replica.)

* Creates a security group for the NeptuneDB Instance that allows inbound traffic from the VPC and SSH from the VPC with open outbound.

* Creates three subnets. Two for the DB cluster across multiple AZ's and one for the DB instance. The instance subnet is associated with the public route table so that it can download and install the gremlin client. The DB cluster is on a private subnet and does not have direct access to the internet as Neptune is designed as a VPC only service.

* Creates two route tables, one public and one private. As mentioned before, this is done so that the DB instance can have internet access to download packages and also act as an endpoint for internal and external requests (if desired) to the DB Cluster.

* Creates an S3 endpoint to facilitate bulk loading data into Neptune. More information can be found [here.](https://docs.aws.amazon.com/neptune/latest/userguide/bulk-load-data.html)

* Creates an EC2 instance with gremlin installed so that you can query the DB. (See Resources)

* (Optional) Creates a read-only replica in another availability zone to support external queries and keep the cluster from getting busy with read requests.

# Deploy
`aws cloudformation create-stack -t main.yaml --s3-bucket myBucket --region myRegion`

# Update
`aws cloudformation update-stack -t main.yaml`

# Destroy
`aws cloudformation destroy-stack -t main.yaml`

# Resources
* https://docs.aws.amazon.com/neptune/latest/userguide/access-graph-gremlin-console.html

# Owner
Adam Shero<br>
cloudarmy.io@gmail.com
