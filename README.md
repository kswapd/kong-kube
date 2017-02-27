# kong-kube
kubernetes deployments yaml files for kong project.
## how to use:
Create postgres service:
```
    kubectl create -f postgres.yaml
```
   Edit kong.yml, modify postgres ip to your postgres cluster  ip.
```
	    - name: KONG_PG_HOST
              value: Your_postgrescluster_ip
```
   
Create kong service:
```
    kubectl create -f kong.yaml
```
