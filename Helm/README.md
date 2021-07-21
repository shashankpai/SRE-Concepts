
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

# 3. Helm dry run with debug 

```
helm install my-chart --dry-run --debug my-chart/
```

You can also use `--generate-name` flag to generate a name for your chart 
