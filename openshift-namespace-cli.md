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
