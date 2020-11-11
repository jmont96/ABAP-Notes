---


---

<h1 id="web-dynpro-context">Web Dynpro Context</h1>
<h2 id="contexts">Contexts</h2>
<p>Context: hierarchial dataa storage stucture. Data held in the context exist only for the lifespan of tehc ontrller.<br>
the strucutre (metadata) is tpically defined at design time but can be modified at functime dynamically.</p>
<p>Changing the context</p>
<ol>
<li>Open any controller using the change option in teh menu</li>
<li>Choose the context tab</li>
<li>Properties can be displayed by selecting the context nodes</li>
</ol>
<h2 id="context-structure-at-runtime">Context structure at runtime</h2>
<p>Nodes can be nested basically<br>
Runtime system won’t automatically instantiate a node sometimes, you might need to create it (if you have a range in the cardinality, some objects are yet to be defined at runtime)</p>
<h2 id="cardinality">Cardinality</h2>
<p>0…1 : zero or one element permitted<br>
0…n zero or more eleemnts permitted<br>
1…1 Exactly one element permitted<br>
1…n one or more element permitted</p>
<p>cardinality violations:</p>
<ul>
<li>Deleting the default element of a node with cardinality 1…1 or 1…n</li>
<li>Adding a second element to a node with a cardinality of 0…1 or 1…1</li>
</ul>
<h2 id="lead-seleciton-index">Lead seleciton index</h2>
<p>Each context node has the attibute LEAD_SELECITON_INDEX.<br>
The attiribute is an integer and is used to simpliy access to the node’s colection.<br>
Automatically set to 1 as soon as first element has been created, but can be set by program source code.<br>
If a single row.<br>
Lead seleciton is basically an index in the node that points to a certain element</p>
<p>Lead election index is important in the follwing situations:</p>
<ul>
<li>If a single row is selected in a table, the LSI automatically adjust according to the selected row</li>
<li>Form fields ma be bound to attributes of a context node with the cardinality 0:n or 1:n. in this case, hte form data originiates from the element related to the node’s lead selection index</li>
<li>special methods (supply funtions) can be assign to context nodes. The framwork may call a supply function automatically if the lead selection in a parent node changes.</li>
</ul>
<h2 id="singleton-property">Singleton Property</h2>
<p>Singleton proporty: can only instatiate one object.<br>
If we have a node N1 that contains node N2 and singleton is true for N2, for all elements of the parent node n1 only one common instance of node n2 is created (only one instance of N2 that is shared). If singleton is false for N2, for each element of parent N1, an own instance of N2 is created (each element has their own instance of N2).</p>
<h2 id="mapping">Mapping</h2>
<p>Context mapping allows a controller (typically a VC) to access data that was preprocessed by some other controller. This data is a reference so no duplicaiton is needed.</p>
<p>The node that acts as the data source is known as the mapping origin node and node that is mapped is known as the mapped node.</p>
<p>If a view controller acts as a data source for a mapping relationship (origin) a situation can arise in which the component controller is dependent upon the VC. This is NOT permitted cuz its awful design.</p>
<p>To establish mapping, the target controller has to declare the source controller as a used controller in its properties.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

