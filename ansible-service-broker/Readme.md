Once the cluster is running, we can install the OpenShift Ansible Broker onto the cluster and register it with the Service Catalog. First, we will need a new project to run the broker in. Using the CLI, let’s create the ansible-service-broker project.

oc login -u system:admin
oc new-project ansible-service-broker
After a successful run, you’ll see something like this:

Now using project "ansible-service-broker" on server "https://127.0.0.1:8443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app centos/ruby-22-centos7~https://github.com/openshift/ruby-ex.git

to build a new example application in Ruby.
With the project created, we can now deploy the broker. We’ve assembled an OpenShift template that can be used for this purpose. Let’s download the template, process the variables, and create an OpenShift Ansible Broker instance.

curl -s https://raw.githubusercontent.com/openshift/ansible-service-broker/master/templates/simple-broker-template.yaml | oc process -n "ansible-service-broker" -f - | oc create -f -
A successful deployment will look like this:

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
We now have an OpenShift cluster with the Service Catalog and Ansible Broker running. You can communicate with the Broker through the Service Catalog using the oc command line. Here is an example of listing all the available APB service classes:

oc get clusterserviceclasses --all-namespaces -o custom-columns=NAME:.metadata.name,DISPLAYNAME:spec.externalMetadata.displayName | grep APB
It may take some time for the broker to sync the APBs into the catalog. If you get no APBs at first, run it again in a few seconds. Once they are available we can start provisioning services.

Provisioning Services
As mentioned above, the Broker implements the Open Service Broker API. This API contains some key verbs: provision, bind, and others. Provision will typically deploy a service in your cluster. In the case of the OpenShift Ansible Broker, it provisions a service using the Ansible Playbook Bundle meta-container and invoking the provision playbook.

For our service provisioning example, we’re going to walkthrough provisioning MediaWiki which is backed by a PostgreSQL database. This is accomplished by first provisioning a PostgreSQL instance and then the MediaWiki service.

Once the two services have been provisioned, we will tie them together by creating a binding between them. Bind is another one of the OSB API verbs used to provide credentials/coordinates for specific services. Like the provision operation, the Broker uses the PostgreSQL APB meta-container and invokes the bind playbook to create the binding.

Let’s recap, first, we will provision two services using APBs: PostgreSQL and MediaWiki. Next, we create and consume the binding to the PostgreSQL database instance. Finally, we will verify the MediaWiki service is up and running.
