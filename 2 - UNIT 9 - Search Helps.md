---


---

<h1 id="search-helps">Search Helps</h1>
<p>Objectives:</p>
<ul>
<li>Describe the input help process</li>
<li>Create collective search helps</li>
<li>Create elementary search helps</li>
<li>Create append search helps to enchance basic search helps</li>
<li>Implement search helps exits</li>
</ul>
<h2 id="creating-search-helps">Creating Search Helps</h2>
<p>Can assign a search help to a data element, structure or a table field.</p>
<p>Search help is a list of possible values that could fill the input.</p>
<p>A search helps controls data consistency and reduces user error</p>
<p>Design</p>
<ul>
<li>A search help has a selection method that selects data from the Dictionary to show in the search help</li>
<li>You can create new views to populate your search helps</li>
</ul>
<p>Parameters</p>
<ul>
<li>A search help has import and export params</li>
<li>You first send an input param to the search help and it sends back the full object from the table that is mapped to the help as an export object</li>
<li>This then populates the corresponding fields</li>
</ul>
<p>Enhancements</p>
<ul>
<li>Type ahead search
<ul>
<li>User’s search term is automatically completed based on what they have typed (autocomplete)</li>
</ul>
</li>
<li>Full text search
<ul>
<li>All columns are searched for the entered string</li>
</ul>
</li>
</ul>
<h2 id="assigning-search-helps">Assigning Search Helps</h2>
<p>What can I assign a search help to?</p>
<ul>
<li>Structure field</li>
<li>Data element</li>
<li>Check table</li>
</ul>
<h2 id="collective-search-helps">Collective Search Helps</h2>
<p>Combine several search paths.</p>
<h2 id="append-search-helps">Append Search Helps</h2>
<p>Always do enhancements in display mode<br>
Appends are used to only add enhancements, not perform modifications</p>
<p><strong>Enhancements are upgrade safe, modifications are not!</strong></p>
<h2 id="exits">Exits</h2>
<ul>
<li>A function that calls and will be executed automcatially during different steps in the process</li>
<li>ABAP can be executed before someone sees a search help</li>
<li>When you go to run it, something can be executed before the select call is made for the search help</li>
<li>When they double click, code can be executed before the export vars are returned to the user’s search help screen</li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

