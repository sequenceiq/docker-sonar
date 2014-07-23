# docker-sonar

SonarQube is an open platform to manage code quality.

The SonarQube platform is made of 3 components:

1. One Database to store
2. One Web Server for users to browse quality snapshots and configure the SonarQube instance
3. One or more Analyzers to analyze projects.

### Description

On this repo you'll find 2 images that provide the first 2 components:

	* Database (sonar-mysql)
	* WebServer (sonar-server).

This fork contains a docker file which will install the objective C plugin from octo into the sonar instance.

### Setup

1. Until the trusted build on index.docker.io is ready, you need to build the images:

	`cd sonar-mysql && docker build -t sequenceiq/sonar-mysql .`
	
	`cd sonar-server && docker build -t sequenceiq/sonar-server .`

1. First you need to run the database image, but you need to give it a name so it can be later linked with the sonar-server:

	`docker run -d -p 3306:3306 -name sonar_mysql sequenceiq/sonar-mysql`

2. Now you need to run the server and link it with the database. That link will be named "db".

	`docker run -d -p 9000:9000 -name sonar_server --link sonar_mysql:db sequenceiq/sonar-server`
	
3. Go to http://docker_host:9000/setup to upgrade the database
