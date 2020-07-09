# EFKOpenShift

## Openshift: Cluster Logging components
The cluster logging components are based upon Elasticsearch, Fluentd, and Kibana (EFK). The collector, Fluentd, is deployed to each node in the OpenShift Container Platform cluster. It collects all node and container logs and writes them to Elasticsearch (ES). Kibana is the centralized, web UI where users and administrators can create rich visualizations and dashboards with the aggregated data.

## Pre-Requisites
<br>IBM Cloud Account.</br>
<br>IBM Cloud CLI installtion : - curl -sL https://ibm.biz/idt-installer | bash. Alternatively we will use IBM cloud shell https://shell.cloud.ibm.com </br>
<br>IBM Cloud Openshift cluster previsioned.</br>
<br>openshift login token.</br>

## Steps
1. Create openshift-operators-redhat namespace
2. Create openshift-operators-redhat OperatorGroup
3. Create Elastic Search Operator
4. Create role name prometheus-k8s to access openshift-operators-redhat namespace
5. Create openshift-logging namesapce
6. Create openshift-logging operatorGroup
7. Change the virtual memory in all worker nodes(Fot elastic search , virtual memory required is 263754 wheras free cluster provisioned have virtual memory set to 253754. So we will change all worker nodes to update memory
8. Create Cluster logging operator
9. Create cluster logging Instance (This instance will create our reuired pods in openshift-logging namespace)

You can do this lab either on local terminal ot ibmcloud webshell 
### start your cloud shell 
https://shell.cloud.ibm.com

### Start with cloning the directory which contain all the required yaml file 
````$ git clone https://github.com/shiprajain14/EFKOpenShift.git ```
### go to yaml folder
``` $ cd EFKOpenShift/yaml```
you will find few of the yamls which we will use to create our resources

### connect you shell to openshift cluster 
copy the openshift logging token copied from openshift console 
``` $ oc login --token=ysBBmHyQJnWW4WN7B-n8uOCMVu0e_KenYKzUejM_sfI --server=https://c100-e.au-syd.containers.cloud.ibm.com:30142
Logged into "https://c100-e.au-syd.containers.cloud.ibm.com:30142" as "IAM#shiprajain.jain@gmail.com" using the token provided.

You have access to 59 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "default".
Welcome! See 'oc help' to get started
```

### Create openshift-operators-redhat namespace using below command
``` $  oc create -f 1_elastic-search-operator-namespace.yaml 
       namespace/openshift-operators-redhat configured
```

### Create openshift-operators-redhat OperatorGroup
``` $ oc create -f 2_elastic-search-operator-group.yaml 
    operatorgroup.operators.coreos.com/openshift-operators-redhat configured 
```
### 3. Create Elastic Search Operator
```$ oc create -f 3_elastic-search-subscription-operator.yaml 
ubscription.operators.coreos.com/elasticsearch-operator configured ```

4. Create role name prometheus-k8s to access openshift-operators-redhat namespace
5. Create openshift-logging namesapce
6. Create openshift-logging operatorGroup
7. Change the virtual memory in all worker nodes(Fot elastic search , virtual memory required is 263754 wheras free cluster provisioned have virtual memory set to 253754. So we will change all worker nodes to update memory
8. Create Cluster logging operator
9. Create cluster logging Instance (This instance will create our reuired pods in openshift-logging namespace)
### 



