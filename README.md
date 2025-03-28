# OpenShift Cheat Sheet

A comprehensive cheat sheet for OpenShift, including basic and advanced commands, categorized for easier reference.


## Cluster and Project Management

| Command | Description |
|---------|-------------|
| `oc login https://homelab.ocp4.tayyabtahir.com --token=asd######` | Log in to OpenShift cluster |
| `oc loging -u tayyab -p password https://homelab.ocp4.tayyabtahir.com` | Log in to OpenShift cluster |
| `oc whoami` | View current user information |
| `oc config get-clusters` | List all clusters in the current kubeconfig |
| `oc status` | Get the status of the current project and cluster |
| `oc project <project-name>` | Switch to a different project/namespace |
| `oc get projects` | List all OpenShift projects |
| `oc new-project <project-name>` | Create a new project |
| `oc delete project <project-name>` | Delete a project |
| `oc adm policy add-cluster-role-to-user <role-name> <username>` | Assign a cluster role to a user |
| `oc adm policy remove-cluster-role-from-user <role-name> <username>` | Remove a cluster role from a user |

---
## Pod Management and Creation

| Command | Description |
|---------|-------------|
| `oc get pods` | List all pods in the current project |
| `oc describe pod <pod-name>` | Get detailed information about a specific pod |
| `oc logs <pod-name>` | View logs for a specific pod |
| `oc logs -f <pod-name>` | Follow logs of a specific pod in real-time |
| `oc logs <pod-name> -c <container-name>` | View logs of a specific container within a pod |
| `oc delete pod <pod-name>` | Delete a specific pod |
| `oc create -f <pod-file.yaml>` | Create a pod from a YAML file |
| `oc adm top pod <pod-name>` | View metrics (CPU, memory) of a specific pod |
| `oc rsh <pod-name>` | Open a remote shell inside a running pod |
| `oc port-forward <pod-name> <local-port>:<pod-port>` | Forward a port from a pod to your local machine |
| `oc exec -it <pod-name> -- <command>` | Execute a command inside a running pod |

---

## Deployment Management and Creation

| Command | Description |
|---------|-------------|
| `oc get deployments` | List all deployments |
| `oc describe deployment <deployment-name>` | Get detailed information about a specific deployment |
| `oc rollout status deployment/<deployment-name>` | Get the rollout status of a deployment |
| `oc set image deployment/<deployment-name> <container-name>=<image-name>:<tag>` | Update the image of a container in a deployment |
| `oc scale --replicas=<number> deployment/<deployment-name>` | Scale a deployment to a specific number of replicas |
| `oc rollout undo deployment/<deployment-name>` | Rollback to the previous version of a deployment |
| `oc expose deployment <deployment-name> --port=<port> --name=<service-name>` | Expose a deployment as a service |
| `oc set triggers dc/<deployment-config-name> --from-image=<image-name>:<tag>` | Set an image change trigger for a deployment config |
| `oc create -f <deployment.yaml>` | Create a deployment from a YAML file |
| `oc delete deployment <deployment-name>` | Delete a specific deployment |
| `oc autoscale deployment <deployment-name> --min=1 --max=10 --cpu-percent=80` | Create an autoscaler for a deployment |

---

## Service and Route Management

| Command | Description |
|---------|-------------|
| `oc get svc` | List all services in the current project |
| `oc describe svc <service-name>` | Get detailed information about a specific service |
| `oc get routes` | List all routes in the current project |
| `oc expose svc/<service-name> --hostname=<hostname>` | Expose a service as a route |
| `oc expose deployment <deployment-name> --port=<port> --name=<service-name>` | Expose a deployment as a service |
| `oc delete route <route-name>` | Delete a specific route |
| `oc get endpoints` | List all endpoints in the current project |
| `oc expose pod <pod-name> --port=<port> --name=<service-name>` | Expose a pod as a service |

---

## Storage and Secret Management

| Command | Description |
|---------|-------------|
| `oc get configmaps` | List all ConfigMaps in the current project |
| `oc create configmap <configmap-name> --from-file=<file-path>` | Create a ConfigMap from a file |
| `oc get secrets` | List all secrets in the current project |
| `oc create secret generic <secret-name> --from-file=<file-path>` | Create a secret from a file |
| `oc create secret generic <secret-name> --from-literal=<key>=<value>` | Create a secret from a literal value |
| `oc describe secret <secret-name>` | Get detailed information about a specific secret |
| `oc create secret docker-registry <secret-name> --docker-server=<registry-url> --docker-username=<username> --docker-password=<password>` | Create a Docker registry secret |
| `oc delete secret <secret-name>` | Delete a specific secret |
| `oc set volume deployment/<deployment-name> --add --name=<volume-name> --mount-path=<mount-path> --secret-name=<secret-name>` | Mount a secret as a volume to a deployment |
| `oc set volume pod/<pod-name> --add --name=<volume-name> --mount-path=<mount-path> --configmap=<configmap-name>` | Mount a configmap as a volume to a pod |

---


## Logs and Debugging

| Command | Description |
|---------|-------------|
| `oc logs <pod-name>` | View logs of a specific pod |
| `oc logs -f <pod-name>` | Follow logs of a pod in real-time |
| `oc get events --field-selector involvedObject.name=<pod-name>` | View events related to a specific pod |
| `oc describe pod <pod-name>` | Get detailed description of a pod for debugging |
| `oc run debug --rm -i --tty --image=<image-name> --command -- /bin/bash` | Start a debug pod with an interactive terminal |
| `oc debug pod/<pod-name> --image=<debug-image>` | Debug a running pod using a different image |

---

## Advanced Commands

| Command | Description |
|---------|-------------|
| `oc apply -f <file.yaml>` | Apply a YAML file to create or update resources |
| `oc delete <resource> -l <label-selector>` | Delete resources by label selector |
| `oc patch <resource> <resource-name> -p '{"spec":{"replicas":<number>}}'` | Patch a resource (e.g., change replica count for a deployment) |
| `oc create secret tls <secret-name> --cert=<cert-file> --key=<key-file>` | Create a TLS secret |
| `oc set resources pod <pod-name> --limits=cpu=<cpu-limit>,memory=<memory-limit>` | Set resource limits for a pod |
| `oc adm manage-node <node-name> --schedulable=false` | Mark a node as unschedulable (prevent new pods from being scheduled) |
| `oc create -f <buildconfig-file.yaml>` | Create a build configuration from a YAML file |
| `oc get clusteroperators` | List the status of all cluster operators |
| `oc set resources deployment/<deployment-name> --limits=cpu=<cpu-limit>,memory=<memory-limit>` | Set resource limits for a deployment |
| `oc adm upgrade` | Initiate an OpenShift cluster upgrade |
| `oc scale deployment/<deployment-name> --replicas=<num-replicas>` | Scale a deployment to a specific number of replicas |

---

## Build and Cron Jobs

| Command | Description |
|---------|-------------|
| `oc get buildconfigs` | List all build configurations |
| `oc create buildconfig -f <buildconfig-file.yaml>` | Create a build configuration from a YAML file |
| `oc start-build <buildconfig-name>` | Trigger a build manually |
| `oc get builds` | List all builds |
| `oc describe build <build-name>` | Get detailed information about a specific build |
| `oc logs build/<build-name>` | View logs for a specific build |
| `oc cancel-build <build-name>` | Cancel a specific build |
| `oc create cronjob <cronjob-name> --image=<image-name> --schedule="<cron-schedule>"` | Create a cron job for scheduled tasks |
| `oc describe cronjob <cronjob-name>` | Get detailed information about a specific cron job |
| `oc delete cronjob <cronjob-name>` | Delete a specific cron job |

---

## Role and Policy Management

| Command | Description |
|---------|-------------|
| `oc adm policy add-role-to-user <role-name> <username>` | Assign a role to a user within a project |
| `oc adm policy remove-role-from-user <role-name> <username>` | Remove a role from a user |
| `oc create rolebinding <role-binding-name> --role=<role-name> --user=<user-name>` | Create a role binding for a user |
| `oc delete rolebinding <role-binding-name>` | Delete a specific role binding |
| `oc get rolebindings` | List all role bindings in the current project |

---

## Node and Resource Management

| Command | Description |
|---------|-------------|
| `oc get nodes` | List all nodes in the cluster |
| `oc describe node <node-name>` | Get detailed information about a specific node |
| `oc adm top nodes` | View resource usage (CPU, memory) for each node in the cluster |
| `oc adm manage-node <node-name> --schedulable=false` | Mark a node as unschedulable (prevent new pods from being scheduled) |
| `oc adm manage-node <node-name> --schedulable=true` | Mark a node as schedulable (allow new pods to be scheduled) |
| `oc get resourcequotas` | List resource quotas for the current project |
| `oc describe resourcequota <quota-name>` | Get detailed information about a resource quota |
| `oc set resources deployment/<deployment-name> --requests=cpu=<cpu-request>,memory=<memory-request>` | Set resource requests for a deployment |

---


