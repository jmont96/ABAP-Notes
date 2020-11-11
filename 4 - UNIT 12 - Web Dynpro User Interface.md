---


---

<h1 id="web-dynpro-user-interface">Web Dynpro User Interface</h1>
<h2 id="ui-elements">UI elements</h2>
<ul>
<li>Textview</li>
<li>Label</li>
<li>Button</li>
<li>Image</li>
<li>InputField</li>
</ul>
<p>Categories:</p>
<ul>
<li>Text
<ul>
<li>Can be used to display texts or to enter literals</li>
</ul>
</li>
<li>Action
<ul>
<li>Simple elemets that the user can choose to trigger something like navigation</li>
</ul>
</li>
<li>Selection
<ul>
<li>Displays multiple values for choosing</li>
</ul>
</li>
<li>complex
<ul>
<li>Contains elements that require subelements to define a valid ui element</li>
</ul>
</li>
<li>Layout
<ul>
<li>Structure layout</li>
</ul>
</li>
<li>Graphics
<ul>
<li>Render graphics of the page</li>
</ul>
</li>
<li>Integration
<ul>
<li>Embed all kinds of non-ABAP technologies into WD</li>
</ul>
</li>
</ul>
<p>Hardcoded UI elements are not great practice, typically we want to dyanlically control them.</p>
<p>Controlling UI element behavior with Data binding<br>
to control behavior of UI elements, you need to manipulate the data that backs the UI element in the controller context.</p>
<p>UI elements can be bound to nodes or attirbutes in the context, meaning it gets its value from the element it is bound to.</p>
<p>If the UI element can be manipulated on the frontend, the contet data is updated accordingly.</p>
<p>If validation is set up and fails, the context data will NOT be changed.</p>
<h2 id="defining-binding">Defining Binding</h2>
<p>If a value is hardcoded at design time, it can only be changed at runtime by the hook method WDDOMODIFYVIEW() because only this method provides a reference to the UI element hierarchy. This is considered poor design.</p>
<p>To control the behavior programmatically, create a context attibute with a data type that mathces the property you wish to control. This allows you to control the behavior of the UI element by modifying the related attribute’s value.</p>
<h2 id="composite-ui-elements">Composite UI Elements</h2>
<p>Any UI element that requires child UI elements<br>
Table UI, TableColumn elements and Tree UI are examples<br>
Composite UI ellements are incapable of displayng information on their own. They must have child UI eleements to display data.<br>
A table UI element must be bound to a context node of cardinality 0…1 or 1…n</p>
<h2 id="child-ui-elements-of-a-table-column">Child UI Elements of a Table Column</h2>
<p>To present information to the user, a TableColumn UI element must have a child UI element that acts as a cell editor. The kind of interaction between the user and the data in each column must be clarified.</p>
<p>The mandatory table cell editors must be bound to child attributes of the same node to which the parent Table UI element is bound.</p>
<h2 id="selection-of-table-rows">Selection of Table Rows</h2>
<p>When you choose the selection button of a table row on the rendered screen, a round trip is initiated.  This round trip causes the lead selection of the context node to which this table is bound to be altered.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

