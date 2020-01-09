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
  <li>Restore the ETCD using below command</li>
  <pre>[root@ocpmaster etcdbackup]# 

ETCDCTL_API=3 etcdctl snapshot restore /root/etcdbackup-backup/member/snap/db --name ocpmaster.example.local --initial-cluster ocpmaster.example.local=https://x.x.x.x:2380 --initial-cluster-token etcd-cluster-1 --initial-advertise-peer-urls https://x.x.x.x:2380 --data-dir /var/lib/etcd/restore --skip-hash-check=true

2020-01-08 16:57:48.898195 I | mvcc: restore compact to 48520210
2020-01-08 16:57:49.243363 I | etcdserver/membership: added member 95c90cc859b94ed0 [https://x.x.x.x:2380] to cluster 676239b0d9b745cc
[root@ocpmaster etcdbackup]#</pre>
<li>Copy the file from /var/lib/etcd/restore to /var/lib/etcd/</li>
<pre>cd /var/lib/etcd
mv restore/* .</pre>
<p>Move th etcd.yaml</p>
<pre>mv etcd.yaml /etc/origin/node/pods/</pre>
</ol>

<p>For more information:<a href="https://access.redhat.com/solutions/4013381">Click here</a></p>
