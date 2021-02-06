# DO 280 v4.2
<ol>
  <li>Create a 2 groups commander and pilot. 
    <p> Add user armstrong as part of commander group. </p>
    <p> Add jack & eric as part of pilot group. </p>
    <p> commander group should be allowed to edit project3.</p>
    <p> Pilot group should be allowed to view project1.</p></li>
  <pre>oc adm groups new commander
oc adm groups new pilot</pre>
  <pre>oc adm groups add-users commander armstrong</pre>
  <pre>oc adm groups add-users  pilot jack</pre>
  <pre>oc adm groups add-users  pilot eric</pre>
  <pre>oc adm policy add-role-to-group edit commander -n project3</pre>
  <pre>oc adm policy add-role-to-group view pilot -n project1</pre>
  <li>Create a resource quota with name ex280-quota on the project1 with resource consumption to be PODS=3, SERVICE=6, MEMORY=1Gi, CPU= 2 Core.</li>
  <pre>oc create quota ex280-quota --hard=cpu=2,memory=1G,pods=3,services=6 -n project1</pre>
  <pre>oc describe quota ex280-quota -n project1</pre>
  <li>Create a LimitRange on Project4 with the limit sets to be for a POD & CONTAINER CPU 10m to 100m and MEMORY 5Mi to 500MIi</li>
  <pre>vim limitrange.yaml
---
apiVersion: v1
kind: LimitRange
metadata:
  name: dev-limits
  namespace: project4
spec:
  limits:
  - type: Pod
    min:
      cpu: 10m
      memory: 5Mi
    max:
      cpu: 100m
      memory: 500Mi
  - type: Container
    min:
      cpu: 10m
      memory: 5Mi
    max:
      cpu: 100m
      memory: 500Mi
      </pre>
   <pre>   
      oc create -f limitrange.yaml
</pre>
</ol>
