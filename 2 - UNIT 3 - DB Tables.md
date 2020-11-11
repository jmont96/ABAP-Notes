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
<h2 id="internal-tables">Internal Tables</h2>
<p>Hashed Tables:<br>
Uses a hash function to find a single row by its unique key. Typically used for finding small amount of data in a large table.</p>
<p>Sorted Tables<br>
A sorted table is sorted by the key and performs a binary serach to read items.<br>
Good for searching ranges using sorted results.</p>
<p>Tables can be generically defined by:</p>
<ul>
<li>Index table
<ul>
<li>Standard</li>
<li>Sorted</li>
</ul>
</li>
<li>Hashed Table
<ul>
<li>Hashed table</li>
</ul>
</li>
</ul>

<table>
<thead>
<tr>
<th>Table Kind</th>
<th>Standard Table</th>
<th>Sorted Table</th>
<th>Hashed Table</th>
</tr>
</thead>
<tbody>
<tr>
<td>Index Access</td>
<td>+</td>
<td>+</td>
<td>-</td>
</tr>
<tr>
<td>Key Access</td>
<td>+</td>
<td>+</td>
<td>+</td>
</tr>
<tr>
<td>Key Unique?</td>
<td>Non-unique</td>
<td>Both</td>
<td>Unique</td>
</tr>
<tr>
<td>Uses</td>
<td>Mainly Index Access</td>
<td>Mainly Key Access</td>
<td>ONLY Key Access</td>
</tr>
</tbody>
</table><p>To create a work area automatically matched to a table (deprecated):</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span> it_1 <span class="token keyword">TYPE</span> table_type <span class="token keyword">WITH</span> <span class="token keyword">HEADER</span> <span class="token keyword">LINE</span><span class="token punctuation">.</span>
</code></pre>
<p>This will define the table it_1[] and the structure it_1.</p>
<p>To do with separately (safer), create a work area structure:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span><span class="token punctuation">:</span> it_1 <span class="token keyword">TYPE</span> table_type<span class="token punctuation">,</span>
	  s_1 <span class="token keyword">LIKE</span> <span class="token keyword">LINE</span> <span class="token keyword">OF</span> it_1<span class="token punctuation">.</span>
</code></pre>
<p>To read one row from an internal table into a structure work area:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">READ</span> <span class="token keyword">TABLE</span> it_table <span class="token keyword">INTO</span> struct<span class="token punctuation">.</span>
</code></pre>
<p>Moving fields from table to table:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">MOVE-CORRESPONDING</span> it_1 <span class="token keyword">TO</span> it_2<span class="token punctuation">.</span>
</code></pre>
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
<p>Note: Can access data contained in pooler or clustered tabled with OPEN SQL, but NOT Native SQL</p>
<p>Older systems may still have these, but its really not that important</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

