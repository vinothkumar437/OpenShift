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
</ol>
