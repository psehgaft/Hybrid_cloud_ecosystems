# Hybrid cloud ecosystems

> **CONTRIBUTORS: **Luis Santiagio Vazquez,

> **NOTE: This laboratory has specific research and innovation purposes, configurations are assumed and omitted, which is why it is not recommended for a productive environment.**

## Justification

Deploying microservices with a hybrid cloud microservices ecosystem strategy can offer several advantages that contribute to a more efficient deployment of these solutions. 

**Implementation Flexibility:**
The hybrid cloud strategy allows microservices to be deployed in different environments according to the specific needs of each service. This provides flexibility to leverage public cloud, private cloud, or on-premises environments depending on the performance, scalability, and security requirements of each microservice.

**Cost Optimization:**
Hybrid cloud offers the ability to select the most cost-effective deployment platform for each microservice. By leveraging public cloud resources when they are cost-effective and using on-premises resources for specific workloads, organizations can optimize infrastructure costs.

**Dynamic Scalability:**
Hybrid cloud strategy facilitates dynamic scalability of microservices. You can scale services individually based on demand, taking advantage of public cloud elasticity or on-premises scalability as needed.

**Unified Management:**
Unified management tools and platforms allow you to centrally manage microservices in different environments. This simplifies operational management and facilitates monitoring, diagnosis and troubleshooting.

**Improved Resilience:**
Distributing microservices across multiple environments improves system resilience. In the event of failures or interruptions in an environment, other microservices can continue to operate, ensuring service continuity.

**Regulatory Compliance and Security:**
Hybrid cloud addresses security and compliance considerations by deploying microservices in environments that meet specific requirements. Critical or regulated data can be handled locally, while other services can leverage the public cloud.

**Application Portability:**
The hybrid cloud strategy makes it easy to port applications between different deployment environments. This allows organizations to migrate and scale microservices as needed, without relying exclusively on one vendor or environment.

**Reducing Supplier Lockdown Risks:**
By diversifying deployment environments, you reduce the risks of vendor lock-in. Organizations can change providers or adjust their deployment strategy without compromising service continuity.


The hybrid cloud microservices ecosystem strategy provides a flexible and efficient architecture that adapts to the changing needs of microservices. 
It enables open industries to optimize costs, improve resilience, meet security requirements and ensure operational efficiency in an increasingly dynamic and diverse environment.

## Challenges

Implementing microservices offers numerous benefits, but also presents challenges and potential problems when an architectural framework of microservices as ecosystems is not established.
Some of the current problems when implementing microservices include:

1. Management Complexity:

Microservices present greater complexity in the management of multiple independent services, each with its own database and business logic. Coordinating and managing these pieces can be challenging.
`Reference: Lewis, J. and Fowler, M. (2014). Microservices: a definition of this new architectural term.`

2. Consistency and Distributed Transactions:

Maintaining data consistency in a microservices environment, especially in operations that involve distributed transactions, can be complicated and require specific solutions.
`Reference: Newman, S. (2015). Building microservices: detailed system design.`

3. Security and Data Protection:

Managing security in a microservices environment, involving multiple services and entry points, can be challenging. Data protection and authentication must be carefully considered.
`Reference: Richardson, C. (2018). Microservices security in action.`

4. Monitoring and Follow-up:

Tracking and monitoring distributed microservices can be complex. Specialized solutions are required to understand system-wide performance and issues.
`Reference: Burns, B. (2019). Distributed Systems Design: Patterns and Paradigms for Scalable and Reliable Services.`

5. Testing and Continuous Deployment:


Implementing effective testing and continuous deployment strategies for microservices can be more complicated than in monolithic architectures, especially given the need to test interactions between services.
`Reference: Newman, S. (2015). Building microservices: detailed system design.`

6. Cultural and Organizational Change:

Adopting a microservices architecture often involves a significant cultural and organizational change. Organizations must adapt to a small, independent team mentality.
`Reference: Fowler, M. and Lewis, J. (2018). Microservices: the dark side.`

7. Network Overload and Latency & Hybrid Cloud Balancing:

Communication between microservices can introduce latency, and a poorly designed architecture can result in network overload, affecting overall performance.
`Reference: Newman, S. (2015). Building microservices: detailed system design.`

8. Duplication of Functionalities and Waste of Resources:

Fragmentation of services can lead to duplication of functionality, which can result in wasted resources and development efforts.
`Reference: Richardson, C. (2018). Microservices Patterns: With examples in Java.`

It is important to address these problems with a strategic approach and consider specific solutions to mitigate the challenges associated with the implementation of microservices in an enterprise environment, which is why it is important to undertake research on microservices implementation that reduces the impact of the aforementioned problems. . .

## Architecture

```https://app.diagrams.net/#G1k04ZY8GSguBKeE2pBmFBMpn24OraFMvv
```

![Open Hybrid Ecosystems](./images/hybrid-microservices-ecosystems.png)



The lab consists of three Red Hat OpenShift Clusters.

1. Hub Cluster
2. Primary Cluster (OCP-01)
3. Secondary Cluster (OCP-01)

### AWS
This lab is designed to run on an OpenShift 4 cluster that has been completely installed by the new installer. You will need access to AWS with sufficient permissions and limits to deploy the 3 masters, 4-6 regular nodes,
and NVME-equipped nodes for storage.

Check out the
[documentation](https://docs.openshift.com/container-platform/latest/installing/installing_aws/installing-aws-default.html)
for _Installing on AWS_.

### OpenShift 4
At this time an OpenShift 4 cluster can be obtained by visiting
https://try.openshift.com -- a free "subscription" to / membership in the
developer program is required.

### Red Hat Advanced Cluster Management for Kubernetes

Red Hat Advanced Cluster Management for Kubernetes provides end-to-end management visibility and control to manage your Kubernetes environment. Take control of your application modernization program with management capabilities for cluster creation, application lifecycle, and provide security and compliance for all of them across hybrid cloud environments. Clusters and applications are all visible and managed from a single console, with built-in security policies. Run your operations from anywhere that Red Hat OpenShift runs, and manage any Kubernetes cluster in your fleet.

With Red Hat Advanced Cluster Management for Kubernetes:

1. Work across a range of environments, including multiple data centers, private clouds and public clouds that run Kubernetes clusters.
2. Easily create Kubernetes clusters and offer cluster lifecycle management in a single console.
3. Enforce policies at the target clusters using Kubernetes-supported custom resource definitions.
4. Deploy and maintain day-two operations of business applications distributed across your cluster landscape.

Red Hat Advanced Cluster Management (RHACM) provides the ability to manage multiple clusters and application lifecycles. Hence, it serves as a control plane in a multi-cluster environment.

1. RHACM is split into two parts:
2. RHACM Hub: components that run on the multi-cluster control plane.
Managed clusters: components that run on the clusters that are managed.

### OpenShift Data Foundation

OpenShift Data Foundation provides the ability to provision and manage storage for stateful applications in an OpenShift Container Platform cluster.

OpenShift Data Foundation is backed by Ceph as the storage provider, whose lifecycle is managed by Rook in the OpenShift Data Foundation component stack. Ceph-CSI provides the provisioning and management of Persistent Volumes for stateful applications.

OpenShift Data Foundation stack is now enhanced with the following abilities for disaster recovery:

1. Enable RBD block pools for mirroring across OpenShift Data Foundation instances (clusters)
2. Ability to mirror specific images within an RBD block pool
3. Provides csi-addons to manage per Persistent Volume Claim (PVC) mirroring

### OpenShift DR
Red Hat OpenShift Data Foundation Regional Disaster Recovery (Regional-DR) solution along with the steps and commands necessary to be able to failover an application from one OpenShift Container Platform cluster to another and then failback the same application to the original primary cluster.

Regional-DR is composed of Red Hat Advanced Cluster Management for Kubernetes and OpenShift Data Foundation components to provide application and data mobility across Red Hat OpenShift Container Platform clusters.

> **_NOTE:_** Regional-DR is supported with OpenShift Data Foundation 4.14 and Red Hat Advanced Cluster Management for Kubernetes 2.9 combinations only.

OpenShift DR is a set of orchestrators to configure and manage stateful applications across a set of peer OpenShift clusters which are managed using RHACM and provides cloud-native interfaces to orchestrate the life-cycle of an application’s state on Persistent Volumes. These include:

- Protecting an application and its state relationship across OpenShift clusters
- Failing over an application and its state to a peer cluster
- Relocate an application and its state to the previously deployed cluster

OpenShift DR is split into three components:

1. ODF Multicluster Orchestrator: Installed on the multi-cluster control plane (RHACM Hub), it orchestrates configuration and peering of OpenShift Data Foundation clusters for Metro and Regional DR relationships
2. OpenShift DR Hub Operator: Automatically installed as part of ODF Multicluster Orchestrator installation on the hub cluster to orchestrate failover or relocation of DR enabled applications.
3. OpenShift DR Cluster Operator: Automatically installed on each managed cluster that is part of a Metro and Regional DR relationship to manage the lifecycle of all PVCs of an application.

# Deploying the Lab Guide

Deploying the lab guide will take three steps. First, you will need to get
information about your cluster. Second, you will build a container based on your lab.
Third, you will deploy the lab guide using the information you found so that proper
URLs and references are automatically displayed in the guide.

## Requirements / Prerequisites

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services. Items marked with a ^ have already been implemented.

Most of the information can be found in the output of the installer.

<details>
<summary> ^ Requirements </summary>

* Python (3.5.3)
* awscli (1.11.109-2.fc25) Fedora
* click (6.7)
* pip (9.0.1)
* setuptools (36.2.4)
* wheel (0.30.0a0)
* ansible (7.7.0-1)

</details>

<details>
<summary> ^ Install packages </summary>

```sh
sudo dnf install -y ansible
sudo dnf install -y awscli awscli2
sudo dnf install -y python pip python3-wheel python3-click 
sudo dnf install -y setuptool
ansible-playbook submariner/submarinercli-install.yml
```
</details>
<details>
    
<summary> ^ Install the Skupper command-line tool </summary>

First, install the Skupper command-line tool on your Linux system.

```sh
curl https://skupper.io/install.sh | sh
```
</details>

<details>
<summary> ^ Required Environment Variables </summary>

#### Explaination and examples
- `API_URL` - URL to access API of the cluster
    - `https://api.cluster-gu1d.sandbox101.opentlc.com:6443`
- `MASTER_URL` - Master Console URL
    - `http://console-openshift-console.apps.cluster-gu1d.sandbox101.opentlc.com`
- `KUBEADMIN_PASSWORD` - Password for `kubeadmin`
- `SSH_PASSWORD` - password for ssh into bastion
- `ROUTE_SUBDOMAIN` - Subdomain that apps will reside on
    - `apps.cluster-gu1d.sandbox101.opentlc.com:6443`
    - `apps.mycluster.company.com`

Specific to Red Hat internal systems
- `GUID` - GUID
    - `gu1d`
- `BASTION_FQDN` - Bastion Domain Name
    - `bastion.gu1d.sandbox101.opentlc.com`

Create a file called `workshop-settings.sh` using the values of your environment. Here is an example.

> :warning: For `export` ensure [special characters](http://mywiki.wooledge.org/BashGuide/SpecialCharacters) are escaped (ie. use `\!` in place of `!`).

```bash
export API_URL=https://api.openshift4.example.com:6443
export MASTER_URL=https://console-openshift-console.apps.openshift4.example.com
export KUBEADMIN_PASSWORD=IqJK7-o3hYR-ZTr6c-7sztN
export SSH_USERNAME=lab-user
export SSH_PASSWORD=apassword
export BASTION_FQDN=foo.bar.com
export GUID=XXX
export ROUTE_SUBDOMAIN=apps.openshift4.example.com
export HOME_PATH=/opt/app-root/src
export USER=[asigned user]
export SUBMARINER-PATH="$PATH:~/.local/bin"
```
</details>

<details>
<summary> ^ Storage </summary>

Persistent storage requirement is key to many application and to achieve disaster recovery for such applications, data replication becomes very important. In this lab we will leverage Red Hat OpenShift Data Foundations Storage.

</details>

<details>
<summary> ^ Configure LAB </summary>

Now that you have the `workshop/workshop-settings.sh` file with the various required variables, you can deploy the lab guide into your cluster.

First, clone the repo:

> **_NOTE:_** Remember to checkout the branch you want to test against.

```shell
git clone https://github.com/openshiftdemos/openshift-ops-workshops
```

Next, Build a container using the repo/branch you checked out.

```shell
cd openshift-ops-workshops
export QUAY_USER=myusername
export BRANCH=$(git branch --show-current)
podman build -t quay.io/${QUAY_USER}/lab-hybrid-cloud-ecosystems:${BRANCH} .
```

Now, login to quay (it's free to sign up) or another registry your cluster has access to.

```shell
podman login quay.io
```

Next push your container to your repo.

```shell
podman push quay.io/${QUAY_USER}/lab-hybrid-cloud-ecosystems:${BRANCH}
```

You will use this image to deploy the lab. The following command will log you in as `kubeadmin` on systems with `oc` client installed:

```bash
oc login -u kubeadmin -p $KUBEADMIN_PASSWORD

oc new-project lab-ocp-hce

# This part is needed if you're running on a "local" or "self-provisioned" cluster
oc adm policy add-role-to-user admin kube:admin -n lab-ocp-hce

# Create deployment.
oc new-app -n lab-ocp-hce https://raw.githubusercontent.com/redhat-cop/agnosticd/development/ansible/roles/ocp4-workload-workshop-admin-storage/files/production-cluster-admin.json \
--param TERMINAL_IMAGE="quay.io/${QUAY_USER}/lab-hybrid-cloud-ecosystems:${BRANCH}" --param PROJECT_NAME="lab-ocp-hce" \
--param WORKSHOP_ENVVARS="$(cat ./workshop/workshop-settings.sh)"

# Wait for deployment to finish.

oc rollout status dc/dashboard -n lab-ocp-hce
```

If you made changes to the container image and want to refresh your deployed Homeroom quickly, execute this:

```shell
oc import-image -n lab-ocp-hce dashboard
```

</details>

<details>
<summary> ^ Doing and follow the lab </summary>

Your lab guide should deploy in a few moments. To find its url, execute:

```bash
oc get route dashboard -n lab-ocp-hce
```

You should be able to visit that URL and see the lab guide. From here you can
follow the instructions in the lab guide.

## Notes and Warnings
Remember, this experience is designed for a provisioning system internal to
Red Hat. Your lab guide will be mostly accurate, but slightly off.

* You aren't likely using `lab-user`
* You will probably not need to actively use your `GUID`
* You will see lots of output that references your `GUID` or other slightly off
  things
* Your `MachineSets` are different depending on the EC2 region you chose

But, generally, everything should work. Just don't be alarmed if something
looks mostly different than the lab guide.

Also note that the first lab where you SSH into the bastion host is not
relevant to you -- you are likely already doing the exercises on the host
where you installed OpenShift from.

Logon to the Hub Cluster ACM, OCP-01 and OCP-02 console using your OpenShift credentials.

Go to the OpenShift console and log in with your credentials username: admin and password: [PASSWORD] `DevNationDayDec12``

![OCP Login](./images/openshift-login.png)

</details>

<details>
<summary> Troubleshooting </summary>

Make sure you are logged-in as kubeadmin when creating the project

If you are getting _too many redirects_ error then clearing cookies and
re-login as kubeadmin. This usually happens if you're using RHPDS and
stopped/started a cluster.

</details>

<details>
<summary> Cleaning up </summary>

To delete deployment run
```
oc delete all,serviceaccount,rolebinding,configmap -l app=admin -n lab-ocp-hce
```
</details>

<details>
<summary> Get materials </summary>

First, clone the repo

> **NOTE** Remember to checkout the branch you want to test against

```shell
git clone https://github.com/psehgaft/Hybrid_cloud_ecosystems
```
</details>


## 1. Management Complexity

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services. Items marked with a ^ have already been implemented.

<details>
<summary> Hub cluster </summary>

The hub cluster is the common term that is used to define the central controller that runs in a Red Hat Advanced Cluster Management for Kubernetes cluster. From the hub cluster, you can access the console and product components, as well as the Red Hat Advanced Cluster Management APIs. You can also use the console to search resources across clusters and view your topology.

The Red Hat Advanced Cluster Management hub cluster uses the MultiClusterHub operator to manage, upgrade, and install hub cluster components and runs in the open-cluster-management namespace. The hub cluster aggregates information from multiple clusters by using an asynchronous work request model and search collectors. The hub cluster maintains the state of clusters and applications that run on it.

The local cluster is the term used to define a hub cluster that is also a managed cluster, discussed in the following sections.

</details>

<details>
<summary> Managed cluster </summary>

The managed cluster is the term that is used to define additional clusters that are managed by the hub cluster. The connection between the two is completed by using the klusterlet, which is the agent that is installed on the managed cluster. The managed cluster receives and applies requests from the hub cluster and enables it to service cluster lifecycle, application lifecycle, governance, and observability on the managed cluster.

</details>

<details>
<summary> Cluster lifecycle </summary>

Red Hat Advanced Cluster Management cluster lifecycle defines the process of creating, importing, managing, and destroying Kubernetes clusters across various infrastructure cloud providers, private clouds, and on-premises data centers.

The cluster lifecycle function is provided by the multicluster engine for Kubernetes operator, which is installed automatically with Red Hat Advanced Cluster Management. See Cluster lifecycle introduction for general information about the cluster lifecycle function.

</details>

<details>
<summary> Implementation objetives </summary>

You can use either the OpenShift 4 web console's built-in OperatorHub or the OpenShift CLI to install ACM. The installation breaks down to six steps:

1. Prepare the environment for the ACM installation.
2. Create a new OpenShift project and namespace.
3. Create an image-pull secret.
4. Install ACM and subscribe to the ACM Operator group.
5. Create the MultiClusterHub resource.
6. Verify the ACM installation.

These steps are already executed for you during the lab setup except for the application onboarding which is the next lab.

1. *Install the ACM operator on the hub cluster:* After creating the OCP hub cluster, install from OperatorHub the ACM operator. After the operator and associated pods are running, create the MultiClusterHub resource.

2. *Create or import managed OCP clusters into ACM hub:* Import or create the two managed clusters with adequate resources for ODF (compute nodes, memory, cpu) using the RHACM console.

3. *Ensure clusters have unique private network address ranges:* Ensure the primary and secondary OCP clusters have unique private network address ranges.

</details>

<details>
<summary> ^ Deploy Advanced Cluster Management for Kubernetes </summary>

We will use the OpenShift command line for the first several steps; . then, I will show you how to use either the command line or the OpenShift 4 web console.

```vars.yml
ansible-playbook lab-deployment.yml --tags acm
```
</details>

<details>
<summary> ^ Cluster Lifecycle </summary>

At a high level Cluster Lifecycle management is about creating, upgrading, and destroying and importing clusters in a multi cloud environment.

AWS credentials:
- Access Key ID
- Secret Access Key
- Base DNS Domain.  

In order to create a new OpenShift cluster in the AWS cloud we will need these keys to create a Provider Connection. On the left bar, select Credentials and then select Add Credential.

```![ACM add credential](./images/ACM-add-credential.png) #TODO#
```

You will need to provide connection details:

**Credential Type:** Choose *Amazon Web Services* and then, *Amazon Web Services* again
**Credential Name:**  aws
**Namespace:** open-cluster-management
**Base DNS Domain:**  This is in the email from the RHDP system

Click NEXT

**Access Key ID:**  This is in the email from the RHDP system
**Secret Access Key ID:** This is in the email from the RHDP system

Click NEXT - We don’t need to configure a Proxy

**Red Hat OpenShift pull secret:** Get from your [Red Hat login](https://cloud.redhat.com/openshift/install/pull-secret)
*SSH private and public keys(optional):*  ~/.ssh/id_rsa

Click NEXT, verify the information and click ADD

</details>

<details>
<summary> ^ Create a new OpenShift clusters in AWS </summary>

**OCP-01**

From the *Clusters* page, select *Create Cluster*
Select *Amazon Web services* and then *Standalone*.
Select the *Infrastructure provider credential*: aws (may be already selected)
**Name:** primary (OCP-01) 
Leave the *Cluster set empty for now*
Select a *Release Image*, chose a 4.14 version
Add a label of *environment=prod*. 

Click NEXT

Change the region to *(Select us-west-1 or us-west-2)*

**OCP-02**

From the *Clusters* page, select *Create Cluster*
Select *Amazon Web services* and then *Standalone*.
Select the *Infrastructure provider credential*: aws (may be already selected)
**Name:** primary (OCP-02) 
Leave the *Cluster set empty for now*
Select a *Release Image*, chose a 4.14 version
Add a label of *environment=prod*. 

Click NEXT

Change the region to *(Select us-west-1 or us-west-2)*

```![ACM add cluster](./images/ACM-add-credential.png) #TODO#
```

</details>

<details>
<summary> ^ Importing clusters </summary>

Click on Add *Cluster* --> *Import Clusters*.

Under labels make sure you add the environment=dev label as a label example.

Please note that the name you use for the cluster is not relevant, but it makes sense to use the actual cluster name in a production environment. 

Once finished click *NEXT*, *NEXT* and *GENERATE CODE*.


```![ACM import cluster](./images/ACM-add-credential.png) #TODO#
```

Once complete, select *COPY COMMAND*

```![ACM import cluster copy command](./images/ACM-add-credential.png) #TODO#
```

From a terminal, login to the target Kubernetes cluster you want to import.  Then paste and run the command you just copied.

Navigate back to ACM and wait for the cluster to become available (should be no more than 5 to 10 minutes).

</details>

<details>
<summary> Verify </summary>

Select All Clusters and verify that you can see local and two managed clusters - primnary and secondary

![ACM all clusters](./images/ACM-all-cluster-hub.png)

</details>

<details>
<summary> Application Lifecycle </summary>


Application Lifecycle functionality in RHACM provides the processes that are used to manage application resources on your managed clusters. This allows you to define a single or multi-cluster application using Kubernetes specifications, but with additional automation of the deployment and lifecycle management of resources to individual clusters. An application designed to run on a single cluster is straightforward and something you ought to be familiar with from working with OpenShift fundamentals. A multi-cluster application allows you to orchestrate the deployment of these same resources to multiple clusters, based on a set of rules you define for which clusters run the application components.

The table below describes the different components that the Application Lifecycle model in RHACM is composed of:

Resource | Purpose 
| :---: | :---: |
Channel  | Defines a place where deployable resources are stored, such as an object store, Kubernetes namespace, Helm repository, or GitHub repository. 
Subscription | Definitions that identify deployable resources available in a Channel resource that are to be deployed to a target cluster.
Placement - (Old PlacementRule API to be deprecated soon) | Defines the target clusters where subscriptions deploy and maintain the application. It is composed of Kubernetes resources identified by the Subscription resource and pulled from the location defined in the Channel resource.
Application | A way to group the components here into a more easily viewable single resource. An Application resource typically references a Subscription resource.

These are all Kubernetes custom resources, defined by a *Custom Resource Definition (CRD)*, that are created for you when RHACM is installed. 
By creating these as Kubernetes native objects, you can interact with them the same way you would with a Pod. 
For instance, running oc get application retrieves a list of deployed RHACM applications just as:

```sh
oc get pods
```

Retrieves a list of deployed Pods.

This may seem like a lot of extra resources to manage in addition to the deployables that actually make up your application. 
However, they make it possible to automate the composition, placement, and overall control of your applications when you are deploying to many clusters. 
With a single cluster, it is easy to log in and run:

```sh
oc create -f <file-name>.yml
```

If you need to do that on a dozen clusters, you want to make sure you do not make a mistake or miss a cluster, and you need a way to schedule and orchestrate updates to your applications. 
Leveraging the Application Lifecycle Builder in RHACM allows you to easily manage multi-cluster applications.


</details>


## 2. Consistency and Distributed Transactions

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services. Items marked with a ^ have already been implemented.

<details>
<summary> Implementation objetives </summary>

These steps are already executed for you during the lab setup except for the application onboarding which is the next lab.

1. *Connect the private networks using Submariner add-ons:* Connect the managed OCP private networks (cluster and service) using the RHACM Submariner add-ons.

2. *Install ODF 4.14 on managed clusters:* Install ODF 4.12 on primary and secondary OCP managed clusters and validate deployment.

3. *Install ODF Multicluster Orchestrator on the ACM hub cluster:* Install from OperatorHub on the ACM hub cluster the ODF Multicluster Orchestrator. The OpenShift DR Hub operator will also be installed.

4. *Configure SSL access between S3 endpoints:* If managed OpenShift clusters are not using valid certificates this step must be done by creating a new user-ca-bundle ConfigMap that contains the certs.

</details>

<details>
<summary> ^ Deploy Submariner </summary>

```sh
sudo dnf install -y ansible
sudo dnf install -y awscli awscli2
sudo dnf install -y python pip python3-wheel python3-click 
sudo dnf install -y setuptool
ansible-playbook submariner/submarinercli-install.yml
```
</details>

<details>
<summary> Validate non-overlapping networks </summary>

In [OCP-01] and [OCP-02] we validate:

```sh
oc get networks.config.openshift.io cluster -o json | jq .spec
```
Example output

```shell
{
  "clusterNetwork": [
    {
      "cidr": "10.128.0.0/14",
      "hostPrefix": 23
    }
  ],
  "externalIP": {
    "policy": {}
  },
  "networkType": "OpenShiftSDN",
  "serviceNetwork": [
    "172.30.0.0/16"
  ]
}
```

Now that we know the cluster and service networks have non-overlapping ranges, it is time to verify the Submariner add-ons for each managed cluster.

</details>

<details>
<summary> Verify that the Managed clusters using Submariner add-ons </summary>

Navigate on All Cland Click *ALL CLUSTERS* > *InfraSturcture* > *Clusters*.
Select *Cluster Sets* tab and in *cluster sets* select *clusterset1* and *Submariner add-ons tab*. 
A successful deployment will show Connection status and *Agent status* as *Healthy* for both *OCP-01* and *OCP-02*.

![ACM Submariner add-on](./images/ACM-Submariner-addon-installed.png)

</details>

## 3. Security and Data Protection

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services. Items marked with a ^ have already been implemented.

<details>
<summary> Governance </summary>

Governance enables you to define policies that either enforce security compliance, or inform you of changes that violate the configured compliance requirements for your environment. Using dynamic policy templates, you can manage the policies and compliance requirements across all of your management clusters from a central interface.

</details>

<details>
<summary> ^ Deploy Advanced Cluster Security for Kubernetes </summary>

When RHACM is available, you can create RHACM policies to deploy RHACS to your cluster fleet. This approach ensures that all fleet clusters are protected by RHACS.

To implement RHACS, you must create two policies in RHACM, one for centralized services and one for protected cluster services. The policy to install centralized services must be applied to the hub cluster. The policy for installing protected cluster services must be applied to the clusters that you want RHACS to protect. You can achieve this separation by using a clusterSelector parameter of the PlacementRule object.

```vars.yml
ansible-playbook lab-deployment.yml --tags acs
```
</details>

<details>
<summary> Disaster recovery </summary>

Organizations running critical applications on Red Hat OpenShift Container Platform need a business continuity plan for site and regional disasters that goes beyond cluster failover or backup and recovery. Your implementation should provide data resiliency and take into account continuous application deployment practices as part of overall enterprise GitOps strategies.

Disaster recovery (DR) helps an organization recover and resume business-critical functions or normal operations when there are disruptions or disasters.

1. We will use an application part of the OpenE-Comerce ecosystem that sells products online.
You will learn how to deploy and configure this application for business continuity.
2. We will test data persistence in failover/relocation (failback) scenarios by updating the data in the database. Verify that data is consistent and available after transition from one site/cluster to another.
3. We incorporated a sample application to be part of the disaster recovery strategy and test failover/relocation (failback).

Regional-DR is composed of Red Hat Advanced Cluster Management for Kubernetes and OpenShift Data Foundation components to provide application and data mobility across Red Hat OpenShift Container Platform clusters.

</details>

<details>
<summary> Implementation objetives </summary>

These steps are already executed for you during the lab setup except for the application onboarding which is the next lab.

1. *Create one or more DRPolicy:* Use the All Clusters Data Services UI to create DRPolicy by selecting the two managed clusters the policy will apply to.

2. *Validate OpenShift DR Cluster operators are installed:* Once the first DRPolicy is created this will trigger the DR Cluster operators to be created on the two managed clusters selected in the UI.

3. *failover/relocate:* Setup an application using RHACM console and test failover/relocate.

</details>

<details>
<summary> ^ Deploy Openshift Data Protection </summary>

When RHACM is available, you can create RHACM policies to deploy RHACS to your cluster fleet. This approach ensures that all fleet clusters are protected by RHACS.

To implement RHACS, you must create two policies in RHACM, one for centralized services and one for protected cluster services. The policy to install centralized services must be applied to the hub cluster. The policy for installing protected cluster services must be applied to the clusters that you want RHACS to protect. You can achieve this separation by using a clusterSelector parameter of the PlacementRule object.

```vars.yml
ansible-playbook lab-deployment.yml --tags oadp
```
</details>

<details>
<summary> ^ Backup </summary>

This is necessary so that metadata can be stored on the alternate cluster in a Multi-Cloud Gateway (MCG) object bucket using a secure transport protocol and in addition the Hub cluster needs to verify access to the object buckets.

> **_NOTE:_** If all of your OpenShift clusters are deployed using signed and valid set of certificates for your environment then this specific step can be skipped during implementation.

</details>

<details>
<summary> Validate OpenShift Data Foundation </summary>

In [OCP-01] and [OCP-02] we validate:

Validate the successful deployment of ODF on each managed OCP cluster with the following command:

```sh
oc get storagecluster -n openshift-storage ocs-storagecluster -o jsonpath='{.status.phase}{"\n"}'
```

Validate Multi-Cluster Gateway (MCG) status:

```sh

oc get noobaa -n openshift-storage noobaa -o jsonpath='{.status.phase}{"\n"}'
```
</details>

<details>
<summary> Validate ODF Multicluster Orchestrator Operator on Hub cluster </summary>

Check to see the following operators Pod are in a Running state. You may also see other operator pods which are not related to Regional DR configuration.

For Hub:

```sh
oc get pods -n openshift-operators
```
</details>

<details>
<summary> Validate Data Policy on Hub cluster </summary>

On the Hub cluster navigate and select *All Clusters* > *Data policies* under Data services menu. 
If this your first DRPolicy created you will see *Create* DRpolicy at the bottom of the page, else you will the the already created DRPolicy.

> **_NOTE:_** Make sure you can access all clusters from the *Multicluster Web console*. The clusters will be directly below All Clusters.

Click on Data policies and review the already created drpolicy.


```sh
oc get pods -n openshift-operators
```

![ACM DR policy selections](./images/MCO-drpolicy-selections.png)

Note that the Replication policy will automatically be selected as async based on the OpenShift clusters selected and a Sync schedule will be available. The replication interval for this dr policy is 5 minutes. You can check by clicking 3 dots on the right side of *drsync5m* data policy and select Edit DR Policy. Please do not update anything here, once you review the content of the yaml file, just cancel the selection so that there is no update to the DR Policy.

- Creating a new DR Policy also creates the two DRCluster resources and also the DRPolicy on the Hub cluster. In addition, when the initial DRPolicy is created the following will happen:

- Create a bootstrap token and exchanges this token between the managed clusters.

- Enable mirroring for the default CephBlockPool on each managed clusters.

- Create a *VolumeReplicationClass* on the *OCP-01 managed cluster* and the *OCP-02 Secondary managed cluster* for the replication interval in the DRPolicy.

- An object bucket created (using MCG) on each managed cluster for storing *PVC* and *PV* metadata.

- A *Secret* created in the openshift-operators project on the *Hub cluster* for each new object bucket that has the base64 encoded access keys.

- The ramen-hub-operator-config *ConfigMap* on the *Hub cluster* is modified with s3StoreProfiles entries.

- The OpenShift DR Cluster operator will be deployed on each managed cluster in the openshift-dr-system project.

- The object buckets *Secrets* on the *Hub cluster* in the project openshift-operators will be copied to the managed clusters in the openshift-dr-system project.

- The s3StoreProfiles entries will be copied to the managed clusters and used to modify the ramen-dr-cluster-operator-config *ConfigMap* in the openshift-dr-system project.

To validate that the *DRPolicy* is created successfully run this command on the *Hub cluster* for the each *Data Policy* resource created.

> **_NOTE:_** Replace <drpolicy_name> with your unique name.

For Hub (drpolicy name is <policy_name>):

```sh
oc get drpolicy <policy_name> -o jsonpath='{.status.conditions[].reason}{"\n"}'
```

To validate object bucket access from the *Hub cluster* to both the *OCP-1 Primary managed cluster* and the *OCP-02 Secondary managed cluster* first get the names of the DRClusters on the *Hub cluster*.

Now test S3 access to each bucket created on each managed cluster using this DRCluster validation command.

> **_NOTE:_** Replace <drcluster_name> with your unique name.

```sh
oc get drcluster <drcluster_name_OCP-01> -o jsonpath='{.status.conditions[2].reason}{"\n"}'

oc get drcluster <drcluster_name_OCP-02> -o jsonpath='{.status.conditions[2].reason}{"\n"}'
```

> **_NOTE:_** Make sure to run command for both *DRClusters* on the *Hub cluster*.

To validate that the OpenShift DR Cluster operator installation was successful on the *OCP-01 Primary managed cluster* and the *OCP-02 Secondary managed cluster* check for *CSV* *odr-cluster-operator* and pod *ramen-dr-cluster-operator* by running the following command:

*On OCP-01 and OCP-02*

```sh
oc get csv,pod -n openshift-dr-system
```

You can also go to *OperatorHub* on each of the managed clusters and look to see the OpenShift DR Cluster Operator is installed.

![ACM ODF cluster operator](./images/ODR-412-Cluster-operator.png)

Validate the status of the ODF mirroring daemon health on the Primary managed cluster and the Secondary managed cluster.

*On OCP-01 and OCP-02*

```sh
oc get cephblockpool ocs-storagecluster-cephblockpool -n openshift-storage -o jsonpath='{.status.mirroringStatus.summary}{"\n"}'
```

> **_NOTE:_** It could take up to 10 minutes for the daemon_health and health to go from Warning to OK. If the status does not become OK eventually then use the ACM console to verify that the Submariner connection between managed clusters is still in a healthy state.

</details>

## 4. Monitoring and Follow-up

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services. Items marked with a ^ have already been implemented.

<details>
<summary> Observability </summary>

The Observability component collects and reports the status and health of the OpenShift Container Platform version 4.x or later, managed clusters to the hub cluster, which are visible from the Grafana dashboard. You can create custom alerts to inform you of problems with your managed clusters. Because it requires configured persistent storage, Observability must be enabled after the Red Hat Advanced Cluster Management installation.

</details>

<details>
<summary> ^ Deploy Openshift Monitoring </summary>

```vars.yml
ansible-playbook lab-deployment.yml --tags acs
```
</details>
<details>
<summary> ^ Deploy Openshift Logging </summary>

```vars.yml
ansible-playbook lab-deployment.yml --tags acs
```
</details>
<details>
<summary> ^ Deploy Thanos </summary>

```vars.yml
ansible-playbook lab-deployment.yml --tags thanos
```
</details>
<details>
<summary> ^ End to End Visibility </summary>

View system alerts, critical application metrics, and overall system health. Search, identify, and resolve issues that are impacting distributed workloads using an operational dashboard designed for Site Reliability Engineers (SREs).  This is done via the integration of Grafana.  Let's walk through the steps to integrate Grafana with ACM.

- You will need your AWS Keys. 
- You will also need to create an AWS S3 bucket.
- SSH information to your bastion host.

**Create the S3 bucket**
- Login to the bastion host.
- Run the following command to login to AWS:  *aws configure*  and enter your AWS keys when prompted.  
-- Default region: *us-east-2*
- Then run the following command to create the S3 bucket:  
```sh
aws s3 mb s3://grafana-$GUID
```
- Please take note of the bucket name.

**Integrate Grafana into ACM**

- Login to the bastion host host.
- Create a namespace by running the following command:  
```sh
oc create namespace open-cluster-management-observability
```
Copy the pull secret into this new namespace by running the following TWO commands:  
```sh
PODMAN_CONFIG_JSON=`oc extract secret/pull-secret -n openshift-config --to=-` 

oc create secret generic multiclusterhub-operator-pull-secret -n open-cluster-management-observability --from-literal=.dockerconfigjson="$PODMAN_CONFIG_JSON" --type=kubernetes.io/dockerconfigjson
```

- In your current folder create a file called *thanos-object-storage.yaml*  and add the following text in the file. `Please be sure to update your S3 bucket name and AWS Keys`.

- Create a secret for your object storage by running the following command: 

```sh
oc create -f thanos-object-storage.yaml -n pen-cluster-management-observability
```

- Create the *MultiClusterObservability* custom resource for your managed clusters.  To do this create a  YAML file named multiclusterobservability_cr.yaml

- Apply the observability YAML to your cluster by running the following command:

```sh
oc apply -f multiclusterobservability_cr.yaml
```

- Log in to the ACM console, and navigate to *Observe environments -> Overview.*
- Click on the Grafana link in the top right to view the metrics from the managed clusters.  `Please note: it will take a few minutes for the metrics to become visible on the dashboard.`

```IMAGE TODO
```

You should shortly see something like the below

```IMAGE TODO
```

</details>

## 5. Testing and Continuous Deployment

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services. Items marked with a ^ have already been implemented.

<details>
<summary> Implementation objetives </summary>

These steps are already executed for you during the lab setup except for the application onboarding which is the next lab.

1. Create an application using RHACM console for highly available application across regions.

2. Test failover and reolcate operations using the sampole application between managed clusters.

</details>

<details>
<summary> Create Application On Primary </summary>

**Go to the Hub OpenShift console.**

This is a kubernetes platform from which you can create containerized applications. Part of this environment is the Red Hat Advanced Cluster Management (RHACM) platform along with Red Hat Openshift Disaster Recovery with ODF.

1. To get started, you will need to access the RHACM plaftorm by clicking local-cluster from the left menu and then selecting All Clusters.

2. Upon clicking the All Cluster option, you will be redirected to the RHACM console displaying your available clusters. There are 3 clusters available:

    i. *local-cluster:* This is your management cluster where you will create, failover and relocate your application.

    ii. *primary:* Your main cluster where your applications are initially deployed to.

    iii. secondary: Your backup cluster where your applications are failed over to.

3. You will now need to create your application which we will use in this workshop. Click on *Applications* on the left menu and click* Create application→Subscription*.

4. Once in the Create application wizard, enter the following details:

Name: globex
Namespace: globex
Under Repository location for resources:
    Repository Types: Git
    URL: https://github.com/psehgaft/globex.git
    Branch: main    
    Under Select clusters for application deployment:
        Select Deploy application resources on clusters with all specified labels
            Label: name
            Value: primary
    Click Create on the top right to create your application. This should create an ACM application subscription which in turn creates a Helm release which will deploy your application to the primary cluster.

5. Go back to Applications and search for globex-app. This is where you will see the app deployment topology. Following are not part of existing deployment and hence not deployed. Hence they will be marked as not available: acivity-tracking, order-placement and recommendation-engine. The app is focused on catalog, inventor and UI.

**Go to the Primary OpenShift OCP-01**

1. Once logged in click *Networking→Routes* on the left menu. Ensure your selected project is *globex* and then click on the *Location* link of the *globex-ui* route. (Keep the route)

2. Once you’ve clicked the link you will be redirected to globex online store front end. Select *Cool Stuff Store* at the top of the page.

3. You are now going to get the route of globex-ui, copy and paste in a browser window to get the coolstore app UI. This is the same route you can see from previous step by login to OpenShift Console:

```sh
oc get route -n globex | grep globex-ui
```
4. A list of store items will be presented to you. Take note of the price of the first item Quarkus T-shirt. Later you will change the price before you initiate a failover and ensure that the new price carries over to the secondary cluster.

</details>

<details>
<summary> Failover Application To Secondary </summary>

**Go to the primary OpenShift OCP-01**

1. You are now going to make an update to the price of one of the globex store items. This data is stored in a postgres database attached to a PVC which we will preserve during the failover. Update the price by running the below commands:

```sh
POD=$(oc get pods -n globex | grep catalog-database | awk '{print $1}')
oc exec -it $POD -n globex -- psql --dbname catalog --command "update catalog set price = 15 where name = 'Quarkus T-shirt';"
```
2. Switch back to the Globex application and refresh the page. Select the last page (6) and notice that the price of the Quarkust T-shirt is now $15.00

3. Return to the RHACM Hub console and then click Data *Services→Data policies* from the left menu.

4. Click on the 3 dots on the *drsync5m* disaster recovery policy and select *Apply DRPolicy*.

5. On the *Apply DRPolicy* popup, select the globex application and under *PVC label* enter *app=globex*. These options allow the globex application to be included in the DR policy and preserves any PVC’s with a label matching *app=globex*, in our case the PVC associated with the postgres database containing our prices. Click *Apply*.

**Go to the secondary OpenShift OCP-02**

1. You will now need to create the globex namespace in the secondary cluster and annotate it with the globex subscription name.

```sh
oc new-project globex || oc project globex
oc annotate ns globex --overwrite=true apps.open-cluster-management.io/hosting-subscription=globex/globex-subscription-1
```

2. Switch back to the RHACM console and select *Applications* and filter on *Subscription*. Click the 3 dots at the end of the globex application and select *Failover application*.

3. Provide the following details on the popup:

    a. *Select policy*: drsync5m
    b. *Target cluster*: secondary
    c. *Select subscriptions group*: globex-subscription-1
    d. Click Initiate

> **_NOTE:_** The subscription group may not be in a ready state to select. Wait a few minutes and try again.

**Go to the primary OpenShift OCP-01**

1. In the globex namespace will start terminating as the app starts failing over. Also check that the PVC will be in terminating state as well. Ensure that PVC is terminated and not visible on the primary. Review the status of the pvc (terminating) and the cephblockpool on primary. The health may be temporary in warning state and then goes back to healthy state:

```sh
oc get cephblockpool ocs-storagecluster-cephblockpool -n openshift-storage -o jsonpath='{.status.mirroringStatus.summary}{"\n"}'
```

2. Check the pvc’s (persistent volumen claims) being terminated and eventually disappears.

```sh
oc get pvc -n globex
```

**Go to the secondary OpenShift OCP-02**

1. Click *Workloads→Pods* on the left menu. Ensure your selected project is globex. Notice that the application pods have been recreated in this namespace.

2. Next, click *Networking→Routes* on the left menu and then click on the Location link of the *globex-ui* route.

3. Once you’ve clicked the link you will be redirected to globex online store front end. Select *Cool Stuff Store* at the top of the page.

4. You are now going to get the route of globex-ui and copy the route for example globex-ui-globex.apps.cluster-flxz7-2.sandbox2418.opentlc.com and paste in a browser window to get the coolstore app UI. This is the same route you can see from previous step by login to OpenShift Console:

```sh
oc get route -n globex | grep globex-ui
```

5. On the Coolstore Globex UI, select the last page (6) and notice that the price of the Quarkust T-shirt is $15.00. Our data from the primary cluster has been preserved during the failover.

6. Review the status of the pvc and the cephblockpool on secondary. The health may be temporary in warning state and then goes back to healthy state. You may also see *states:map[replaying:2]:*

```sh
oc get cephblockpool ocs-storagecluster-cephblockpool -n openshift-storage -o jsonpath='{.status.mirroringStatus.summary}{"\n"}'
```

```sh
oc get pvc -n globex
```

> **_NOTE:_** For production environment or real life scenario, the applications routes will be updated in Global Load Balancer using automated way for e.g. using ansible to update GLB’s with the new updated routes post failover / relocate.

</details>

<details>
<summary> Relocate Application To Primary </summary>

You will now attempt to relocate/failback the application to the primary cluster. Before we do that, we want to ensure that any changes made on the secondary cluster are preserved when relocating back to the primary cluster.

**Go to the secondary OpenShift OCP-02**

1. You are again going to make an update to the price of the Quarkus T-shirt. Update the price by running the below commands:

```sh
POD=$(oc get pods -n globex | grep catalog-database | awk '{print $1}')
oc exec -it $POD -n globex -- psql --dbname catalog --command "update catalog set price = 20 where name = 'Quarkus T-shirt';"
```

2. Confirm if the price has updated to by switching back to the Globex application on the secondary cluster and refresh the page. Select the last page (6) and notice that the price of the Quarkust T-shirt is now $20.00

3. Go back to the Hub Cluster RHACM console and select *Applications* and filter on *Subscription*. 

4. Click the 3 dots at the end of the globex application and select *Relocate application*.

5. Provide the following details on the popup:

    a. *Select policy:* drsync5m
    b. *Target cluster:* primary
    c. *Select subscriptions group:* globex-subscription-1
    s. Click Initiate

6. You will notice that the pods on the secondary cluster in the globex namespace will start terminating as the app starts relocating back to the primary cluster.

7. Review the status of the pvc and the cephblockpool on secondary. The health may be temporary in warning state and then goes back to healthy state. You may also see states:map[replaying:2]:

```sh
oc get cephblockpool ocs-storagecluster-cephblockpool -n openshift-storage -o jsonpath='{.status.mirroringStatus.summary}{"\n"}'
```

**Go to the primary OpenShift OCP-01**

1. Click *Workloads→Pods* on the left menu. Ensure your selected project is globex. Notice that the application pods have been recreated in this namespace. You will see the pods in primary once all the pvc’s complete termination in secondary cluster.

2. Once you’ve clicked the link you will be redirected to globex online store front end. Select Cool Stuff Store at the top of the page.

3. Select the last page (6) and notice that the price of the Quarkust T-shirt is still $20.00.

4. Review the status of the pvc (terminating) and the cephblockpool on primary. The health may be temporary in warning state and then goes back to healthy state:

```sh
oc get cephblockpool ocs-storagecluster-cephblockpool -n openshift-storage -o jsonpath='{.status.mirroringStatus.summary}{"\n"}'


oc get pvc -n globex
```

</details>

## 6. Cultural and Organizational Change

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services. Items marked with a ^ have already been implemented.

The importance of industry verticals can vary depending on the context, region, and the current economic and technological landscape. However, here we will focus on a list of some of the diverse and historically important industrial sectors that have played an important role in economies around the world:

<details>
<summary> Open industries </summary>

0. **(Open Ecosistems services) Generic/Cross microservices:** Generic and cross microservices, common services to energize the ecosystems of the industries.

1. **(Open IT and Open AI) Technology and IT:** This sector includes hardware, software, telecommunications and Internet-related companies. It has been a major driver of economic growth and innovation in recent decades.

2. **(Open Banking) Finance and banking:** The financial industry encompasses banks, insurance companies, investment companies and more. It plays a crucial role in managing money and providing financial services.

3. **(Open Insurance) Healthcare:** Healthcare includes hospitals, pharmaceutical companies, biotechnology companies, and medical device manufacturers. It is essential to maintain public health and well-being.

4. **(Open Energy) Energy:** This sector involves the production, distribution and consumption of energy resources, including oil, gas, renewable energy sources and utilities.

5. **(Open Manufacturing) Manufacturing:** Manufacturing covers a wide range of industries, from automotive and aerospace to the production of consumer electronics and heavy machinery.

6. **(Open Agriculture) Agriculture and Food:** This sector includes agriculture, food processing and distribution. It is essential to feed the world population.

7. **(Open Transportation and logistics) Transportation and logistics:** Transportation and logistics covers everything from shipping and freight to airlines and public transportation systems.

8. **(Open E-Commerce) Retail:** Retail businesses encompass physical stores and e-commerce platforms, which sell a variety of products to consumers.

9. **(Open Real Estate) Real Estate:** Real estate includes residential, commercial and industrial properties, as well as property development and management.

10. **(Open Media and Entertainment) Entertainment and media:** This sector covers film, television, music, publishing, games and other forms of entertainment and information dissemination.

11. **(Open Infrastructure and Construction) Construction and Infrastructure:** Involves the construction of buildings, roads, bridges and other infrastructure projects.

12. **(Open Education) Education:** The education industry includes schools, universities, online education platforms, and educational technology companies.

13. **(Open Traveling) Hospitality and Tourism:** This sector includes hotels, restaurants, travel agencies and tourist destinations.

14. **(Open Government) Government and public services:** Government agencies and public services, such as healthcare, education, and law enforcement, are essential to the functioning of society.

15. **(Open Eco) Environment and sustainability:** With growing concerns about climate change, this sector focuses on renewable energy, green technologies and conservation efforts.

16. **(Open Telecommunications) Telecommunications: **Telecommunications companies provide communication services through wired and wireless networks.

17. **(Open Pharmaceutical) Pharmaceuticals and Healthcare Research:** This subset of healthcare focuses on drug discovery, medical research, and the pharmaceutical industry.

18. **(Open E-Retail) Consumer Goods:** Consumer goods include everyday products such as clothing, electronics, and household items.

19. **(Open Automotive) Automotive:** The automotive industry involves the manufacturing and sale of vehicles, including cars, trucks, and electric vehicles.

20. **(Open Legal Services) Legal services:** Legal firms and services provide legal advice, representation and support to individuals and companies.

The importance of these industry verticals may change over time due to technological advances, economic changes, and global events. Additionally, new industries and sectors may emerge as society evolves and new needs arise. Therefore, the relative importance of these industry verticals may vary by region and time period.
</details>

<details>
<summary> Creating an open industry ecosystem </summary>

TPrerequisites:  
- On the local cluster add a label:  *environment=dev*.

```IMAGE TODO
```

- On the new cluster you provisioned via ACM double check you added the label:  *environment=prod*.

```IMAGE TODO
```

1. In RHACM, navigate to Applications and click Create application and select Subscription. 
Enter the following information:


**Name**: open-education 
**Namespace**: open-education 
 Under Repository location for resources, select the GIT repository
**URL**:  https://github.com/psehgaft/open-education.git
**Branch**:  main
**Path**:  open-education

Next to Create application, make sure the YAML dial is ON

```IMAGE TODO
```

Under the S*elect clusters for application deployment*, select *Deploy application resources on clusters with all specified labels*
**Cluster sets**: global
**Label**: environment
**Value**: dev

```IMAGE TODO
```

Click Create and after a few minutes you will see the application and all its components available in RHACM.

```IMAGE TODO
```

If everything was done correctly you should be able to see the application deployed to local-cluster. Go to *Applications*, and make sure to filter by subscription as the image below:

```IMAGE TODO
```

This will show only the apps deployed from ACM, instead of all the existing apps in the managed clusters. 

Click on the *open-education application* and have a look at the topology view

```IMAGE TODO
```

Select the Route and click on the URL provided, you should see the Book Import application

See the Book Import user interface.

```IMAGE TODO
```


</details>

## 7. Network Overload and Latency & Hybrid Cloud Balancing

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services. Items marked with a ^ have already been implemented.

<details>
<summary> ^ Deploy Skupper Operator </summary>

Skupper is a Layer 7 service interconnect that enables multicloud communication across Kubernetes clusters. There are a few reasons you might need to communicate between a local cluster and a remote one in development:

A service is deployed on the remote cluster, and you want to consume it with a local cluster.
A workload is high resource-consuming, and it is not feasible to deploy it on the local cluster given the available resources.
An existing stage/test database service is deployed on a remote cluster, and your workload needs to connect to it.

If you want to try a cluster-wide installation, you don't need to create the `OperatorGroup` as it is already defined at the destination namespaces, so you just need to create the subscription at the correct namespaces, see below.

> **_NOTE:_**Note for cluster-wide installations

If you want to try a cluster-wide installation, you don't need to create the `OperatorGroup` as it is already defined at the destination namespaces, so you just need to create the subscription at the correct namespaces, see below.

Cluster-wide installation on OpenShift

On OpenShift the `Subscription` needs to be defined in the `openshift-operators` namespace, like:

```sh
kubectl apply -f skupper/20-Subscription-cluster.yaml
```

</details>
<details>
<summary> Validate skupper-operator is running </summary>

Look at the pods running in your `open-ecosystems-cross-services` namespace now. You should 
see a running pod for the `skupper-site-controller`.

```
oc get pods -n open-ecosystems-cross-services
NAME                                     READY   STATUS    RESTARTS   AGE
skupper-site-controller-d7b57964-gxms6   1/1     Running   0          39m
```

Now the Skupper Operator is running and you can create a site. 
At this point with most Operators, you would create a CR, however 
the Skupper Operator manages your
Skupper site by watching a `ConfigMap` named exclusively `skupper-site`
in the namespace where it is running (in this case the `open-ecosystems-cross-services` namespace).

</details>
<details>
<summary> Creating a new skupper site </summary>

Create a `ConfigMap` named `skupper-site` in the `open-ecosystems-cross-services` namespace:

```
kubectl apply -f examples/skupper-site-interior.yaml
```

Once the `ConfigMap` is created, Skupper Site Controller will initialize
your Skupper site and you can verify everything is running properly if you
see the `skupper-router` and the `skupper-service-controller` pods running
in the `open-ecosystems-cross-services` namespace, in example:

```sh
oc get pods -n open-ecosystems-cross-servicese
NAME                                          READY   STATUS    RESTARTS   AGE
skupper-router-8c6cc6d76-27562                1/1     Running   0          40s
skupper-service-controller-57cdbb56c5-vc7s2   1/1     Running   0          34s
skupper-site-controller-d7b57964-gxms6        1/1     Running   0          51m
```

You can now navigate to the Skupper console.

The namespace in the example YAML is `open-ecosystems-cross-services`.

Navigate to the `skupper` route and log in using the credentials you specified in YAML. The example YAML uses `admin/changeme`.

For more information, visit the official [Skupper website](https://skupper.io)
</details>

<details>
<summary> Creating a new skupper site </summary>

*On OCP-01 and OCP-02*

1. Create a new proyect

```sh
oc new-project globex
```

*On OCP-01*

1. Run the skupper init command to install the router in each namespace.

```sh
skupper init --cluster-local
```

*On OCP-02*

```sh
skupper init
```

</details>
<details>

<summary> Expose open ecosystems services </summary>

First, we will deploy the cross service on the OCP-01 and the ecosystem-demo service to OCP-02. Then, we’ll connect the cross with the ecosystem-demo.

*On OCP-01*

```sh
oc  create deployment open-ecosystems-demo --image quay.io/psehgaft/open-ecosystems-demo
```

*On OCP-02*

```sh
oc  create deployment open-ecosystems-cross --image quay.io/psehgaft/open-ecosystems-cross

oc get svc
```

*On OCP-01*

```sh
$ oc expose deployment open-ecosystems-demo --port 8080
service/hello-world-frontend exposed

$ oc expose svc open-ecosystems-demo
route.route.openshift.io/hello-world-frontend exposed

$ curl open-ecosystems-demo.apps-crc.testing
```

skupper expose deployment open-ecosystems-cross --port 8080 --protocol http

</details>


## 8. Duplication of Functionalities and Waste of Resources

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services. Items marked with a ^ have already been implemented.

0. **(Open Ecosistems Cross services) Generic/cross microservices:** Generic and cross microservices, common services to energize the ecosystems of the industries.

<details>
<summary> Scenarios </summary>

### Deploy applications

<details>
<summary> Hybrid cloud eccosistem </summary>

#### Deploy Services

> **_IMPORTANT:_** If you are using `minikube` as one cluster, run `minikube tunnel` in a new terminal.

As Kubernetes enables you to have cloud portability, the workload can be deployed on any Kubernetes context.
Deploy the backend using the following three commands on all clusters and change only `WORKER_CLOUD_ID` value to differentiate between them.  The name of the cloud or the location/geography are useful to illustrate where the work is being conducted/transacted. 

```[source, shell-session]
kubectl create namespace hybrid
kubectl -n hybrid apply -f backend.yml
kubectl -n hybrid set env deployment/hybrid-cloud-backend WORKER_CLOUD_ID="localhost" # aws, azr, gcp
```

The annotation has already been applied in the backend.yml file but if wish to apply it manually, use the following command.

```[source, shell-session]
kubectl annotate service hybrid-cloud-backend skupper.io/proxy=http
```

Deploy the frontend to your *main* cluster:

The Kubernetes service is of type `LoadBalancer`.
If you are deploying the frontend in your public cluster open `frontend.yml` file and modify Ingress configuration with your host:

```[source, yaml]
spec:
  rules:
  - host: ""
```

In your *main* cluster, deploy the frontend by calling:

```[source, shell-session]
kubectl apply -f frontend.yml
```

TIP: In case of OpenShift you can run: `oc expose service hybrid-cloud-frontend` after deploying frontend resource, and it is not required to modify the Ingress configuration. But of course, the first approach works as well in OpenShift.

To find the frontend URL, on OpenShift use the Route

```[source, shell-session]
kubectl get routes | grep frontend
```

On vanilla Kubernetes, try the external IP of the Service

```[source, shell-session]
#AWS
kubectl get service hybrid-cloud-frontend -o jsonpath="{.status.loadBalancer.ingress[0].hostname}"

#Azure, GCP
kubectl get service hybrid-cloud-frontend -o jsonpath="{.status.loadBalancer.ingress[0].ip}"
```

In your *main* cluster, init `skupper` and create the `connection-token`:

```[source, shell-session]
skupper init --console-auth unsecured # <1>

Skupper is now installed in namespace 'hybrid'.  Use 'skupper status' to get more information.

skupper status

Skupper is installed in namespace '"hybrid"'. Status pending...
```

1. This makes anyone be able to access the Skupper UI to visualize the clouds. Fine for demos, not to be used in production.

See the status of the skupper pods.
It takes a bit of time (usually around 2 minutes) until the pods are running:

```[source, shell-session]
kubectl get pods 

NAME                                        READY   STATUS    RESTARTS   AGE
hybrid-cloud-backend-5cbd67d789-mfvbz       1/1     Running   0          3m55s
hybrid-cloud-frontend-55bdf64c95-gk2tf      1/1     Running   0          3m27s
skupper-router-dd7dfff55-tklgg              2/2     Running   0          59s
skupper-service-controller-dc779b7c-5prhc   1/1     Running   0          56s
```

Finally create a token:

```sh
skupper token create token.yaml -t cert

Connection token written to token.yaml
```

In *all the other clusters*, use the connection token created in the previous step:

```[source, shell-session]
skupper init
skupper link create token.yaml
```

Check the service status on all clusters

```[source, shell-session]
skupper service status
Services exposed through Skupper:
╰─ hybrid-cloud-backend (http port 8080)
   ╰─ Targets:
      ╰─ app.kubernetes.io/name=hybrid-cloud-backend,app.kubernetes.io/version=1.0.0 name=hybrid-cloud-backend
```

Check the link status on the 2nd/3rd cluster

```[source, shell-session]
skupper link status
Link link1 is active
```

This has been the short-version to get started, continue reading if you want to learn how to build the Docker images, deply them , etc.

#### Skupper UI

If you run:

```[source, shell-session]

kubectl get services 

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP                                                              PORT(S)               AGE
hybrid-cloud-backend    ClusterIP      172.30.157.62   <none>                                                                   8080/TCP              10m
hybrid-cloud-frontend   LoadBalancer   172.30.70.80    acf3bee14b0274403a6f02dc062a3784-405180745.eu-west-1.elb.amazonaws.com   8080:32156/TCP        10m
skupper                 ClusterIP      172.30.128.55   <none>                                                                   8080/TCP,8081/TCP     7m50s
skupper-router          ClusterIP      172.30.7.7      <none>                                                                   55671/TCP,45671/TCP   7m53s
skupper-router-local    ClusterIP      172.30.8.239    <none>                                                                   5671/TCP              7m53s                                                               5671/TCP              34m
```

### Services

#### Backend

If you want to build, push and deploy the service:

```[source, shell-session]
cd backend
./mvnw clean package -DskipTests -Dquarkus.kubernetes.deploy=true -Pazure
```

If service is already pushed in quay.io, so you can skip the push part:

```[source, shell-session]
cd backend

./mvnw clean package -DskipTests -Pazure -Dquarkus.kubernetes.deploy=true -Dquarkus.container-image.build=false -Dquarkus.container-image.push=false
``` 

#### Frontend

If you want to build, push and deploy the service:

```[source, shell-session]
cd backend
./mvnw clean package -DskipTests -Dquarkus.kubernetes.deploy=true -Pazure -Dquarkus.kubernetes.host=<your_public_host>
```

If service is already pushed in quay.io, so you can skip the push part:

```[source, shell-session]
cd backend

./mvnw clean package -DskipTests -Pazr -Dquarkus.kubernetes.deploy=true -Dquarkus.container-image.build=false -Dquarkus.container-image.push=false
```

#### Cloud Providers

The next profiles are provided: `-Pazr`, `-Paws`, `-Pgcp` and `-Plocal`, this just sets an environment variable to identify the cluster.

#### Setting up Skupper

Make sure you have a least the `backend` project deployed on 2 different clusters. The `frontend` project can be deployed to just one cluster.

Here, we will make the assumption that we have it deployed in a local cluster *local* and a public cluster *public*.

Make sure to have 2 terminals with separate sessions logged into each of your cluster with the correct namespace context (but within the same folder).

##### Install the Skupper CLI 

Follow the instructions provided https://skupper.io/start/index.html#step-1-install-the-skupper-command-line-tool-in-your-environment[here].

##### Skupper setup

. In your *public* terminal session : 

```sh
skupper init --id public
skupper connection-token private-to-public.yaml
```

. In your *local* terminal session : 

```sh
skupper init --id private
skupper connect private-to-public.yaml
```

##### Annotate the services to join to the Virtual Application Network

. In the terminal for the *local* cluster, annotate the hybrid-cloud-backend service:

```sh
kubectl annotate service hybrid-cloud-backend skupper.io/proxy=http
```

. In the terminal for the *public* cluster, annotate the hybrid-cloud-backend service:

```sh
kubectl annotate service hybrid-cloud-backend skupper.io/proxy=http
```

Both services are now connected, if you scale one to 0 or it gets overloaded it will transparently load-balance to the other cluster.
</details>

<details>
<summary> Creating an Application </summary>


</details>


</details>

<details>
<summary> Deploying Ansible Automation Platform 2 </summary>

<details>
<summary> Install the Operator Ansible Automation Platform 2 </summary>

1. For this exercise, we’ll start by accessing the Operator Hub in the OpenShift console*(local-cluster/ACM Hub Cluster)* to deploy AAP. So, for this, go to the Operator Hub and select the Ansible Automation Platform.

Make sure to select channel stable-2.4-cluster-scoped and click INSTALL.

After a couple of minutes, the APP operator installation will finish. Verify that pods are running by either accessing *Workloads → Pods* under the AAP namespace, or by running this command in the bastion machine: 

```sh
oc get pods -n aap
```

There should be 4 pods in a running state.

There should be 4 pods in a running state.

2. Deploy the Automation Controller

After the operator is successfully deployed, we’ll need to have the Automation Controller instance. Access the AAP operator dashboard(you can do this by clicking on Installed Operators and clicking on the AAP Operator), click in the Automation Controller tab. Then click on Create *AutomationController*:

Now, a form will be presented to you. Just give your AutomationController instance a name, like aap2, and hit CREATE. This installation will also take a couple of minutes.

Verify this installation, again, by checking the pods in the aap namespace. Now, there should be 7 pods in a running state. 

```sh
oc get pods -n aap
```

3. Access the AAP dashboard

If everything was done correctly, shortly we’ll be able to see an AAP route deployed. Before accessing the URL, still in the aap namespace, navigate over to Secrets and get the AAP admin password in the secret <name-of-aap-controller-instance>-admin-password. In this case, app2-admin-password.

Click on the secret name and you will be able to copy the password at the bottom of the following page. 
Now we’re all set. Access *Networking → Routes*, and click on the AAP route. 

> **_Note:_** you may see that AAP is starting up and upgrading components, while the WEB UI is setting up. This should just take less than a minute.

Use *“admin”* as username and the retrieved secret as password to login to AAP.

4. Configure AAP

Now that you’re logged in, let’s proceed with the initial configuration.
First of all, when you click on the AAP url, you will be presented with a Subscription dialog window.  Click on username/password and provide your Red Hat credentials (from your account in access.redhat.com, not Red Hat SSO). You’ll need an Ansible subscription in order to be able to use it. Feel free to use one of your trials and/or the employee SKU.

Select one and click *NEXT*.

Disable the User Analytics and the Automation Analytics for AAP, we don’t need those for our example. Click *NEXT*.

Lastly, accept the end user license agreement by clicking on *SUBMIT*.

5. Generate a token for ACM

If everything was done correctly it will redirect to the controller page. In the Ansible dashboard, generate a token for the *admin* user.  Go to *Users*, click *admin*, select *TOKENS*, then click the *ADD* button.  Add a short description “*Token for use by ACM*”, update the *SCOPE* to *Write*, then click *SAVE*.  

</details>

<details>
<summary> Deploying a ServiceNow Developer Instance </summary>

The purpose of this exercise is to take advantage of the Ansible Automation Platform (AAP) you just deployed to kick off Ansible Jobs (tied to prehook or posthook tasks in the application lifecycle of ACM.  

A pre hook will kick off an Ansible job before the application creation / modification.
A post hook will kick off an Ansible job after the application creation / modification.

In the following example the Ansible job will trigger the creation of ServiceNow Change Requests. Perform this step if you would like to show or learn how this integration works.  You will take advantage of this within the application lifecycle engine.

To deploy your own instance of ServiceNow, please visit https://developer.servicenow.com
Select Sign up and Start Building.

After signing up and requesting your developer ServiceNow instance.

You can select the Utah version(latest) and soon, you will have an instance URL that looks like this:  https://dev#####.service-now.com.

Make note of your instance URL, your admin username and password.

</details>

<details>
<summary> Configure Ansible to trigger a job that will create a ServiceNow Change Request </summary>

*Create a ServiceNow Credential Type*

In Ansible Automation Platform we need to create a *Credential Type* for ServiceNow, and then add the *Credentials* for our ServiceNow developer instance.

- Select *Credential Types*, under *Administration*, in the left menu and then click *ADD*.
- Name: ServiceNow
- Input Configuration:

```yml
fields:
  - id: SNOW_USERNAME
    type: string
    label: Service Now Username
  - id: SNOW_INSTANCE
    type: string
    label: Service Now Instance Name (https://devXXXXX.service-now.com)
  - id: SNOW_PASSWORD
    type: string
    label: Service Now Password
    secret: true
required:
  - SNOW_USERNAME
  - SNOW_INSTANCE
  - SNOW_PASSWORD
```

- Add the following text to the *INJECTOR CONFIGURATION* field

```yml
extra_vars:
  snow_instance: '{{ SNOW_INSTANCE }}'
  snow_password: '{{ SNOW_PASSWORD }}'
  snow_username: '{{ SNOW_USERNAME }}'
```

- *SAVE* this new credential type

Add the ServiceNow Credentials

- Navigate to *Resources → Credentials*.  Click on *ADD*.  
- *Name*: ServiceNow Credentials 
- *CREDENTIAL TYPE* field, select *ServiceNow*
- *ORGANIZATION* field, select *Default*
- In the *USERNAME* and *INSTANCE NAME *add admin and the instance name to your developer instance.  Will be something like: https://dev#####.service-now.com  
- In the *PASSWORD* field, in get the password from your user settings in the ServiceNow dashboard/website. Then *SAVE*.

Create an Ansible Project

- In Ansible we need to create a Project
- Select Projects, under Resources, in the left menu.  Click on ADD.  Enter snow-create-change-record in the NAME field
- Set the ORGANIZATION field to Default
- Set the SCM TYPE to Git
- Set the *SCM URL* to:  https://github.com/psehgaft/ansible_snow
- Click *SAVE*

Create an Ansible Job Template

In Ansible we need to create a *Job Template*.

- Select *Templates*, under *Resources*, in the left menu.  
- *Click* on *ADD* then Add *Job Template*.  
    - *NAME*: snow-create-change-record 
    - *INVENTORY* field search and select Demo Inventory, and check PROMPT ON LAUNCH 
    - *PROJECT*: snow-create-change-record 
    - *PLAYBOOK*: select servicenow_changerequest.yml
    - *CREDENTIALS*: from the dropdown select ServiceNow, and select ServiceNow Credentials Click SELECT
    - *VARIABLES* field check PROMPT ON LAUNCH 
- Scroll all the way to the bottom, leave everything as default and click *SAVE*
- Success will indicate it can communicate with ServiceNow and it successfully created a Change Request in ServiceNow

To verify all was configured properly click the *Launch Button*.
Click *NEXT*, *NEXT* and *LAUNCH*.

Verify that the job ran successfully by looking at the output.

You can also look in your ServiceNow instance.

</details>

<details>
<summary> Create AAP credential in ACM </summary>

Here, we are going to set up the credential which is going to allow ACM to interact with our AAP instance. Click on *Credentials* on the left menu and select *Add Credential* button.

- *Credential type*: Ansible Automation Platform
- *Credential name*: aapaccess
- *Namespace*: open-cluster-management
- *Click NEXT*

For *Ansible Tower Host* enter you Ansible instance URL, you will find this information on previous screen if not check the *ROUTES* on your *HUB* Cluster

For *Ansible Tower token* enter the admin user token you generated earlier

In order to save, click *NEXT* and *ADD*. You’ll be redirected to the *Credentials* page.

</details>


<details>
<summary> Create an application to take advantage of the ACM - Ansible integration </summary>

The purpose of this short section is to show how ACM integration with Ansible will kick off an Ansible Job.  In this case the Ansible Job will run a playbook that will trigger the creation of a ServiceNow Change Request, exactly like we did and saw in the previous section.

Within ACM navigate to the Applications menu on the left, and click *Create application → Subscription*. Enter the following information:


- *Name*: book-import2
- *Namespace*: book-import2 

Under repository types, select the GIT repository

- *URL*:  https://github.com/levenhagen/book-import.git
- *Branch*:  prehook
- *Path*:  book-import

Expand the “*Configure automation for prehook and posthook*” dropdown menu.

Ansible Automation Platform credential: aapaccess

Select Deploy application resources only on clusters matching specified labels

- Label: env
- Value: prod

SAVE the application.  Give this a few minutes.  The application will complete and in the application topology view you will see the Ansible prehook, and you can infer that it’s a ServiceNow change request creation.

</details>

</details>

---

# License
This repository and everything within it are licensed under the [GNU General
Public License (GPL) v3.0](LICENSE)
