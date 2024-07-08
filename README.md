## Kubernetes Notes
https://arkalim.notion.site/Kubernetes-c64b2976b0364cc69864490edef33717


# K8s Commands
 - ## PODS
1. Get pods configurations 
```sh
    k -n name_space get pod -oyaml
```
2. Get pods with labels
```sh
kubectl get pod --show-labels
```
## K8s Dry RUN
```sh
kubectl run pod --image=nginx --dry-run=client -o yaml > testpod.yaml
```
### Valid --dry-run values : client, none, server
```sh
k -n name_space get pod -oyaml | grep -i <word> -B 20
```
### Create ClusterRole
```sh
k create clusterrole acme-corp-clusterrole --verb=create --resource=replicaset,daemonset,deploy
```
###

```sh
k -n name_space get pod -oyaml | grep -i <word> -B 20
```


```sh
k -n name_space get pod -oyaml | grep -i <word> -B 20
```
- To grep a word and make it bold
```sh
k -n name_space get pod -oyaml | grep -i <word> -B 20
```

## Scheduling Priority
```sh
apiVersion: v1
kind: Pod
metadata:
  name: important
  namespace: lion
  labels:
    name: myapp
spec:
  containers:
  - name: myapp
    image: nginx:1.21.6-alpine
    resources:
      limits:
        memory: "1Gi"
        cpu: "500m"
    ports:
      - containerPort: 80
  priority: 300000000
  priorityClassName: level3

```

Check HPA (Horizontal Pod Autoscaller Status)
```sh
kubectl get hpa my-app-hpa
```
Dillinger is currently extended with the following plugins.
Instructions on how to use them in your own application are linked below.


|Q.1:  You have an application deployed on an EKS cluster, and you need to scale it based on a custom metric. How would you achieve this?
A: Can use the Kubernetes Horizontal Pod Autoscaler (HPA) with custom metrics|

Q.2: You have an application deployed on an EKS cluster, and you want to enable automatic scaling of both pods and worker nodes based on CPU utilization. How would you accomplish this?
A: To enable automatic scaling of pods and worker nodes based on CPU utilization, you can follow these steps:
1. Create a Kubernetes Horizontal Pod Autoscaler (HPA) manifest or use the Kubernetes API to define an HPA object for your application.
2. Set the HPA to scale based on CPU utilization, specifying the desired minimum and maximum number of replicas for your application.
3. Deploy the updated HPA manifest to the cluster.
4. The HPA controller will periodically monitor the CPU utilization of the pods and adjust the number of replicas accordingly.
5. To enable automatic scaling of worker nodes, create an Amazon EC2 Auto Scaling Group (ASG) or a managed node group for the EKS cluster.
6. Configure the ASG or node group to scale based on CPU utilization, specifying the desired minimum and maximum number of worker nodes.
7. Associate the ASG or node group with the EKS cluster.
8. The ASG or node group will monitor the CPU utilization of the worker nodes and scale the cluster up or down accordingly.

Q.3: You have a multi-tenant EKS cluster where multiple teams deploy their applications. You want to ensure resource isolation and prevent one team's application from affecting the performance of another team's application. How would you achieve this?

Answer 5:
To ensure resource isolation and prevent interference between applications in a multi-tenant EKS cluster, you can employ the following approaches:
1. Utilize Kubernetes namespaces to logically separate applications and teams. Each team can have its own namespace, allowing them to manage and deploy their applications independently.
2. Implement Kubernetes Resource Quotas within each namespace to define limits on CPU, memory, and other resources that each team can utilize. This prevents one team from monopolizing cluster resources and impacting others.
3. Configure Kubernetes Network Policies to control network traffic between pods and namespaces. Network Policies can restrict or allow communication based on specific rules, ensuring that applications are isolated from each other.
4. Consider using Kubernetes Pod Security Policies to enforce security and isolation measures. Pod Security Policies define a set of conditions that pods must adhere to, ensuring that each team's applications meet the defined security standards.
5. Monitor and analyze resource usage within the cluster using tools like Prometheus and Grafana. This allows you to identify resource-intensive applications and take necessary actions to ensure fair resource distribution and prevent performance degradation for other applications.
6. Regularly communicate and collaborate with teams to understand their requirements and address any potential conflicts or issues related to resource utilization and performance.

## Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantaneously see your updates!

Open your favorite Terminal and run these commands.

First Tab:

```sh
node app
```

Second Tab:

```sh
gulp watch
```

(optional) Third:

```sh
karma test
```

#### Building for source

For production release:

```sh
gulp build --prod
```

Generating pre-built zip archives for distribution:

```sh
gulp build dist --prod
```

## Docker

Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the
Dockerfile if necessary. When ready, simply use the Dockerfile to
build the image.

```sh
cd dillinger
docker build -t <youruser>/dillinger:${package.json.version} .
```

This will create the dillinger image and pull in the necessary dependencies.
Be sure to swap out `${package.json.version}` with the actual
version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on
your host. In this example, we simply map port 8000 of the host to
port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

```sh
docker run -d -p 8000:8080 --restart=always --cap-add=SYS_ADMIN --name=dillinger <youruser>/dillinger:${package.json.version}
```

> Note: `--capt-add=SYS-ADMIN` is required for PDF rendering.

Verify the deployment by navigating to your server address in
your preferred browser.

```sh
127.0.0.1:8000
```

## Containers vs VM
|---|---|---|

