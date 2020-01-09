<h2>How do I restore from an etcd backup in OpenShift?</h2>

<h3>Resolving the problem</h3>
<ol>
  <li>Create a backup directory and move the etcd.yaml file</li>
  <pre>mkdir /home/user/etcdbackup/
cd /home/user/etcdbackup/
mv /etc/origin/node/pods/etcd.yaml .</pre>
</ol>
