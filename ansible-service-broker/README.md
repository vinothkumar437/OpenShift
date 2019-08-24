## OpenShift 3.11 Ansible Service broker Setup

Once the OpenShift 3.11 cluster is running, we can install the OpenShift Ansible Broker onto the cluster and register it with the Service Catalog. 

First, we will need a new project to run the broker in. Using the CLI, let’s create the ansible-service-broker project.

<pre>oc login -u system:admin</pre>

<pre>oc new-project ansible-service-broker</pre>

After a successful run, you’ll see something like this:
<pre>
Now using project "ansible-service-broker" on server "https://127.0.0.1:8443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app centos/ruby-22-centos7~https://github.com/openshift/ruby-ex.git

to build a new example application in Ruby.
</pre>

With the project created, we can now deploy the broker.  Let’s process the variables, and create an OpenShift Ansible Broker instance.

<pre>
cat simple-broker-template.yaml | oc process -n "ansible-service-broker" -f - | oc create -f -
</pre>

A successful deployment will look like this:
<pre>
service "asb" created
service "asb-etcd" created
serviceaccount "asb" created
clusterrolebinding "asb" created
clusterrole "asb-auth" created
clusterrolebinding "asb-auth-bind" created
clusterrole "access-asb-role" created
persistentvolumeclaim "etcd" created
deploymentconfig "asb" created
deploymentconfig "asb-etcd" created
secret "asb-auth-secret" created
secret "registry-auth-secret" created
configmap "broker-config" created
serviceaccount "ansibleservicebroker-client" created
clusterrolebinding "ansibleservicebroker-client" created
secret "ansibleservicebroker-client" created
route "asb-1338" created
clusterservicebroker "ansible-service-broker" created
</pre>

We now have an OpenShift cluster with the Service Catalog and Ansible Broker running. You can communicate with the Broker through the Service Catalog using the oc command line. Here is an example of listing all the available APB service classes:

<pre>
oc get clusterserviceclasses --all-namespaces -o custom-columns=NAME:.metadata.name,DISPLAYNAME:spec.externalMetadata.displayName | grep APB
</pre>

It may take some time for the broker to sync the APBs into the catalog. If you get no APBs at first, run it again in a few seconds. Once they are available we can start provisioning services.
