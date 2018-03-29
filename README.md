##FITMAN Collaborative Asset Management Enabler Installation and Execution
This section describes the necessary steps to install the prepared/validated enablers. The selected enablers are provided with a Dockerfile and a docker-compose if necessary.
###	Requirements To install and execute the enabler 
it is necessary to have a Docker environment installed. More information can be found at https://docs.docker.com/get-started/
###	Installation 
To install the enabler, it is necessary to create the image from the Dockerfile. To do it type the following command on bash, at Dockerfile location by performing the command below. 

Start first with docker-liferay-6.2 folder to install lifreray with the required dependencies (sso, asset-rest, portlets… ), by executing the following commands: 
Docker build .

Execute the same command in the second folder (tomcat7) to init another tomcat server with required dependencies (openrdf-sesame, openrdf-workbench, consumer-marketplace, cm-api…) 

Docker build .


###	Execution

Execute the following commands to start the deployment of the images :

First start with the liferay image: 
Docker images

And then get the image number corresponding the two docker images, and then execute these commands: 
For tomcat: 
docker run -it --rm  -p 80:80 #imageNumber#


For Liferay:

First start the by creating the mysql image:

docker run --name lep-mysql -e MYSQL_ROOT_PASSWORD=mysecretpassword -e MYSQL_USER=lportal -e MYSQL_PASSWORD=lportal -e MYSQL_DATABASE=lportal -d mysql:5.6


And then execute the following command to link the database with Liferay image:
docker run --rm -it -p 8080:8080 --link lep-mysql:db_lep -e DB_TYPE=MYSQL #imageNumber#





