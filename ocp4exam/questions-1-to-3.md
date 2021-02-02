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
  <pre>oc create secret generic ex280-htpass --from-file=/xxx/yyy/passwd -n openshift-config</pre>
  <pre> oc get oauth -o yaml
  apiVersion: config.openshift.io/v1
kind: OAuth
metadata:
  annotations:
    release.openshift.io/create-only: "true"
  creationTimestamp: "2021-01-01T02:16:11Z"
  generation: 3
  name: cluster
  resourceVersion: "2171927"
  selfLink: /apis/config.openshift.io/v1/oauths/cluster
  uid: 48c88463-e2cb-4ca2-a40d-1cd88d65ecde
spec:
  identityProviders:
  - htpasswd:
      fileData:
        name: ex280-htpass
    mappingMethod: claim
    name: Admin Portal
    type: HTPasswd
</pre>
  <li>Tea</li>
  <li>Milk</li>
</ol> 
