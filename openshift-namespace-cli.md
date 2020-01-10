<h2>Node Selector annotations</h2>

<blockquote>
  For DC
</blockquote>
<pre>
oc get nodes --show-labels=true
oc patch dc/<dcname> -p '{"spec":{"template":{"spec":{"nodeSelector":{"<label_name>":"<label_value>"}}}}}'</pre>
