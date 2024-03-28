

# Kubernetes hackathon part-2

## Prerequisites
- Kubectl installation
	- https://kubernetes.io/docs/tasks/tools/
- Minikube installation
	- https://minikube.sigs.k8s.io/docs/start/
- Start the cluster using 
	 ```minikube start```
- Ensure minikube cluster context is set in **kubectl** command


## Task 1
Create a namespace `my-namespace` in your cluster

## Task 2
Create a Pod with name `nginx` with images `nginx:latest`, `grafana/grafana-oss` in `my-namespace` using yaml configurations.

Create a YAML for a Pod with multiple containers with container names `first`, `second` for the given images


Copy the YAML content below
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: my-namespace
spec:
  containers:
  - name: first
    image: nginx:latest
    ports:
    - containerPort: 8080
  - name: second
    image: grafana/grafana-oss
    ports:
    - containerPort: 8082

```

List all the pods in the namespace `my-namespace` using `kubectl get pods -n <namespace>` command
```
PS C:\WINDOWS\system32> kubectl get pods -n my-namespace
NAME    READY   STATUS    RESTARTS   AGE
nginx   2/2     Running   0          2m
```

## Task 3

List all the logs of pod `nginx` running in `my-namespace`  using `kubectl logs` command

Refference: 
https://kubernetes.io/docs/reference/kubectl/generated/kubectl_logs

get the logs for container `first` in `nginx` pod

```
PS C:\WINDOWS\system32>  kubectl logs pods/nginx -c first -n my-namespace
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/03/28 06:23:43 [notice] 1#1: using the "epoll" event method
2024/03/28 06:23:43 [notice] 1#1: nginx/1.25.4
2024/03/28 06:23:43 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2024/03/28 06:23:43 [notice] 1#1: OS: Linux 5.15.133.1-microsoft-standard-WSL2
2024/03/28 06:23:43 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/03/28 06:23:43 [notice] 1#1: start worker processes
2024/03/28 06:23:43 [notice] 1#1: start worker process 29
2024/03/28 06:23:43 [notice] 1#1: start worker process 30
2024/03/28 06:23:43 [notice] 1#1: start worker process 31
2024/03/28 06:23:43 [notice] 1#1: start worker process 32
2024/03/28 06:23:43 [notice] 1#1: start worker process 33
2024/03/28 06:23:43 [notice] 1#1: start worker process 34
2024/03/28 06:23:43 [notice] 1#1: start worker process 35
2024/03/28 06:23:43 [notice] 1#1: start worker process 36
```

get the logs for container `second` in `nginx` pod

```
PS C:\WINDOWS\system32>  kubectl logs pods/nginx -c second -n my-namespace
logger=settings t=2024-03-28T06:24:34.797450001Z level=info msg="Starting Grafana" version=10.4.1 commit=d94d597d847c05085542c29dfad6b3f469cc77e1 branch=v10.4.x compiled=2024-03-28T06:24:34Z
logger=settings t=2024-03-28T06:24:34.801264803Z level=info msg="Config loaded from" file=/usr/share/grafana/conf/defaults.ini
logger=settings t=2024-03-28T06:24:34.801302602Z level=info msg="Config loaded from" file=/etc/grafana/grafana.ini
logger=settings t=2024-03-28T06:24:34.801308102Z level=info msg="Config overridden from command line" arg="default.paths.data=/var/lib/grafana"
logger=settings t=2024-03-28T06:24:34.801311202Z level=info msg="Config overridden from command line" arg="default.paths.logs=/var/log/grafana"
logger=settings t=2024-03-28T06:24:34.801313701Z level=info msg="Config overridden from command line" arg="default.paths.plugins=/var/lib/grafana/plugins"
logger=settings t=2024-03-28T06:24:34.801316401Z level=info msg="Config overridden from command line" arg="default.paths.provisioning=/etc/grafana/provisioning"
logger=settings t=2024-03-28T06:24:34.801319101Z level=info msg="Config overridden from command line" arg="default.log.mode=console"
logger=settings t=2024-03-28T06:24:34.801355Z level=info msg="Config overridden from Environment variable" var="GF_PATHS_DATA=/var/lib/grafana"
logger=settings t=2024-03-28T06:24:34.8013581Z level=info msg="Config overridden from Environment variable" var="GF_PATHS_LOGS=/var/log/grafana"
logger=settings t=2024-03-28T06:24:34.8013608Z level=info msg="Config overridden from Environment variable" var="GF_PATHS_PLUGINS=/var/lib/grafana/plugins"
logger=settings t=2024-03-28T06:24:34.8013637Z level=info msg="Config overridden from Environment variable" var="GF_PATHS_PROVISIONING=/etc/grafana/provisioning"
logger=settings t=2024-03-28T06:24:34.8013669Z level=info msg=Target target=[all]
logger=settings t=2024-03-28T06:24:34.8013749Z level=info msg="Path Home" path=/usr/share/grafana
logger=settings t=2024-03-28T06:24:34.8013775Z level=info msg="Path Data" path=/var/lib/grafana
logger=settings t=2024-03-28T06:24:34.8013799Z level=info msg="Path Logs" path=/var/log/grafana
logger=settings t=2024-03-28T06:24:34.801453398Z level=info msg="Path Plugins" path=/var/lib/grafana/plugins
logger=settings t=2024-03-28T06:24:34.801487697Z level=info msg="Path Provisioning" path=/etc/grafana/provisioning
logger=settings t=2024-03-28T06:24:34.801499297Z level=info msg="App mode production"
logger=sqlstore t=2024-03-28T06:24:34.810681761Z level=info msg="Connecting to DB" dbtype=sqlite3
logger=sqlstore t=2024-03-28T06:24:34.811394743Z level=info msg="Creating SQLite database file" path=/var/lib/grafana/grafana.db
logger=migrator t=2024-03-28T06:24:34.830890743Z level=info msg="Starting DB migrations"
logger=migrator t=2024-03-28T06:24:34.846835735Z level=info msg="Executing migration" id="create migration_log table"
logger=migrator t=2024-03-28T06:24:34.851489815Z level=info msg="Migration successfully executed" id="create migration_log table" duration=4.65408ms
```

## Task 4
Delete the nginx pod


## Task 5
Create a replicaset named `nginx-replicaset` for image `nginx:1.42.6` with 3 replicas in the namespace `my-namespace` using YAML configurations

1. Copy the YAML content below
	```
	apiVersion: apps/v1
	kind: ReplicaSet
	metadata:
	name: nginx-replicaset
	namespace: my-namespace
	spec:
	replicas: 3
	selector:
		matchLabels:
		app: nginx-replicaset-app
	template:
		metadata:
		labels:
			app: nginx-replicaset-app
		spec:
		containers:
		- name: nginx
			image: nginx:1.42.6

	```

2. Apply the yaml configurations using `kubectl apply -f <yaml file>`

3. List the replicaset in the namespace `my-namespace` using `kubectl get replicaset -n <namespace>`
	```
	PS C:\WINDOWS\system32> kubectl get replicaset -n my-namespace
	NAME               DESIRED   CURRENT   READY   AGE
	nginx-replicaset   3         3         0       34s

	```

4. List the pods in the namespace `my-namespace` 
	```
	PS C:\WINDOWS\system32> kubectl get pods -n my-namespace
	NAME                     READY   STATUS             RESTARTS   AGE
	nginx-replicaset-5qktb   0/1     ImagePullBackOff   0          2m3s
	nginx-replicaset-c4gzj   0/1     ErrImagePull       0          2m3s
	nginx-replicaset-dwmvj   0/1     ImagePullBackOff   0          2m3s

	```

5. Find out why the pods are failing in the `nginx-replicaset` replicaset 
	```
	It gives image pull error stating that it had issues pulling images of nginx:1.42.6 upon further inspection it was found that these is no version 1.42.6 for nginx and thus we will use latest

	```

6. Fix the issue in the YAML configuration created  and re-apply configuration using `kubectl apply`

	List the pods in the namespace `my-namespace` 
	```
	PS C:\WINDOWS\system32> kubectl get pods -n my-namespace
	NAME                     READY   STATUS             RESTARTS   AGE
	nginx-replicaset-7sxvn   0/1     ImagePullBackOff   0          27s
	nginx-replicaset-hlnw7   0/1     ImagePullBackOff   0          27s
	nginx-replicaset-l9hqh   0/1     ImagePullBackOff   0          27s

	``

7. Do a `kubectl delete -f <file-name>` and apply it again using `kubectl apply -f <file-name>`

	List the pods in the namespace `my-namespace` 
	```
	PS C:\WINDOWS\system32> kubectl get pods -n my-namespace
	NAME                     READY   STATUS    RESTARTS   AGE
	nginx-replicaset-c6dhj   1/1     Running   0          20s
	nginx-replicaset-cf2hl   1/1     Running   0          20s
	nginx-replicaset-tjk97   1/1     Running   0          20s

	```

8. Explain your observations from steps 6,7

	```
	changing nginx version to latest have solved the issue of image pull and have got 3 replicas of nginx running. And replicaset needs to be deleted before it can be re-applied to see the changes.

	```


9. Increase/dicrease the count of replicas by 1 in the YAML and apply it again 

	List the pods in the namespace `my-namespace` 
	```
	PS C:\WINDOWS\system32> kubectl get pods -n my-namespace
	NAME                     READY   STATUS    RESTARTS   AGE
	nginx-replicaset-c6dhj   1/1     Running   0          2m11s
	nginx-replicaset-tjk97   1/1     Running   0          2m11s
	```

10. Delete the `nginx-replicaset` using `kubectl delete replicaset/<replicaset-name> -n <namespace>`

## Task 6
Create a deployment named `nginx-deployment` for image `nginx:1.42.6` with 3 replicas in the namespace `my-namespace` using YAML configurations

1. Copy the YAML content below
	```
	apiVersion: apps/v1
	kind: Deployment
	metadata:
		name: nginx-deployment
		namespace: my-namespace
	spec:
		replicas: 3
		selector:
			matchLabels:
			app: nginx
		template:
			metadata:
			labels:
				app: nginx
			spec:
			containers:
			- name: nginx
				image: nginx:1.42.6
				ports:
				- containerPort: 80

	```

2. Apply the yaml configurations using `kubectl apply -f <yaml file>`

3. List the deployments in the namespace `my-namespace` using `kubectl get deployments -n <namespace>`
	```
	PS C:\WINDOWS\system32> kubectl get deployments -n my-namespace
	NAME               READY   UP-TO-DATE   AVAILABLE   AGE
	nginx-deployment   0/3     3            0           91s

	```
4. List the replicasets in the namespace `my-namespace` using `kubectl get replicaset -n <namespace>`
	```
	PS C:\WINDOWS\system32> kubectl get replicaset -n my-namespace
	NAME                         DESIRED   CURRENT   READY   AGE
	nginx-deployment-b5cb4c4fc   3         3         0       4m37s

	```

5. List the pods in the namespace `my-namespace` 
	```
	PS C:\WINDOWS\system32> kubectl get pods -n my-namespace
	NAME                               READY   STATUS             RESTARTS   AGE
	nginx-deployment-b5cb4c4fc-4nqb8   0/1     ImagePullBackOff   0          5m3s
	nginx-deployment-b5cb4c4fc-gtdpb   0/1     ImagePullBackOff   0          5m3s
	nginx-deployment-b5cb4c4fc-slqvq   0/1     ImagePullBackOff   0          5m3s

	```

6. Change the image in YAML to `nginx:1.25.4` and re-apply the yaml using `kubectl apply -f <file-name>`

	```
	PS C:\WINDOWS\system32> kubectl apply -f D:\texttosql\demo\k8s-basics-hackathon-part-2\nginx-deployment.yaml
	deployment.apps/nginx-deployment created

	```
	List the pods in the namespace `my-namespace` 
	```
	PS C:\WINDOWS\system32> kubectl get pods -n my-namespace
	NAME                                READY   STATUS    RESTARTS   AGE
	nginx-deployment-7ffd9c9dbb-76h6w   1/1     Running   0          66s
	nginx-deployment-7ffd9c9dbb-h4ngx   1/1     Running   0          66s
	nginx-deployment-7ffd9c9dbb-mzw7f   1/1     Running   0          66s

	```
	  List the replicaset in the namespace `my-namespace` 
	```
	PS C:\WINDOWS\system32> kubectl get replicaset -n my-namespace
	NAME                          DESIRED   CURRENT   READY   AGE
	nginx-deployment-7ffd9c9dbb   3         3         3       2m6s

	```
7. Increase/dicrease the count of replicas by 1 in the YAML and apply it again 

	List the pods in the namespace `my-namespace` 
	```
	PS C:\WINDOWS\system32> kubectl get pods -n my-namespace
	NAME                                READY   STATUS    RESTARTS   AGE
	nginx-deployment-7ffd9c9dbb-6pjq4   1/1     Running   0          4m13s
	nginx-deployment-7ffd9c9dbb-76h6w   1/1     Running   0          7m15s
	nginx-deployment-7ffd9c9dbb-h4ngx   1/1     Running   0          7m15s
	nginx-deployment-7ffd9c9dbb-mzw7f   1/1     Running   0          7m15s
	```

8. Compare the effort while updating the images in replicaset and deployment
	```
	replicaset is used to run aditional replicas of a pod in case if a pod fails then the traffic can be re-routed to one of its replicas. Deployment it used to roll out or deploy images, replicasets and other components.

	```
9.  Delete the deployment  `nginx-deployment` using kubectl delete command

## Bonus task

Apply the given deployment.yaml file using `kubectl apply -f`

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: my-namespace
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
	app: nginx
    spec:
      containers:
      - name: nginx
	image: nginx:latest
	ports:
	- containerPort: 80
  readinessProbe:
	httpGet:
	  path: /
	  port: 82
  livenessProbe:
	httpGet:
	  path: /
	  port: 82
```

1. List the pods for deployment
	```
	PS C:\WINDOWS\system32> kubectl get pods -n my-namespace
	NAME                               READY   STATUS             RESTARTS      AGE
	nginx-deployment-fbd6c6f5f-87zc6   0/1     CrashLoopBackOff   4 (38s ago)   3m9s

	```
2. Findout why the pods are not ready
	```
	I checked the events of the pod using describe and found out that the livenessProb had failed to establish connection. Through a bit reserch and help I found that the livenessprob was trying to establish connection to a different prob than the one where nginx was running. fixing the port resolved the issue.
	
	```
3. Fix the issue and explain your understanding on  `readinessProbe` `livenessProbe`
	
	```
	apiVersion: apps/v1
	kind: Deployment
	metadata:
	name: nginx-deployment
	namespace: my-namespace
	spec:
	replicas: 1
	selector:
		matchLabels:
		app: nginx
	template:
		metadata:
		labels:
			app: nginx
		spec:
		containers:
		- name: nginx
			image: nginx:latest
			ports:
			- containerPort: 80
			readinessProbe:
			httpGet:
				path: /
				port: 80
			livenessProbe:
			httpGet:
				path: /
				port: 80

	```
	Understanding on readness and liveness probe
	```
	liveness prob is used to check if a port is live. the pod would restart if it could not establish a connection to the port. And readiness prob probs the port to see if it is ready to get the incomming traffic.

	```

## Cleanup task
Delete the namespace `my-namespace` 
