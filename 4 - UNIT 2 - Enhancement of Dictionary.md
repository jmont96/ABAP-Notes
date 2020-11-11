---


---

<h2 id="enhancement-of-dictionary-items">Enhancement of Dictionary Items</h2>
<p>Objectives:</p>
<h2 id="adding-sap-table-fields">Adding SAP Table Fields</h2>
<p>Append Structures</p>
<ul>
<li>Multiple append structures can be used for a single table</li>
<li>Append strctures can be used like normal structures as types in programs</li>
</ul>
<p>Customization includes</p>
<ul>
<li>Already integrated into SAP tables</li>
<li>Customers add the desired additional fields</li>
</ul>
<h2 id="append-structures-at-upgrade">Append structures at upgrade</h2>
<p>Upon activation, the new fields will be added to the end of the table at the DB level.</p>
<p>Components have to start with ZZ or YY</p>
<p>Enhancement Categories</p>

<table>
<thead>
<tr>
<th>Not classified</th>
<th>Table has no category</th>
</tr>
</thead>
<tbody>
<tr>
<td>Cannot be enhanced</td>
<td>Table cannot be enhanced</td>
</tr>
<tr>
<td>Can be enhanced (char-type)</td>
<td>All table components and their enhancements must be character-type</td>
</tr>
<tr>
<td>Can be enhanced (char or numeric)</td>
<td>Structure and its enhancement cannot contain deep types</td>
</tr>
<tr>
<td>Can be enhanced any way</td>
<td>Can contain any data type</td>
</tr>
</tbody>
</table><h2 id="overwriting-an-sap-field-label">Overwriting an SAP field label</h2>
<p>If F is the type you can’t change it.<br>
4 - Field label for header</p>
<p>Transaction CMOD will help with label changes</p>
<p>You need to restore your customer labels after a delivered upgrade.</p>
<p>Can add enhanced customer documentation in Goto-&gt;text enhancements -&gt; data elements -&gt; new DE customer document</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

