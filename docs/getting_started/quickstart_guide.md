# Quickstart Guide

## Prerequesites

- A running **cloud.iO services** instance. See the getting started guide: [Deploy cloud hosted infrastructure](/getting_started/deploy).
- **Java JDK 11+ installed.**

## Create an endpoint

- Open to the cloudio swagger interface at **`http://cloudio_host/swagger-ui/index.html`**.
- Under *Endpoint management*, click on *Create a new endpoint.*, then *Try it out* and *Execute*.
- The server responds with the new endpoint informations, including its **UUID**:
<p align="center">
  <br>
  <img src="getting_started/_media/create_endpoint.png" style="width:50%" />
  <br>
</p>
Save it somewhere.

## Generate certificates

- Open to the cloudio swagger interface at **`http://cloudio_host/swagger-ui/index.html`**.
- Under *Endpoint provisioning*, click on *Get endpoint configuration information for a given endpoint.*.
- Select *application/java-archive* for the response media type:

<p align="center">
  <br>
  <img src="getting_started/_media/create_certs.png" style="width:50%" />
  <br>
</p>

- Enter the endpoint UUID as parameter:
<p align="center">
  <br>
  <img src="getting_started/_media/create_certs_2.png" style="width:50%" />
  <br>
</p>
- Click *Execute* and download the jar archive.

!> The jar file obtained is not an executable file. It is a jar archive that contains the certificates.

## Get an example endpoint
**Clone** or **download** the [cloudio-endpoint-java-example](https://github.com/cloudio-project/cloudio-endpoint-java-example) repository.

## Github Packages configuration
The [cloudio-endpoint-java library](https://github.com/cloudio-project/cloudio-endpoint-java) is hosted on Github Packages.

As the login is mandatory to read a Github package, you'll need to fill the *gradle.properties* file with your Github **username** and 
a **personal access token**. Don't know how to generate a github **personal access token**? 
Go to [the Github documentation](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

## Extract the certificates

- Copy the certificates jar archive in *cloudio-endpoint-java-example/src/main/resources/cloud.io/*.
- Extract the files contained in the jar archive:
<p align="center">
  <br>
  <img src="getting_started/_media/extract.png" style="width:50%" />
  <br>
</p>

## Fill the properties file

- Copy the content of **xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.properties** and paste it in **example.properties**.
- Complete *hostname*, *clientCert* and *authorityCert* path in **example.properties**.
- A filled *example.properties*:
```
ch.hevs.cloudio.endpoint.hostUri=ssl://192.168.37.130
ch.hevs.cloudio.endpoint.ssl.authorityCert=file:/C:/Users/myUsername/Desktop/cloudio-endpoint-java-example-main/src/main/resources/cloud.io/authority.jks
ch.hevs.cloudio.endpoint.ssl.clientCert=file:/C:/Users/myUsername/Desktop/cloudio-endpoint-java-example-main/src/main/resources/cloud.io/8aecad7e-2e69-4d0b-a656-a88395dbc2cf.p12
ch.hevs.cloudio.endpoint.ssl.verifyHostname=false
ch.hevs.cloudio.endpoint.uuid=8aecad7e-2e69-4d0b-a656-a88395dbc2cf
ch.hevs.cloudio.endpoint.ssl.clientPassword=qTAGQYkNtFMTJiQU
ch.hevs.cloudio.endpoint.ssl.authorityPassword=qTAGQYkNtFMTJiQU
```

## Run the endpoint

Linux:
```bash
./gradlew build
./gradlew run
```
<br>Windows:
```bash
gradlew.bat build
gradlew.bat run
```

You should now see the log *"Endpoint is online"* in the console.

## Read the endpoint data

Open a browser and enter:

```http
http://**cloudio hostname**/api/v1/data/**endpoint UUID**
```

The result will be the endpoint structure, filled with the last measured values.

?>More information about data access can be found [here](/data_access/data).

