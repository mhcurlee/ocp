# OCP install notes


### General notes

Override arg for health checks
```
openshift_disable_check=docker_image_availability,memory_availability,package_availability
```


master and infra need at least 4GB of RAM to have success.




### Egress IP

#### Set per-project egress policy:
```
oc patch netnamespace marvintest -p '{"egressIPs": ["192.168.255.230"]}'
```


#### Bind egress IP to a specific node:
```
oc patch hostsubnet node01.curlee.local -p \
  '{"egressIPs": ["192.168.255.230"]}'
```


#### Egress network policy example:

```
---
kind: EgressNetworkPolicy
apiVersion: v1
metadata:
  name: demo-egress-policy
spec:
  egress:
  - type: Deny
    to:
      dnsName: github.com
```



