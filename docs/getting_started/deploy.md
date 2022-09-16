# Deploy a cloud hosted infrastructure

## Prerequesites
- **Docker 20.10.10+**: As all services are deployed as Docker containers, Docker is required. Documentation can be found [here](https://docs.docker.com/engine/install/).
- **Make**: Used to automate key, certificate and keystore/truststore creation.
- **OpenSSL**: Needed to create keys, certificates and keystores/truststores. Another use is the creation of a random password for the admin user.
- **Git**: To clone the deployement scripts.

## Run the cloudio server
```bash
git clone https://github.com/cloudio-project/cloudio-deployment-examples.git
cd cloudio-deployment-examples/develop-latest/docker-compose-single-node-persistent/
sudo chmod +x *.sh
sudo ./up.sh
```
The cloud.io microservices, databases and message broker are now running. You can see in the log `Using 5U1VD0RVwqWd7rXbmH7j8p2+Jz7XCa/U8pE7dHR3HPU= as password for admin user`.
This password is the admin password for the 2 databases, and the message broker. The REST API admin password is another one.

## Get the REST API admin password
- Display all the running containers:
```bash
sudo docker ps
```
- Copy the cloud.io services `CONTAINER ID`.
- ```bash
sudo docker logs **The CONTAINER ID you copied**
```
- Search for the log `User repository is empty - creating default admin user 'admin' with password 'WTxhFMXpwc1WffFG'`. It's generated at the microservices startup, when the user repository is empty.

?> Your cloud.iO server is now running on the port 80 of your machine!

## Files and folders

- `certificates`: This folder contains all keys and certificates for the CA and the message broker after the Makefile is processed.  
The folder initially contains just 2 files: 
  - `openssl.cnf`: OpenSSL configuration used to generate the keys and certificates.
  - `Makefile`: Makefile that automates the creation of all required keys and certificates.  
- `docker-compose.yml`: Contains the service definition of the cloud.iO application stack. Due to the limitations of the syntax for environment variables, those are defined in bash 
  scripts.
- `up.sh`: Creates the network, the containers, the links between them and starts all containers in background. This command can be used too to update running 
  containers.
- `stop.sh`: Stops the running containers of the cloud.iO application stack without actually removing them.
- `start.sh`: Resumes a cloud.iO application stack that was stopped using the command `stop.sh` before.
- `down.sh`: Stops and removes all containers and removes the docker network. All data in PostgreSQL and InfluxDB along with the passwords, keys and certificates 
will be preserved.
