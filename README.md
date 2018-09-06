# Apache Ranger S3 Plugin

Ranger S3 Plugin enables creation of policies in Apache Ranger for S3 buckets hosted on Ceph/RadosGW (S3 coming later). 
It merely allows for the creation of policies and does not set ACLs by itself. It can be used together with its sister 
`scala` project [gargoyle-s3proxy](https://github.com/arempter/gargoyle-s3proxy).

# Installation

1. Run ceph demo container using docker-compose
```
docker-compose up
```
It will start Ceph demo image on port 8010. 

2. Build the plugin jar using maven 
```
mvn package
``` 
If you do not have a local Ceph installation to test against use `mvn package -DskipTests`.

3. Copy the jar to `${RANGER_HOME}/ews/webapp/WEB-INF/classes/ranger-plugins/s3`. Please note that the location
is important (`s3`). 

4. Load the service definition into Apache Ranger. 
```
curl -u <admin>:<admin> -d "@s3-ranger.json" -X POST -H "Accept: application/json" -H "Content-Type: application/json" 
http://{RANGER_HOST}:{RANGER_PORT}/service/public/v2/api/servicedef
```
5. Configure the service in Apache Ranger by logging in to the Web UI.

# Roadmap

* Proper lookups
* No ceph-user name required
* AWS S3 support
