---


---

<h1 id="table-changes">Table Changes</h1>
<p>Objectives</p>
<ul>
<li>Effect of table changes</li>
<li>Convert transparent tables</li>
<li>Correct conversion errors</li>
<li>Add enhancements to tables by appending structures</li>
</ul>
<h2 id="performing-a-table-conversion">Performing a Table Conversion</h2>
<ul>
<li>The DB is not always changed to reflect changes in the ABAP Dictionary
<ul>
<li>When order of fields changes (except key fields)</li>
</ul>
</li>
<li>Changes can be made through a couple methods, though
<ul>
<li>Delete the database table adn create it again</li>
<li>Use ALTER TABLE to change the DB catalog
<ul>
<li>Indexes may have to be built again</li>
</ul>
</li>
<li>Converting the table</li>
</ul>
</li>
</ul>
<p>Table Change Types:</p>
<ul>
<li>Table Growth
<ul>
<li>Use ALTER TABLE</li>
</ul>
</li>
<li>Table shrinkage
<ul>
<li>Use table conversions</li>
</ul>
</li>
</ul>
<p>Conversions</p>
<ul>
<li>Most resource-intensive process listed above</li>
<li>Saves a lot of time fixing other complications that result from other methods</li>
<li>Conversion can only happen if you’re trying to shrink a table</li>
<li>Steps
<ul>
<li>The system creates an inactive version of the table in the ABAP Dictionary</li>
<li>Step 1
<ul>
<li>Table becomes locked to prevent further changes while in conversion. The table will stay locked until conversion is completed correctly.</li>
</ul>
</li>
<li>Step 2
<ul>
<li>The table is renamedm all secondary indexes are deleted.</li>
</ul>
</li>
<li>Step 3
<ul>
<li>Inactive Version is activated in ABAP Dcitionary, and a temp table is created in the DB with a primary index. Active version points to old, now empty Table.</li>
</ul>
</li>
<li>Step 4
<ul>
<li>Data is loaded back from newly created table into old table using Move-Corresponding. Now both tables contain the data.</li>
</ul>
</li>
<li>Step 5
<ul>
<li>New table is deleted</li>
</ul>
</li>
<li>Step 6
<ul>
<li>Secondary indexes are created again. Views are activated again.</li>
</ul>
</li>
<li>Step 7
<ul>
<li>Lock is removed and table can be changed by system.</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2 id="enhancing-tables-using-append-structures">Enhancing Tables Using Append Structures</h2>
<p>Allows you to append fields to SAP tables and SAP structures without having to modify the table defintion.</p>
<p>Cannot be done with pooled or cluster tables.</p>
<p>This approach can cause a lot of problems</p>
<ul>
<li>Affect dependednt structures</li>
<li>Can lead to syntax errors adn runtime problems</li>
<li>Can affect value asignments, operator checks and access attempts</li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

