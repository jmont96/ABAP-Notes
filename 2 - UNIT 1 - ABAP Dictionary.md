---


---

<h1 id="abap-dictionary">ABAP Dictionary</h1>
<p>Objectives:</p>
<ul>
<li>Describe the functions of the ABAP Dictionary</li>
</ul>
<p>The ABAP Dictionary allows the system to be managed centrally with consistent type definitions. Basically, a dictionary for finding definitions of data in ABAP.</p>
<h2 id="dictionary-elements">Dictionary Elements</h2>
<p>The ABAP Dictionary includes:</p>
<ul>
<li>Type Definitions
<ul>
<li>Data Elements
<ul>
<li>Basic type defined by data type, length and decimal places and semantic info</li>
</ul>
</li>
<li>Structures
<ul>
<li>Object of components with differing types</li>
</ul>
</li>
<li>Table types
<ul>
<li>Describe structure of an internal table</li>
</ul>
</li>
</ul>
</li>
</ul>
<p>With the dictionary, you can perform:</p>
<ul>
<li>Create user-defined type, such as data elements, structures, table type and more</li>
<li>Create DB objects such as tables, indexes and views</li>
<li>Development supporting services that process computations and screen actions
<ul>
<li>Bad practice: placing data  on a screen that isn’t backed by a data element</li>
</ul>
</li>
</ul>
<p>Example services in the dictionary:</p>
<ul>
<li>Input helps</li>
<li>Field helps</li>
<li>Input checks</li>
<li>Lock sets and releases</li>
<li>Data buffering</li>
<li>Logging</li>
</ul>
<p>The ABAP dictionary is essentially just a program that contains objects above the database layer. The DB holds the data and the definition is stored in the dictionary.</p>
<p>Changes in the dictionary definition are automatically reflected in the DB.</p>
<p>We can’t do DDL (Data definition language - to make CRUD updates) statements at the database level, we must use the dictionary.</p>
<p>We need to use SQL commands on the dictionary through manipulation, then the database interface manipulates the DB object for us.</p>
<h2 id="dictionary-integration">Dictionary Integration</h2>
<p>All changes in the ABAP dictionary are immediately reflected in the ABAP programs and screens, since the Dictionary is integrated into all tools in the system.</p>
<p>When a program is executed, the ABAP interpreter accesses the Dictionary to get type definitions.</p>
<p>The DB interface also directly uses the Dictionary to access specific data for elements of different types.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

