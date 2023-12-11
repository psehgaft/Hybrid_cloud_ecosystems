# Hybrid_cloud_ecosystems

## Justification

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

7. Network Overload and Latency:

Communication between microservices can introduce latency, and a poorly designed architecture can result in network overload, affecting overall performance.
`Reference: Newman, S. (2015). Building microservices: detailed system design.`

8. Duplication of Functionalities and Waste of Resources:

Fragmentation of services can lead to duplication of functionality, which can result in wasted resources and development efforts.
`Reference: Richardson, C. (2018). Microservices Patterns: With examples in Java.`

It is important to address these problems with a strategic approach and consider specific solutions to mitigate the challenges associated with the implementation of microservices in an enterprise environment, which is why it is important to undertake research on microservices implementation that reduces the impact of the aforementioned problems. . .

## Architecture

![Open Hybrid Ecosystems](./images/hybrid-microservices-ecosystems.png)

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

# Deploying the Lab Guide

Deploying the lab guide will take three steps. First, you will need to get
information about your cluster. Second, you will build a container based on your lab.
Third, you will deploy the lab guide using the information you found so that proper
URLs and references are automatically displayed in the guide.

## Requirements / Prerequisites

Most of the information can be found in the output of the installer.

### Requirements

* Python (3.5.3)
* awscli (1.11.109-2.fc25) Fedora
* click (6.7)
* pip (9.0.1)
* setuptools (36.2.4)
* wheel (0.30.0a0)
* ansible (7.7.0-1)

<details>
<summary> Install packages </summary>

```sh
sudo dnf install -y ansible
sudo dnf install -y awscli awscli2
sudo dnf install -y python pip python3-wheel python3-click 
sudo dnf install -y setuptool
ansible-playbook submariner/submarinercli-install.yml
```
</details>

<details>
<summary> Required Environment Variables </summary>

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
<summary> vars.yml</summary>

```vars.yml
username: {{ user }}
subctl-cli-url: "https://get.submariner.io"
submariner-path: "$PATH:~/.local/bin"
```
</details>

<details>
<summary> Configure LAB </summary>

Now that you have the `workshop/workshop-settings.sh` file with the various required variables, you can deploy the lab guide into your cluster.

First, clone the repo

> **NOTE** Remember to checkout the branch you want to test against

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
<summary> Doing the Lab </summary>

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

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services.

<details>
<summary> Deploy Advanced Cluster Management for Kubernetes </summary>

You can use either the OpenShift 4 web console's built-in OperatorHub or the OpenShift CLI to install ACM. The installation breaks down to six steps:

1. Prepare the environment for the ACM installation.
2. Create a new OpenShift project and namespace.
3. Create an image-pull secret.
4. Install ACM and subscribe to the ACM Operator group.
5. Create the MultiClusterHub resource.
6. Verify the ACM installation.

We will use the OpenShift command line for the first several steps; . then, I will show you how to use either the command line or the OpenShift 4 web console.

```vars.yml
ansible-playbook lab-deployment.yml --tags acm
```
</details>

## 2. Consistency and Distributed Transactions

<details>
<summary> Deploy Submariner </summary>

```sh
sudo dnf install -y ansible
sudo dnf install -y awscli awscli2
sudo dnf install -y python pip python3-wheel python3-click 
sudo dnf install -y setuptool
ansible-playbook submariner/submarinercli-install.yml
```
</details>


### Configure Submariner

## 3. Security and Data Protection

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services.

<details>
<summary> Deploy Advanced Cluster Security for Kubernetes </summary>

When RHACM is available, you can create RHACM policies to deploy RHACS to your cluster fleet. This approach ensures that all fleet clusters are protected by RHACS.

To implement RHACS, you must create two policies in RHACM, one for centralized services and one for protected cluster services. The policy to install centralized services must be applied to the hub cluster. The policy for installing protected cluster services must be applied to the clusters that you want RHACS to protect. You can achieve this separation by using a clusterSelector parameter of the PlacementRule object.

```vars.yml
ansible-playbook lab-deployment.yml --tags acs
```
</details>

<details>
<summary> Deploy Openshift Data Protection </summary>

When RHACM is available, you can create RHACM policies to deploy RHACS to your cluster fleet. This approach ensures that all fleet clusters are protected by RHACS.

To implement RHACS, you must create two policies in RHACM, one for centralized services and one for protected cluster services. The policy to install centralized services must be applied to the hub cluster. The policy for installing protected cluster services must be applied to the clusters that you want RHACS to protect. You can achieve this separation by using a clusterSelector parameter of the PlacementRule object.

```vars.yml
ansible-playbook lab-deployment.yml --tags oadp
```
</details>

### DRP

### Backup

## 4. Monitoring and Follow-up

> **_NOTE:_** This part of the laboratory has already been provisioned, to focus on the deployment of the ecosystem's own services.

<details>
<summary> Deploy Openshift Monitoring </summary>

```vars.yml
ansible-playbook lab-deployment.yml --tags acs
```
</details>
<details>
<summary> Deploy Openshift Logging </summary>

```vars.yml
ansible-playbook lab-deployment.yml --tags acs
```
</details>
<details>
<summary> Deploy Thanos </summary>

```vars.yml
ansible-playbook lab-deployment.yml --tags thanos
```
</details>


## 5. Testing and Continuous Deployment
## 6. Cultural and Organizational Change

The importance of industry verticals can vary depending on the context, region, and the current economic and technological landscape. However, here we will focus on a list of some of the diverse and historically important industrial sectors that have played an important role in economies around the world:

<details>
<summary> Open industries </summary>

0. **(Open Ecosistems services) Generic/transversal microservices:** Generic and transversal microservices, common services to energize the ecosystems of the industries.

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


## 7. Network Overload and Latency

### Hybrid Cloud Balancing

### Deploy Skupper Operator

If you want to try a cluster-wide installation, you don't need to create the `OperatorGroup` as it is already defined at the destination namespaces, so you just need to create the subscription at the correct namespaces, see below.

```sh
# Create a Project
oc new-project "{{ username }}"

# Creating a CatalogSource in the `openshift-marketplace` namespace
oc apply -f ocp/00-CatalogSource.yaml

# Wait for the skupper-operator catalog pod to be running
oc -n openshift-marketplace get pods | grep skupper-operator

# Create an OperatorGroup in the `my-namespace` namespace
oc apply -f ocp/10-OperatorGroup.yaml


oc apply -f ocp /20-Subscription-cluster.yaml

# Create a Subscription in the `my-namespace` namespace
oc apply -f ocp/20-Subscription.yaml
```


## 8. Duplication of Functionalities and Waste of Resources

0. **(Open Ecosistems services) Generic/transversal microservices:** Generic and transversal microservices, common services to energize the ecosystems of the industries.

<details>
<summary> Scenarios</summary>

### Deploy applications

<details>
<summary> Create Proyects </summary>

Create several Projects for deploy applications

```vars.yml
oc adm new-project app-dev-$USER --display-name="Application Development"
oc adm new-project app-test-$USER --display-name="Application Testing"
oc adm new-project app-prod-$USER --display-name="Application Production"
```
</details>

</details>

---

# License
This repository and everything within it are licensed under the [GNU General
Public License (GPL) v3.0](LICENSE)
