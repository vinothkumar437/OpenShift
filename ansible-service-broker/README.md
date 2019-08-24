## OpenShift 3.11 Ansible Service broker Setup

Once the cluster is running, we can install the OpenShift Ansible Broker onto the cluster and register it with the Service Catalog. 

First, we will need a new project to run the broker in. Using the CLI, let’s create the ansible-service-broker project.

<pre>oc login -u system:admin</pre>

<pre>oc new-project ansible-service-broker</pre>

