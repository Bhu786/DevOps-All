The problem described is that while **Horizontal Pod Autoscaler (HPA)** can increase the number of application pods during high traffic, those pods end up in a **Pending** state when the existing worker nodes lack the necessary CPU or memory capacity to host them (1:24 - 2:06).

The solution is to implement a **Cluster Autoscaler** (3:01). This component automatically monitors the cluster for pending pods and provisions additional worker nodes to provide the necessary capacity (3:09 - 3:15). 

**Key steps for implementation include:**
* **Prepare Environment:** Set up an *Amazon EKS* cluster with a managed worker node group (4:10).
* **IAM Configuration:** Enable an *IAM OIDC* provider and configure the necessary permissions to allow the autoscaler to manage EC2 instances (11:57 - 13:16).
* **Deployment:** Use *Helm* to deploy the Cluster Autoscaler, ensuring the `values.yaml` file is correctly configured with your cluster name, region, and scaling policies (14:10 - 22:24).
* **Verification:** Once installed, the autoscaler detects resource shortages, adds nodes automatically, and removes them when they are underutilized, which helps optimize costs (24:43 - 29:55).


The problem described is that while **Horizontal Pod Autoscaler (HPA)** can increase the number of application pods during high traffic, those pods end up in a **Pending** state when the existing worker nodes lack the necessary CPU or memory capacity to host them (1:24 - 2:06).

The solution is to implement a **Cluster Autoscaler** (3:01). This component automatically monitors the cluster for pending pods and provisions additional worker nodes to provide the necessary capacity (3:09 - 3:15). 

**Key steps for implementation include:**
* **Prepare Environment:** Set up an *Amazon EKS* cluster with a managed worker node group (4:10).
* **IAM Configuration:** Enable an *IAM OIDC* provider and configure the necessary permissions to allow the autoscaler to manage EC2 instances (11:57 - 13:16).
* **Deployment:** Use *Helm* to deploy the Cluster Autoscaler, ensuring the `values.yaml` file is correctly configured with your cluster name, region, and scaling policies (14:10 - 22:24).
* **Verification:** Once installed, the autoscaler detects resource shortages, adds nodes automatically, and removes them when they are underutilized, which helps optimize costs (24:43 - 29:55).


"
pod increase liken penbding me chala ja toh solution haio cluster autoscaler" yejhi  simple me 
