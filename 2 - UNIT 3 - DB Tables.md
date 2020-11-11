---


---

<h1 id="db-tables">DB Tables</h1>
<p>Objectives</p>
<ul>
<li>Create Transparent Tables</li>
<li>Define INCLUDE structures</li>
<li>Create tables in the ABAP Dictionary</li>
<li>Define cluster tables and pooled tables</li>
</ul>
<h2 id="transparent-tables">Transparent Tables</h2>
<p>Characteristics</p>
<ul>
<li>Has key fields and function fields</li>
<li>Key fields are unique to the table</li>
<li>Every field or column in the table will be based on a data element which uses a domain to back its technical information.</li>
<li>Field uses DE which uses Domain</li>
<li>Tables can have fields that have different data types that share a domain
<ul>
<li>Example - departure and arrival airport - both are airports but different field names</li>
</ul>
</li>
</ul>
<p>Hashed Tables</p>
<p>General properties and technical settings</p>
<ul>
<li>Buffer on/off</li>
<li>Size category (how many records)</li>
<li>Data class (what area of the DB shluld the table be stored)
<ul>
<li>Examples: Master data, transactional data</li>
</ul>
</li>
<li>Logging on off (should change events be logged?)</li>
</ul>
<p>Data class</p>
<ul>
<li>Data tables can be organized into the following categories
<ul>
<li>Master data
<ul>
<li>Rarely edited</li>
</ul>
</li>
<li>Organizatiol data
<ul>
<li>Rearely modified</li>
</ul>
</li>
<li>Transaction data
<ul>
<li>Grows quickly</li>
</ul>
</li>
<li>System data
<ul>
<li>System configs</li>
</ul>
</li>
</ul>
</li>
</ul>
<p>Size category</p>
<ul>
<li>As a table grows, it allocates more space in the database</li>
<li>The size categroy is a number like 1, 2, 3 and maps to keywords like ‘TABA’ and ‘TABB’ and ‘TABC’</li>
</ul>
<p>Log data changes</p>
<ul>
<li>If rec/client is set to ‘ALL’ or your client number, then logging will work</li>
<li>There is a separate log table that refers to the target table
<ul>
<li>This will save changes whenever they occur in the target table</li>
</ul>
</li>
</ul>
<p>There are also DB specific properties:</p>
<ul>
<li>Column store vs row store for storage type</li>
<li>Other general properties that don’t matter much</li>
</ul>
<p>Transparent Tables</p>
<ul>
<li>Everything in the table will exist exactly the same in the DB
<ul>
<li>Same name</li>
<li>Same data</li>
<li>Same everything</li>
</ul>
</li>
</ul>
<h2 id="cluster-tables-and-pool-tables">Cluster Tables and Pool Tables</h2>
<p>SAP is trying to kinda phase these out… won’t find them in newer systems. They are made up of multiple tables in the dictionary that then are combined in the DB.</p>
<p><strong>Cluster Tables</strong></p>
<ul>
<li>Store functionaly dependent data.</li>
<li>There is a cluster key that is the key of the table cluster</li>
</ul>
<p><strong>Pooled Tables</strong></p>
<ul>
<li>Tables are not dependednt on one another</li>
<li>Tables are combined into a table pool</li>
</ul>
<p>Advantages</p>
<ul>
<li>Fewer tables and fields</li>
<li>Data compression</li>
<li>Encrypted storage</li>
</ul>
<p>Limitations</p>
<ul>
<li>No joins, group by, order by and other functionalities</li>
<li>No table appends</li>
<li>For cluster tables, selection is limited to cluster key fields</li>
<li>For pools, longer keys are needed than necessary</li>
</ul>
<p>Older systems may still have these, but its really not that important</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

