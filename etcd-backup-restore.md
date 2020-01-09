<h2>How do I restore from an etcd backup in OpenShift?</h2>

<h3>Resolving the problem</h3>
<ol>
  <li>Create a backup directory and move the etcd.yaml file</li>
  <pre>mkdir /home/user/etcdbackup/
cd /home/user/etcdbackup/
mv /etc/origin/node/pods/etcd.yaml .</pre>
  <li>Check the ETCD Container is running or nor, if is exited state please delete</li>
  <pre>[root@ocpmaster etcdbackup]# docker ps -a | grep -i etcd
[root@ocpmaster etcdbackup]#</pre>
  <li>remove the content from /var/lib/etcd/, please make sure you have the backup of /var/lib/etcd</li>
  <pre>[root@ocpmaster etcdbackup]# rm -rf /var/lib/etcd/*
[root@ocpmaster etcdbackup]#</pre>
</ol>
