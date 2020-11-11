---


---

<h1 id="classic-business-add-ins">Classic Business Add-Ins</h1>
<p>Objectives:</p>
<ul>
<li>Describe a class BADI</li>
<li>Enhance programs using BADIs</li>
<li>Explain additional details of BADIs</li>
</ul>
<h2 id="overview">Overview</h2>
<p>Defintion of BADI:</p>
<ul>
<li>BADI name</li>
<li>Interface</li>
<li>Defintion of filters</li>
<li>Properties</li>
</ul>
<p>Essential activies in SAP program</p>
<ul>
<li>Get BADI adapter class instance</li>
<li>Determine and execute all implementations</li>
</ul>
<p>Implementation of a BADI:</p>
<ul>
<li>Implement class, which must implement the interface</li>
<li>Filter values</li>
<li>Properties<br>
On BADI can have many implementations with filter conditions and implementing classes</li>
</ul>
<p>These must be created when a BADI is defined:</p>
<ul>
<li>Interface</li>
<li>Generated Class that implement the interface (adapter pattern)</li>
<li>Filtering
<ul>
<li>If it is a filter-dependent BADI</li>
<li>Filters allow different behavior based on values</li>
</ul>
</li>
<li>Control
<ul>
<li>The BADI adapter calls the active implementations</li>
</ul>
</li>
</ul>
<h2 id="flow-of-badi-program">Flow of BADI Program</h2>
<ol>
<li>A reference variable of the BADI interface is created in the declaration section.</li>
<li>An instance is grabbed from a method of the service class CL_EXITHANDLER and you pass in the reference variable which becomes the adapter.</li>
<li>That variable can now use the BADI instance and its methods are called when wanted.</li>
</ol>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span> r_var <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> badi_interface_name<span class="token punctuation">.</span>

<span class="token keyword">CALL</span> <span class="token keyword">METHOD</span> cl_exithandler<span class="token token-operator punctuation">=&gt;</span>get_instance
	<span class="token keyword">CHANGING</span> instance <span class="token operator">=</span> r_var<span class="token punctuation">.</span>

<span class="token keyword">CALL</span> <span class="token keyword">METHOD</span> r_var<span class="token token-operator punctuation">-&gt;</span>meth_abc
	<span class="token keyword">EXPORTING</span> variables
	<span class="token keyword">IMPORTING</span> variables<span class="token punctuation">.</span>
</code></pre>
<h2 id="finding-a-badi">Finding a BADI</h2>
<ul>
<li>System -&gt; status -&gt; double click program name</li>
<li>Double-click ref variable</li>
<li>Where-used list</li>
<li>SE18</li>
<li>Documentation for BADI</li>
<li>IMG</li>
<li>Repo info system</li>
<li>By name: CL_EX_BADI_NAME</li>
</ul>
<ol>
<li>Can search in an application program for the string CL_EXITHANDLER. Double clicking on the following method will use forward nav to lead you to the instance</li>
<li>Use the repo info system to perform a general search</li>
<li>Search for BADIs by using the entries in the releant Custimizing component</li>
</ol>
<h2 id="extendable-filter-types">Extendable Filter types</h2>
<ul>
<li>Could have filter table</li>
<li>Could have a data element that has a domain which uses fixed values in a value table and text table for translation with 2 fields (language field).
<ul>
<li>Text table assigned to a value table always shows up when there is a foreign key assignment.</li>
</ul>
</li>
<li>The data element respresents the filter type</li>
</ul>
<h2 id="default-implementation">Default Implementation</h2>
<ul>
<li>Created by provider</li>
<li>Executed if no other active BADI implemenations are available</li>
</ul>
<h2 id="technique-comparison">Technique Comparison</h2>
<p>BADIs do it all!</p>

<table>
<thead>
<tr>
<th></th>
<th>Customer Exit</th>
<th>BTE</th>
<th>BADI</th>
</tr>
</thead>
<tbody>
<tr>
<td>Program Exit</td>
<td>+</td>
<td>+</td>
<td>+</td>
</tr>
<tr>
<td>Menu Exit</td>
<td>+</td>
<td>-</td>
<td>+</td>
</tr>
<tr>
<td>Screen Exit</td>
<td>+</td>
<td>-</td>
<td>+</td>
</tr>
<tr>
<td>Append Fields</td>
<td>+</td>
<td>-</td>
<td>+</td>
</tr>
<tr>
<td>Administration Level</td>
<td>+</td>
<td>-</td>
<td>+</td>
</tr>
<tr>
<td>Multiple Implementations?</td>
<td>-</td>
<td>+</td>
<td>+</td>
</tr>
<tr>
<td>Filters?</td>
<td>-</td>
<td>+</td>
<td>+</td>
</tr>
</tbody>
</table><h2 id="naming-conventions">Naming conventions</h2>
<p>BADI defintion - BADI or ZBADI or /…/BADI<br>
Interface - IF_EX_BADINAME OR ZIF_EX_BADINAME<br>
Methods - any name<br>
Generated BADI class (adapter class) - CL_EX_BADI OR ZCL_EX_BADI<br>
Implementation - IMPL or ZIMPL<br>
Implementing class - CL_IM_BADINAME</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

