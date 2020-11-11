---


---

<h1 id="selection-screens">Selection Screens</h1>
<p>Objectives:</p>
<ul>
<li>Explain selection screens</li>
<li>Create parameteres on selection screens</li>
<li>Create input fields with the select-options statement</li>
<li>Initialize a selection screen</li>
<li>Change the design of a screen</li>
<li>Create additional selection screens</li>
<li>Define tabstrips on a selection screen</li>
<li>Implement input checks</li>
<li>Implement field and value help</li>
<li>Create a variant</li>
</ul>
<h2 id="overview">Overview</h2>
<ul>
<li>Parameters and Select options will create a screen for selection</li>
<li>Screen number 1000 is default number for the selection screen</li>
<li>Can use variants for selection screen input fields</li>
<li>Can also use something called the logical database, which can retrieve data.
<ul>
<li>Has a built-in selection screen that you call… you can use NODES to show a selection screen for a table (don’t worry too much about this right now)</li>
</ul>
</li>
</ul>
<h2 id="usage">Usage</h2>
<ul>
<li>Can create multiple screens and call them on demand</li>
<li>Screen 1000 shows up autmatically, but you can use others like this</li>
</ul>
<p>To begin a specific selection screen different from 1000:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">SELECTION-SCREEN</span> <span class="token keyword">BEGIN</span> <span class="token keyword">OF</span> <span class="token keyword">SCREEN</span> <span class="token number">1100</span><span class="token punctuation">.</span>
<span class="token keyword">PARAMETERS</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">SELECTION-SCREEN</span> <span class="token keyword">END</span> <span class="token keyword">OF</span> <span class="token keyword">SCREEN</span> <span class="token number">1100</span><span class="token punctuation">.</span>

<span class="token keyword">CALL</span> <span class="token keyword">SELECTION-SCREEN</span> <span class="token number">1100</span><span class="token punctuation">.</span>
</code></pre>
<p>OBLIGRATORY - means required field<br>
LOWER CASE - offsets forced conversion to uppercase</p>
<p>AS CHECKBOX - checkboxes<br>
RADIOBUTTON GROUP  - radio group, have to define buttons in the group though</p>
<p>Key Events:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">INITIALIZATION</span> <span class="token eol-comment comment">"Executed once</span>
<span class="token keyword">AT</span> <span class="token keyword">SELECTION-SCREEN</span> <span class="token keyword">OUTPUT</span> <span class="token eol-comment comment">"Executed before selection screen is display. Can run multiple times.</span>
<span class="token keyword">AT</span> <span class="token keyword">SELECTION-SCREEN</span> <span class="token eol-comment comment">"Executed immediately after the selection screen is displayed. Can run multiple times.</span>
</code></pre>
<p>These 3 events all run before START-OF-SELECTION</p>
<h2 id="parameter-range">Parameter Range</h2>
<p>Define a range for an input field using:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span> variable_name <span class="token keyword">TYPE</span> <span class="token keyword">I</span><span class="token punctuation">.</span>
<span class="token keyword">SELECT</span> <span class="token keyword">OPTIONS</span><span class="token punctuation">:</span> so_var <span class="token keyword">FOR</span> defined_data_object_name<span class="token punctuation">.</span>
</code></pre>
<p>If the user enters a single value, the conditional operator will be =. If 2 values are entered, the oparatoer will be BETWEEN</p>
<p>Select options uses FOR but it acts like LIKE where it has to be backed by an existing data object variable already declared by the current program.</p>
<p>To define special options for select options variables</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">MOVE</span><span class="token punctuation">:</span> <span class="token string">'AA'</span> <span class="token keyword">to</span> so_var<span class="token token-operator punctuation">-</span>low<span class="token punctuation">.</span> <span class="token eol-comment comment">"lower boundary of range</span>
<span class="token string">'QF'</span> <span class="token keyword">TO</span> so_var<span class="token token-operator punctuation">-</span>high<span class="token punctuation">.</span> <span class="token eol-comment comment">"higher bound of range</span>
<span class="token string">'BT'</span> <span class="token keyword">TO</span> so_var<span class="token token-operator punctuation">-</span>option<span class="token punctuation">.</span> <span class="token eol-comment comment">"operand used for comparison, can also be EQ for between and equals</span>
<span class="token string">'I'</span> <span class="token keyword">to</span> so_var<span class="token token-operator punctuation">-</span>sign <span class="token eol-comment comment">"this is either inclusive or exclusive, meaning the ends of the range are included or not. Can be E for exclusive</span>
</code></pre>
<p>If you want to elimate the option of a value, do something like this:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">MOVE</span><span class="token punctuation">:</span> <span class="token string">'AA'</span> <span class="token keyword">TO</span> so_var<span class="token token-operator punctuation">-</span>low
<span class="token string">'EQ'</span> <span class="token keyword">TO</span> so_var<span class="token token-operator punctuation">-</span>option
<span class="token string">'E'</span> <span class="token keyword">TO</span> so_var<span class="token token-operator punctuation">-</span>sign<span class="token punctuation">.</span>
</code></pre>
<p>Now ‘AA’ won’t be a selection option.</p>
<h2 id="multiple-selection-screens">Multiple Selection Screens</h2>
<p>The standard selection screen is always screen 1000, and all selection screens are numbered in the thousands.</p>
<p>We can define a different selection screen:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">SELECTION-SCREEN</span> <span class="token keyword">BEGIN</span> <span class="token keyword">OF</span> <span class="token keyword">SCREEN</span> <span class="token number">1100</span><span class="token punctuation">.</span>
	<span class="token keyword">PARAMETERS</span><span class="token punctuation">:</span> pa_var <span class="token keyword">AS</span> <span class="token keyword">CHECKBOX</span><span class="token punctuation">.</span>
	<span class="token keyword">SELECT-OPTIONS</span><span class="token punctuation">:</span> so_var <span class="token keyword">FOR</span> <span class="token keyword">I</span><span class="token punctuation">.</span>
<span class="token keyword">SELECTION-SCREEN</span> <span class="token keyword">END</span> <span class="token keyword">OF</span> <span class="token keyword">SCREEN</span> <span class="token number">1100</span><span class="token punctuation">.</span>
</code></pre>
<p>To use this selection screen:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">AT</span> <span class="token keyword">SELECTION-SCREEN</span><span class="token punctuation">.</span>
	<span class="token keyword">CALL</span> <span class="token keyword">SELECTION-SCREEN</span> <span class="token number">1100</span><span class="token punctuation">.</span>
</code></pre>
<p>If any action is perform on the called selection screen, the AT SELECTION-SCREEN event is processed. In this event, sy-dynnr system variable contains the number of the called selection screen.</p>
<p>Call a selection screen as a dialog box:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CALL</span> <span class="token keyword">SELECTION-SCREEN</span> <span class="token number">1100</span>
		<span class="token keyword">STARTING</span> <span class="token keyword">AT</span> &lt;col&gt; &lt;row&gt;  <span class="token eol-comment comment">"starts at this spot</span>
		<span class="token keyword">ENDING</span> <span class="token keyword">AT</span>   &lt;col&gt; &lt;row&gt;<span class="token punctuation">.</span> <span class="token eol-comment comment">"ends at this spot</span>
		<span class="token eol-comment comment">" Top left is 0, 0</span>
</code></pre>
<p>then you can also check sy-subrc… if it &lt;&gt; 0, then you can leave to a different screen or do whatever you want<br>
LEAVE TO SCREEN 1000</p>
<p>Define as selection screen to be used a subscreen in a tab:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">SELECTION-SCREEN</span> <span class="token keyword">BEGIN</span> <span class="token keyword">OF</span> <span class="token keyword">SCREEN</span> <span class="token number">101</span> <span class="token keyword">AS</span> <span class="token keyword">SUBSCREEN</span><span class="token punctuation">.</span>
	<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">SELECTION-SCREEN</span> <span class="token keyword">END</span> <span class="token keyword">OF</span> <span class="token keyword">SCREEN</span> <span class="token number">101</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="input-checks">Input Checks</h2>
<p>can choose to validate pretty much anything specifically and pass an error for specific tabs, blocks or groups</p>
<p>You can check the options on a select options…</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">AT</span> <span class="token keyword">SELECTION-SCREEN</span> <span class="token keyword">ON</span> so_var<span class="token punctuation">.</span>
	<span class="token keyword">If</span> <span class="token punctuation">(</span> so_var<span class="token token-operator punctuation">-</span>low <span class="token keyword">LT</span> <span class="token string">'6000'</span> <span class="token punctuation">)</span><span class="token punctuation">.</span>
		<span class="token keyword">MESSAGE</span> error<span class="token punctuation">(</span>error_number<span class="token punctuation">)</span>
	<span class="token keyword">ENDIF</span><span class="token punctuation">.</span><span class="token punctuation">.</span> 
</code></pre>
<p>Using the ON keyword will only make the target variable available for input again upon error. This is useful if you only want to target one variable for error checking instead of restarting the whole form.</p>
<p>If ON BLOCK block_name is specified, all fields in the block are available for input again after an error<br>
Can also override Dictionary-defined Field help and input help, although this isn’t recommended.</p>
<p>AT SELECTION-SCREEN ON END OF event is trigger after the selection screen has been fully passed to the program.</p>
<h2 id="field-and-input-help">Field and Input Help</h2>
<p>To program our own <strong>field</strong> help:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">AT</span> <span class="token keyword">SELECTION-SCREEN</span> <span class="token keyword">ON</span> <span class="token keyword">HELP-REQUEST</span> <span class="token keyword">FOR</span> field_name<span class="token punctuation">.</span>
</code></pre>
<p>To program our own <strong>input</strong> help:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">AT</span> <span class="token keyword">SELECTION-SCREEN</span> <span class="token keyword">ON</span> <span class="token keyword">VALUE-REQUEST</span> <span class="token keyword">FOR</span> field_name<span class="token punctuation">.</span>
</code></pre>
<p>Field and input help are usually stored in the ABAP dictonary. These events will NOT override what is currently stored in the dictionary for these helps.</p>
<h2 id="variants">Variants</h2>
<p>Pre-defined default values for a form.</p>
<ul>
<li>Uniquely assigned to one program</li>
<li>Useful when you frequenly start a program with the same selection parameter values</li>
<li>Can be created while executing a program at a selection screen using the save button</li>
</ul>
<p>SAP&amp;xxx: SAP variants.<br>
CUS&amp;xxx: Customer variants.</p>
<p>Variants can have many attributes that determine how they behave.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

