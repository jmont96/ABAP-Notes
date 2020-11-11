---


---

<h1 id="customer-exits">Customer Exits</h1>
<h2 id="enhancement-projects">Enhancement Projects</h2>
<p>Implementation of customer exits that are used to create enhancements<br>
To create an enhancement:</p>
<ol>
<li>plan out needed enhancements</li>
<li>Programmers combine these in SAP enhancements</li>
<li>Programmers document their enhancements</li>
</ol>
<p>To implement enhancements:</p>
<ol>
<li>Create enhanecement project in CMOD</li>
<li>Choose the SAP enhancements that you want to use</li>
<li>Edit individual componetsn using the project management function</li>
<li>Document the entire project</li>
<li>Activate the project</li>
</ol>
<p>To create a project in CMOD:</p>
<ol>
<li>Run CMOD to start Project Management function</li>
<li>Name your enhancement project</li>
<li>Go to project attributes and enter a short text that describes the enhancement project</li>
</ol>
<p>Projects need change requests, and should be placed in same change request as all of the enhancement modules like subscreens, menu exits and others.</p>
<h2 id="program-exits">Program Exits</h2>
<p>Basically customer additions that can be called from SAP standard code in order to enhance the SAP standard.<br>
Program exits Syntax<br>
Call a function in the customer namespace</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CALL</span> <span class="token keyword">CUSTOMER-FUNCTION</span> <span class="token string">'001'</span>
	PARAMS<span class="token punctuation">.</span>
</code></pre>
<p>Then the function will have an include with a name that starts with Z or Y</p>
<p>Program exit search<br>
Loop in System -&gt; status -&gt; double-click proram name Call customer-function</p>
<p>Implemetating Program Exit<br>
Choose component and change it, then add your include for the exit program, then add your code in the include program</p>
<h2 id="function-group-structure">Function Group Structure</h2>
<p><strong>SAPL</strong> is the naming convention for a program that is a function group<br>
Top include is for global data<br>
function UXX  is an include file full of include files<br>
each one of those include files is a function module<br>
Exits usually start with LX or ZX<br>
Exits will enhance the current data or function module that exists in the function group program</p>
<p>Subroutines are in F01<br>
PBO - O01<br>
PAi - I01<br>
E01 - Events<br>
U01 - Exits</p>
<p>Can’t put a subroutine inside of a function itself</p>
<h2 id="menu-exits">Menu Exits</h2>
<p>Overview:</p>
<ul>
<li>A customer function in a menu of a GUI status that allows for customer functionality</li>
<li>These can be seen in the dropdown list of a specified menu</li>
<li>To privude menu exits, SAP devs must add function codes that begin with ‘+’ … Example: (+ABC)</li>
<li>Same calling of function, but put it into a CASE using the ok_code</li>
</ul>
<p>To use a menu exit:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CASE</span> ok_code<span class="token punctuation">.</span>
	<span class="token keyword">WHEN</span> <span class="token string">'+ABC'</span><span class="token punctuation">.</span>
		<span class="token keyword">CALL</span> <span class="token keyword">CUSTOMER-FUNCTION</span> <span class="token string">'001'</span> <span class="token eol-comment comment">"Runs customer function</span>
			Params<span class="token punctuation">.</span>
<span class="token keyword">ENDCASE</span><span class="token punctuation">.</span> 
</code></pre>
<h2 id="screen-exits">Screen Exits</h2>
<p>Allows you to use reserved sections a main screen (technically are subscreen areas) to display information or allow the user to enter additional data.</p>
<p>You must use a customer included subscreen provided by the SAP developer.</p>
<p>Another subscreen can be displayed in these subscreens.</p>
<p>To call a Subscreen:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">PROCESS</span> <span class="token keyword">BEFORE</span> <span class="token keyword">OUTPUT</span><span class="token punctuation">.</span>
	<span class="token keyword">MODULE</span> module_name<span class="token punctuation">.</span>
		<span class="token keyword">CALL</span> <span class="token keyword">SUBSCREEN</span> abcd
			<span class="token keyword">INCLUDING</span> sy<span class="token token-operator punctuation">-</span>cprog <span class="token string">'1234'</span><span class="token punctuation">.</span> 
<span class="token eol-comment comment">"1234 is dynpro number, sy-cprog is the program name</span>
<span class="token keyword">ENDMODULE</span><span class="token punctuation">.</span>
</code></pre>
<p>Reminders about subscreens:</p>
<ul>
<li>Does not need an OK_CODE</li>
<li>You cannot define GUI Status’s</li>
<li>Flow logic of screen sequence is only done in the main screen</li>
<li>A function code can only be processed in the main screen</li>
<li>Not all subscreens are for screen exits</li>
</ul>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">PROCESS</span> <span class="token keyword">BEFORE</span> <span class="token keyword">INPUT</span><span class="token punctuation">.</span>
	<span class="token keyword">MODULE</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
		<span class="token keyword">CALL</span> <span class="token keyword">CUSTOMER</span> <span class="token keyword">SUBSCREEN</span> abcd<span class="token punctuation">.</span>
	<span class="token keyword">ENDMODULE</span><span class="token punctuation">.</span>
</code></pre>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

