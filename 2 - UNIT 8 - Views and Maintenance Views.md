---


---

<h1 id="views">Views</h1>
<p>Objectives:</p>
<ul>
<li>Describe Views</li>
<li>Dfine DB views</li>
<li>Decribe M views</li>
<li>Create M views</li>
<li>Identify when to use M views</li>
<li>Define complex M dialogs</li>
</ul>
<h2 id="database-views">Database Views</h2>
<p>A <strong>view</strong> is basically a join from several tables<br>
A <strong>projection</strong> is hiding unimportant data<br>
A <strong>display</strong> is data records that satisfy certain conditions</p>
<p>The data in a view can be displayed just like a table data in extended table maintenance.</p>
<p>The most common thing we do with views is define how to join tables together and how we want to design how the data is shown to the user.</p>
<p>Must define a join condition for the view to make it work (WHERE)</p>
<p>You can include entire tables in views.</p>
<p>Basically just a select and join statement lol idk why they call it a view</p>
<p>With a view</p>
<ul>
<li>Don’t need to specify join in your Select statement, its automatically built into the view.</li>
<li>You have a ‘pre-prepared’ part of a select statement in a view that can be treated like a table</li>
</ul>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">Select</span> <span class="token operator">*</span> 
<span class="token keyword">INTO</span> internal_table 
<span class="token keyword">FROM</span> view_variable 
</code></pre>
<p>To define a view:</p>
<ul>
<li>define the tables and fields you need to be included in the view
<ul>
<li>This should be from multiple tables using different keys</li>
</ul>
</li>
<li>Then, create any conditions in the conditions tab</li>
<li>Finally, allow buffering in the technical settings if you please</li>
</ul>
<h2 id="maintenance-views">Maintenance Views</h2>
<p>Application object - data distributed across more than one table</p>
<p>You can maintain AO’s by using a maintenance view.</p>
<p>A maintenance view automatically distributes data across underlying tables.</p>
<p>All tables used must be linked with a foreign key, and the join conditions are always derived from these keys. you cannot manually enter them like in a DB view.</p>
<p>Each field in a maintenance view must have one of the following attributes</p>
<ul>
<li>R - read only
<ul>
<li>Not user input, filled automatically</li>
</ul>
</li>
<li>H - hidden
<ul>
<li>Not shown, but still used</li>
</ul>
</li>
<li>S - subset
<ul>
<li>Resctricts the work area, the system only shows records which match the subset value specified.</li>
</ul>
</li>
</ul>
<p>Steps for creation:</p>
<ol>
<li>Copy tables to be used and define the join condition. Tables must be connected by foreign key(s)</li>
<li>Copy view fields. All key fields must be included</li>
<li>Define selection conditions (Where)</li>
<li>Define maintenace status. this determines how you can access the table.</li>
<li>Activate View</li>
</ol>
<h2 id="maintenance-view-dialogs">Maintenance View Dialogs</h2>
<p>To create, you must speficy these params</p>
<ul>
<li>Function group</li>
<li>Auth group</li>
<li>Maintenance type</li>
<li>Maintenance Screens</li>
<li>Recording Routine</li>
</ul>
<h2 id="view-clusters">View Clusters</h2>
<p>Used for combining multiple maintenance dialogs into one maintenance unit.</p>
<p>Maintenance views can only maintain tables that a 1:1 relationship with one another, but you can use clusters to maintain tables than have an N:M relationship.</p>
<p>This can be done without key dependency</p>
<p>A max of 14 dialogs can be combined</p>
<p>You have to make all of M views before the cluster</p>
<p>Use sm34 to create a cluster</p>
<p>Advantages</p>
<ul>
<li>Navigation
<ul>
<li>Comfortably navigate between individual M dialogs</li>
</ul>
</li>
<li>Consistency
<ul>
<li>Ensures data consistency when changes manually transported data</li>
</ul>
</li>
</ul>
<p>REVIEW NOTES</p>
<p>Maintenance views - programs to update data<br>
maintenance views and view clusters are not important exam topics<br>
generated for customer tables essentially…</p>
<p>DB views are the common ones! quite important!</p>
<p>View is a logical object, doesn’t physically store data, only stored defintion on how to access data. Nice for defining pre-made joins of tables. its a view of data that is distributed across multiple tables. You can specify the fields you want . Projection hides data. No join option for a project. Provide a table name and choose fields. Projection’s are quite limited, don’t have buffering or other tchnical settings. No option for conditions either.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

