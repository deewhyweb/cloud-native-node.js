# Node.js Cloud Native Architecture Design
We are defining cloud native development or cloud native way as an approach to building and running applications that fully exploits the advantages of the cloud computing model based upon four key tenets:
* Services based architecture
* Containers & Docker image
* DevOps Automation   
* API based design

The scope of the project is to produce a working node.js based e-commerce application using the above principles.
The proposed approach is to take the existing coolstore (https://github.com/jbossdemocentral/coolstore-microservice) application and port some of the services to node.js, incorporating container native design technologies such as high observability, image immutability, and process disposability.
This project will make use of existing NPM modules where possible e.g. nodeshift, and third party tools e.g. Istio for microservice management.  The output from this project will be a comprehensive example of cloud native node.js application development.

* [Openshift installation](/openshift)
