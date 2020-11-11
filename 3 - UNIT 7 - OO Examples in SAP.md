---


---

<h1 id="oop-examples-in-sap">OOP Examples In SAP</h1>
<p>Objectives:</p>
<ul>
<li>Implement a simlpel ALV Grid</li>
<li>Handle a double click event in an ALV</li>
<li>Describe BADIs</li>
</ul>
<h2 id="abap-list-viewer-alv">ABAP List Viewer (ALV)</h2>
<p>Nice feature for displaying non-hierarchial lists in a grid<br>
At its core, an ALV is just a table that allows you to perform certain functions like print, export and sort.</p>
<p>ALVs work with screens in a special way, by being placed into containers and using an included method to instantiate the grid.</p>
<p>these containers provide the technical connection between screens and application controls like na ALV Grid.</p>
<p>ALV’s must be placed in a screen with a fixed size value, so you will need two variables to accomplish this.</p>
<pre class=" language-abap"><code class="prism  language-abap">CL_GUI_CUSTOM_CONTAINER
CL_GUI_ALV_GRID<span class="token punctuation">.</span>
</code></pre>
<p>Follow these steps to create an ALV.</p>
<ol>
<li>Use the screen painter to define a control area on your screen.</li>
<li>Create an instance of CL_GUI_CUSTOM_CONTAINER and move the name of custom control area to the constructor</li>
<li>Create an instance of CL_GUI_ALV_GRID and pass the container variable to the constructor</li>
<li>Call the method SET_TABLE_FOR_FIRST_DISPLAY() from the ALV variable and pass the internal table it. We will now display this table’s data in the ALV</li>
<li>This must be done in a PBO module for best success</li>
</ol>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">MODULE</span> alv <span class="token keyword">OUTPUT</span><span class="token punctuation">.</span>

	<span class="token keyword">DATA</span> container <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> cl_gui_custom_container<span class="token punctuation">,</span>
		grid <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> TP cl_gui_alv_grid<span class="token punctuation">.</span>

	<span class="token keyword">CREATE</span> <span class="token keyword">OBJECT</span> container 
		<span class="token keyword">EXPORTING</span> container_name <span class="token operator">=</span> <span class="token string">'container_1'</span><span class="token punctuation">.</span>

	<span class="token keyword">CREATE</span> <span class="token keyword">OBJECT</span> grid
		<span class="token keyword">EXPORTING</span> i_parent <span class="token operator">=</span> container<span class="token punctuation">.</span>

	grid<span class="token token-operator punctuation">-&gt;</span>set_table_for_first_display<span class="token punctuation">(</span>
			i_structure_name <span class="token operator">=</span> <span class="token string">'SAPLANE'</span>
			it_outtab 		 <span class="token operator">=</span> gt_saplane
			<span class="token punctuation">)</span><span class="token punctuation">.</span>
		
<span class="token keyword">ENDMODULE</span><span class="token punctuation">.</span>
</code></pre>
<p>Again, we need to define modules for a grid in the PBO section of a screen.</p>
<h2 id="business-add-ins-badi">Business Add Ins (BADI)</h2>
<p>Adapters can be added to connect your standard SAP instance to an SAP industry solution or a customer enhancement. This is a Business Add In, or a BADI.</p>
<p>How does this work?</p>
<ol>
<li>SAP will typically create a BADI interface (if_ex_)</li>
<li>Then, they will have methods and data in this interface. This is editable by the customer if they choose.</li>
<li>Finally, there can be a BADi adapter class, which implements the methods that are defined in the BADI interface. This is nice because the customer can make these methods do whatever they want for their specific needs.</li>
</ol>
<p>These BADIs are defined in multiple areas:</p>
<ul>
<li>Repository Info System (se84)</li>
<li>Application Hierarchy (se81)</li>
<li>And more!</li>
</ul>
<p>We need to search for the specific BADI’s we want to use before we can successfully implement them</p>
<p>Multiple BADI implementations are possible for continued additions.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

