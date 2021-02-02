# DO 280 v4.2

<ol>
  <li>Create an users via htpasswd identity provider as "httpd-pass-id" for users <b>armstrong, jobs, woz-niak, jack & erick</b> with the given password. And name of the secret to store these values is <b>ex280-htpass</b></li>
  <pre> oc login -u username -p password apiurl </br>
  sudo yum install httpd-tools </br>
  mkdir work</br>
  cd work</br></pre>
  <p> Create an users_env file with given password</p>
  <pre>cat users_env</br>
export armstrong=aaaaaa
export jobs=bbbbbb
export wozniak=ccccc
export jack=ddddddd
export eric=eeeeeee</br>
source users_env
  </pre>
  <pre>
  htpasswd -c -B -b passwd armstrong ${armstrong}
  htpasswd -B -b passwd jobs ${jobs}
  htpasswd -B -b passwd wozniak ${wozniak}
  htpasswd -B -b passwd jack ${jack}
  htpasswd -B -b passwd eric ${eric}
  </pre>
  <p>Create a secret</p>
  <pre>oc create secret generic ex280-htpass --from-file=htpasswd=/xxxx/yyyy/passwd -n openshift-config</pre>
  <pre> oc get oauth -o yaml
apiVersion: config.openshift.io/v1
kind: OAuth
metadata:
  annotations:
    release.openshift.io/create-only: "true"
  creationTimestamp: "2021-01-01T02:16:11Z"
  generation: 3
  name: cluster
spec:
  identityProviders:
  - htpasswd:
      fileData:
        name: ex280-htpass
    mappingMethod: claim
    name: Admin Portal
    type: HTPasswd
</pre>
<pre>oc login -u armstrong -p ${armstrong}
oc login -u jobs -p ${jobs}
oc login -u eric -p ${eric}
oc login -u jack -p ${jack}
oc login -u wozniak -p ${wozniak}</pre>
  <li>Create a 5 new projects and assign the roles to the respective user, armstrong is an admin for project1, jack & eric has view permission on project2, woznaik has edit permission on project1</li>
  <pre>oc new-project project1
oc new-project project2
oc new-project project3
oc new-project project4
oc new-project project5</pre>
<pre>oc policy add-role-to-user admin armstrong -n project1
oc policy add-role-to-user view jack -n project2
oc policy add-role-to-user view eric -n project2
oc policy add-role-to-user edit wozniak -n project1</pre>
  <li>Milk</li>
</ol> 
