**Lab 04 — ACR + AKS Secure Container Delivery (Managed Identity)**

 **Objectives**

This lab builds a secure container delivery workflow by using Azure Container Registry (ACR) as the trusted image source and Azure Kubernetes Service (AKS) as the runtime.

The goals were to:

* Build and store an image in ACR

* Deploy AKS (Free tier)

* Attach ACR to AKS using managed identity (RBAC)

* Deploy both external and internal services

* Validate controlled exposure (public vs private service endpoints)

 **Environment**

* Region: West US 2

* Resource Group: FortisAid-Lab04

* AKS Cluster: FortisAid-AKS

* ACR Name: fortisbabs

 **Architecture Diagram**

Add architecture diagram placeholder

Suggested diagram:
Developer → ACR (image) → AKS → External LB (public) + Internal LB (private)

**Step-by-Step Walkthrough**

**Step 1** — Create Resource Group

```bash
az group create
--name FortisAid-Lab04
--location westus2

az group show -n FortisAid-Lab04 -o table
```

**Step 2** — Create Azure Container Registry (Basic)

```bash
az acr create
--resource-group FortisAid-Lab04
--name fortisbabs
--sku Basic
--admin-enabled true

az acr show -n fortisbabs --query "{Name:name, SKU:sku.name, LoginServer:loginServer}" -o table
```

**Step 3** — Create Dockerfile

```bash
echo FROM nginx > Dockerfile
```

**Step 4** — Build and Push Image to ACR (ACR Build)

```bash
az acr build
--resource-group FortisAid-Lab04
--registry fortisbabs
--image sample/nginx:v1
--file Dockerfile
.
```

**Step 5** — Verify Repository and Tag

```bash
az acr repository list --name fortisbabs -o table
az acr repository show-tags --name fortisbabs --repository sample/nginx -o table
```

**Expected**:

* Repository: sample/nginx

* Tag: v1

**Step 6** — Create AKS Cluster (Portal)

Configuration that worked:

* Preset: Dev/Test

* Pricing tier: Free

* Region: West US 2

* Cluster name: FortisAid-AKS

* Networking: Azure CNI Overlay

* Node pool mode: System

* OS: Ubuntu

* Size: Standard_D2s_v6

* Node count: 1

* Availability zones: None

**Step 7** — Connect kubectl

```bash
az aks get-credentials
--resource-group FortisAid-Lab04
--name FortisAid-AKS
--overwrite-existing

kubectl get nodes
```

Expected: node status shows Ready

**Step 8** — Attach ACR to AKS (Managed Identity)

```bash
az aks update
-n FortisAid-AKS
-g FortisAid-Lab04
--attach-acr fortisbabs
```

This enables AKS to pull images from ACR without embedding registry credentials.

**Deploy Workloads (External + Internal)**

Image used:

fortisbabs.azurecr.io/sample/nginx:v1

**Step 9** — Deploy External LoadBalancer Service

Create a manifest called nginxexternal.yaml :

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginxexternal
spec:
replicas: 1
selector:
matchLabels:
app: nginxexternal
template:
metadata:
labels:
app: nginxexternal
spec:
containers:
- name: nginx
image: fortisbabs.azurecr.io/sample/nginx:v1
ports:
- containerPort: 80

apiVersion: v1
kind: Service
metadata:
name: nginxexternal
spec:
type: LoadBalancer
selector:
app: nginxexternal
ports:

port: 80
targetPort: 80
```

Apply and validate:

```bash
kubectl apply -f nginxexternal.yaml
kubectl get svc nginxexternal
```

Expected: External public IP assigned.

Test in browser:

```text
http://<EXTERNAL-IP>
```

Expected: Nginx default page loads.

**Step 10** — Deploy Internal LoadBalancer Service

Create a manifest called nginxinternal.yaml (content below):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginxinternal
spec:
replicas: 1
selector:
matchLabels:
app: nginxinternal
template:
metadata:
labels:
app: nginxinternal
spec:
containers:
- name: nginx
image: fortisbabs.azurecr.io/sample/nginx:v1
ports:
- containerPort: 80

apiVersion: v1
kind: Service
metadata:
name: nginxinternal
annotations:
service.beta.kubernetes.io/azure-load-balancer-internal: "true"
spec:
type: LoadBalancer
selector:
app: nginxinternal
ports:

port: 80
targetPort: 80
```

Apply and validate:

```bash
kubectl apply -f nginxinternal.yaml
kubectl get svc nginxinternal
```

Expected: Internal IP assigned (10.x.x.x)

**Step 11** — Validate Internal Access From Inside Cluster

Exec into a pod and curl the internal service:

```bash
POD=$(kubectl get pods -l app=nginxexternal -o jsonpath='{.items[0].metadata.name}')
kubectl exec -it $POD -- sh
```

Inside the pod:

```bash
curl http://nginxinternal

```

Expected: HTML returned successfully.

 **Challenges & Resolutions**
**Issue 1** — AKS System Node Pool Requirement

Problem: Cluster deployment failed when node pool mode was not System.
Resolution: Set node pool mode to System during AKS creation.

**Issue 2** — Availability Zone Restriction

Problem: Certain availability zone selections caused deployment failures.
Resolution: Set Availability zones to None for the successful build.

 **Outcomes**

* ACR successfully built and stored a container image

* AKS successfully pulled from ACR using managed identity (RBAC)

* External service exposed publicly via LoadBalancer

* Internal service restricted to private networking and validated from inside the cluster

 **Key Learnings**

* Managed identity attachment (--attach-acr) avoids credential sprawl

* Public vs private service exposure is a core AKS security control

* Internal LoadBalancers support private service access patterns aligned with zero-trust segmentation

**Extensions**

* Replace external LB with Ingress + WAF

* Add AKS network policies for east-west restriction

* Integrate Defender for Containers and image scanning

* Store manifests as versioned deployment assets

For screenshots and growth reflections, see my Medium post [link]
