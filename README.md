# kong-kube
kubernetes deployments yaml files for kong project.
## How to use:
### Use postgresql as datastore:
Create postgres service:
```
    kubectl create -f postgres.yaml
```
   Edit kong-postgresql.yml, modify postgres ip to your postgres cluster  ip.
```
	    - name: KONG_PG_HOST
              value: Your_Postgresql_Cluster_Ip
```
   
Create kong service:
```
    kubectl create -f kong-postgresql.yaml
```
### Use cassandra as datastore:
Create cassandra service:
```
    kubectl create -f cassandra.yaml
```
   Edit kong-cassandra.yml, modify cassandra ip to your cassandra cluster  ip.
```
            - name: KONG_CASSANDRA_CONTACT_POINTS 
            value: Your_Cassandra_Cluster_Ip 
```
   
Create kong service:
```
    kubectl create -f kong-cassandra.yaml
```
Finally, enjoy it.

##Problem:

1. If use cassandra as kong datastore, kong node replicas number must be set to 1 in kong-cassandra.yaml, if not, cassandra may report error as belows:
``` 
ServerError: 
<ErrorMessage code=0000 [Server error] message="java.lang.RuntimeException:
java.util.concurrent.ExecutionException: 
    java.lang.RuntimeException:      
        org.apache.cassandra.exceptions.ConfigurationException: Column family ID mismatch (found e8c03790-c952-11e4-a753-5981ea73cd7c; expected e8b14370-c952-11e4-a844-8f10bfb9c386)">
	
```
this error will cause kong container starting terminated error.
