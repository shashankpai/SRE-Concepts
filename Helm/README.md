
# 1. To create a Helm chart 
This will create all the required files for you , A skeleton gets created for you to then make change according to your requirements 

` helm create my chart`

ex : 
``` 
helm create my-chart 
Creating my-chart
```

the directory structure that gets created 

```
my-chart
├── charts
├── Chart.yaml
├── templates
│   ├── deployment.yaml
│   ├── _helpers.tpl
│   ├── hpa.yaml
│   ├── ingress.yaml
│   ├── NOTES.txt
│   ├── serviceaccount.yaml
│   ├── service.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml
```

# 2. Syntax checking for your helm charts 

This can be achieved using helm lint command 

ex:
```
helm lint my-chart/
==> Linting my-chart/
[INFO] Chart.yaml: icon is recommended

1 chart(s) linted, 0 chart(s) failed
``` 
```
helm lint my-chart/ --strict 
```

# 3. Helm dry run with debug 

```
helm install my-chart --dry-run --debug my-chart/
```

You can also use `--generate-name` flag to generate a name for your chart 

# 4. Helm dependency check and update 
`helm dep <option>`
  
  build       rebuild the charts/ directory based on the Chart.lock file
  list        list the dependencies for the given chart
  update      update charts/ based on the contents of Chart.yaml

```
helm dep build .
Hang tight while we grab the latest from your chart repositories...
...Unable to get an update from the "bitnami" chart repository (https://charts.bitnami.com/bitnami):
	stream error: stream ID 1; INTERNAL_ERROR
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈Happy Helming!⎈
Saving 1 charts
Downloading appmesh-controller from repo https://aws.github.io/eks-charts
Deleting outdated charts
```

```
helm dep list .
NAME              	VERSION	REPOSITORY                      	STATUS
appmesh-controller	0.5.0  	https://aws.github.io/eks-charts	ok    
```

```
helm dep update .
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "bitnami" chart repository
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈Happy Helming!⎈
Saving 1 charts
Downloading appmesh-controller from repo https://aws.github.io/eks-charts
Deleting outdated charts
```

# 5. Helm environment information

`helm env `

Gives all the environment related information

```
helm env 
HELM_BIN="helm"
HELM_DEBUG="false"
HELM_KUBEAPISERVER=""
HELM_KUBECONTEXT=""
HELM_KUBETOKEN=""
HELM_NAMESPACE="default"
HELM_PLUGINS="/home/shpai/.local/share/helm/plugins"
HELM_REGISTRY_CONFIG="/home/shpai/.config/helm/registry.json"
HELM_REPOSITORY_CACHE="/home/shpai/.cache/helm/repository"
HELM_REPOSITORY_CONFIG="/home/shpai/.config/helm/repositories.yaml"
```

# 6. helm get 

Get info about your helm release (for this you need to have an application installed)

```
helm get all exa 
```
this gives all the info about the installed application

```
helm get hooks exa
```
gives the information of hooks if present 

```
helm get notes exa
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=mychart,app.kubernetes.io/instance=exa" -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace default port-forward $POD_NAME 8080:80
```

```
helm get values exa
USER-SUPPLIED VALUES:
null
```

# 7. helm history

Gives the history of releases

```
helm history exa
REVISION	UPDATED                 	STATUS  	CHART        	APP VERSION	DESCRIPTION     
1       	Wed Jul 21 15:54:13 2021	deployed	mychart-0.1.0	1.16.0     	Install complete
```

so now there is only one release , if we do a upgrade 
ex: 
```
helm upgrade exa .
Release "exa" has been upgraded. Happy Helming!
NAME: exa
LAST DEPLOYED: Wed Jul 21 16:13:19 2021
NAMESPACE: default
STATUS: deployed
REVISION: 2
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=mychart,app.kubernetes.io/instance=exa" -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace default port-forward $POD_NAME 8080:80

```

and then 

```
helm history exa
REVISION	UPDATED                 	STATUS    	CHART        	APP VERSION	DESCRIPTION     
1       	Wed Jul 21 15:54:13 2021	superseded	mychart-0.1.0	1.16.0     	Install complete
2       	Wed Jul 21 16:13:19 2021	deployed  	mychart-0.1.0	1.16.0     	Upgrade complete
```

If you want to see only the last rollout use flag `--max` , defaults to 256 
```
helm history exa --max 1
REVISION	UPDATED                 	STATUS  	CHART        	APP VERSION	DESCRIPTION     
2       	Wed Jul 21 16:13:19 2021	deployed	mychart-0.1.0	1.16.0     	Upgrade complete
```

# 8. helm install 

to intall helm charts

`helm install exa .` or `helm install test test1` here test is the release name and test is the folder 

You can override the values set in values file by usin `--set` flag , so here we are overriding service type to nodeport from clusterip 

```
helm install exa . --set service.type=NodePort
NAME: exa
LAST DEPLOYED: Wed Jul 21 16:28:33 2021
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services exa-mychart)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo http://$NODE_IP:$NODE_PORT
```



