---


---

<h1 id="input-checks">Input Checks</h1>
<p>Objectives:</p>
<ul>
<li>Create fixed values for a domain</li>
<li>Define foreign keys to ensure data consistency</li>
<li>Create a text table</li>
</ul>
<h2 id="fixed-values">Fixed Values</h2>
<ul>
<li>A range of, or specifically set values that can be used for a domain value.</li>
<li>Can be an interval or defined individually</li>
<li>Can use fixed value appends
<ul>
<li>Enhancements (upgrade-safe)</li>
<li>Append can have one domain</li>
<li>Domain can have multiple appends</li>
</ul>
</li>
</ul>
<p>Fixed values are stored in what is called a Value Table.</p>
<p>Having a value table will NOT provide a search help or validation for input</p>
<h2 id="foreign-keys--input-checks">Foreign keys &amp; Input Checks</h2>
<p>A foreign key is a key field that is mapped to another table.<br>
Foreign keys are needed to map to a check table.<br>
A check table is used to check key fields.<br>
The field of the foreign key to be checked is called a check field.<br>
A check table that maps to the table’s fixed values will create a search help that is usable on the front-end.</p>
<p>Must have same domain to check a field from a check table field</p>
<h2 id="cardinalitymultiplicity">Cardinality/Multiplicity</h2>
<ul>
<li>1:1 - each check table has one entry in non-sap key table</li>
<li>1:n - each check table entry has 1 or more non-sap key table entries</li>
<li>1:C - each check table entry has 0 or 1 matching entries in the key table</li>
<li>1:CN - entries in check table can have 0-n matching entries in the key table</li>
<li>1:Cn is by farrrrr the most common relationship here</li>
</ul>
<h2 id="text-tables">Text Tables</h2>
<p>Used for validating language dependent text data.<br>
Each table can only have one text table.<br>
Tables must be linked using a foreign key</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

