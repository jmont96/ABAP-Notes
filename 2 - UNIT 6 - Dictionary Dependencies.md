---


---

<h1 id="dictionary-object-dependencies">Dictionary Object Dependencies</h1>
<h2 id="active-and-inactive-objects">Active and Inactive Objects</h2>
<p>An active object is being used in the system, but what if you have to change it? This is why ABAP saves an active version and an inactive version, so that the active version isn’t broken while you are making changes.</p>
<p>Active:</p>
<ul>
<li>Runtime components access this version</li>
<li>Does not reflect incremental changes</li>
</ul>
<p>Inactive:</p>
<ul>
<li>Has no effect on runtime system</li>
<li>Created after making change on active version</li>
</ul>
<p>When activating an inactive version:</p>
<ol>
<li>Inactive version checked for syntax errors</li>
<li>If consistent with active version, the inactive version replaces the current active version</li>
<li>The runtime system now uses the new active version</li>
</ol>
<h2 id="mass-activation">Mass Activation</h2>
<p>Activation of large sets simultaneously.<br>
Automatically called when a transport request is imported into a system.</p>
<ul>
<li>System gets a list of Dictionary objects</li>
<li>All objects are activated in one action</li>
<li>This has some advantages over activating one at a time
<ul>
<li>If dependent tables are affected by changes to different domains or data elements, they only have to be reactivated once.</li>
</ul>
</li>
<li>An activation log is stypically created when activating an object</li>
</ul>
<p>Runtime Objects:</p>
<ul>
<li>Information about the overall structure, like number of fields</li>
<li>Information about individual structure fields like name, field position and data type</li>
<li>Information required by the DB interface to access table data like a client number or key fields</li>
</ul>
<p>ABAP Dicitonary items that can be used as types:</p>
<ul>
<li>Table types</li>
<li>Data elements</li>
<li>Views</li>
<li>Structures</li>
<li>Tables</li>
</ul>
<p>BOTTOM LINE</p>
<p>Any module will not show changes to other modules in the system until it HAS BEEN ACTIVATED<br>
Just like other users can pull something in git, but changes won’t be reflected until a push has occured.</p>
<h2 id="identifying-dependencies">Identifying Dependencies</h2>
<p>Many modules can depend on different modules or dictionary items.</p>
<p>Use the “Where-is Used” list to help find dependencies.</p>
<p>Any object that relies on a newly activated object is also activited. This process ensures consistency in activation and will not leave an object pointing to an obsolete object.</p>
<h2 id="repository-info-system">Repository Info System</h2>
<p>Helps yo searc for object dictionary objects and their users.</p>
<p>Can find:</p>
<ul>
<li>Items with certain attributes</li>
<li>Where-used lists</li>
<li>Change verifications</li>
<li>Information and relationships between tables ad dependencies (check tables)</li>
<li></li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

