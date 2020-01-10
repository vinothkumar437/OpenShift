<h2>Node Selector annotations</h2>

<blockquote>
  For DC
</blockquote>
<pre>
# oc get nodes --show-labels=true
# oc patch dc/<dcname> -p '{"spec":{"template":{"spec":{"nodeSelector":{"<label_name>":"<label_value>"}}}}}'</pre>

<blockquote>
For Project credit
</blockquote>
<p>Sets the node selector for a specific project by editing the project namespace. As an example to edit namespace for a project named “new project”</p>
<pre># oc edit namespace newproject</pre>
<p>Find the annotations section and add a node selector annotation as under. This is a yaml file; so make sure that the indentation is right.</p>
<pre>  annotations:
    openshift.io/node-selector: “region=secondary"
    openshift.io/description: ""
    openshift.io/display-name: ""</pre>
    
<blockquote>
For Project 
</blockquote>
<pre>
oc annotate ns "target-proj" openshift.io/node-selector='kubernetes.io/hostname=app1.ap.ex.io'
</pre>

<blockquote>
For SCC Range
</blockquote>
<pre>oc annotate ns "target-proj" openshift.io/sa.scc.uid-range='999/1001' --overwrite=true</pre>

