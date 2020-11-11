---


---

<h1 id="dynamic-programming">Dynamic Programming</h1>
<p>Objectives:</p>
<ul>
<li>Explain and use generic data types</li>
<li>Access data objects dynamically</li>
<li>Use generically typed data references</li>
<li>Explain RTTI (Runtime Type Indentification)</li>
<li>Describe data types and data objects at runtime</li>
<li>Describe object types and types at runtime</li>
<li>Create objects, data variables, and types at runtime</li>
</ul>
<h2 id="generic-data-types">Generic Data Types</h2>
<p>Built-in generic data types:</p>
<ul>
<li>Any - Any type</li>
<li>Data - Any data type</li>
<li>Simple - elementary type or flat structure. Can be printed without issue.</li>
<li>Numeric - i, f, p, int8, or any decfloat##</li>
<li>Decfloat - any decfloat##</li>
<li>Clike - character data type - c, n, d, t, string</li>
<li>Csequence - Text data type - c, string</li>
<li>Xsequence - hex byte sequence - x, xstring</li>
</ul>
<p>Potential problems with generic typing:</p>
<ul>
<li>Will never get syntax errors but some stuff might not work at runtime</li>
<li>Could end up getting type errors</li>
</ul>
<p>Bottom Line: Way safer to type everything, but sometimes generic typing is useful.</p>
<p>Generically typing tables:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">TYPE</span> <span class="token keyword">SORTED</span> <span class="token keyword">TABLE</span> <span class="token keyword">OF</span> table_name<span class="token punctuation">.</span>
<span class="token keyword">TYPE</span> <span class="token keyword">INDEX</span> <span class="token keyword">TABLE</span> <span class="token keyword">OF</span> table_name<span class="token punctuation">.</span>
<span class="token keyword">TYPE</span> <span class="token keyword">ANY</span> <span class="token keyword">TABLE</span> <span class="token keyword">OF</span> table_name<span class="token punctuation">.</span>
<span class="token keyword">TYPE</span> <span class="token keyword">ANY</span> <span class="token keyword">TABLE</span><span class="token punctuation">.</span>
</code></pre>
<p>We are only allowed to loop through generic data objects if they are specified to be a table.</p>
<p>For reference variables (type ref to), we can generically type by using:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span> variable <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> <span class="token keyword">DATA</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="field-symbols">Field Symbols</h2>
<p>Field symbols are pointers that can be assigned to data objects dynamically.</p>
<ul>
<li>We can dynamically define specific data object that the field symbol refers to</li>
<li>If a field symbol is typed, then all potential data objects must have the same type</li>
<li>Field symbols can be generically typed</li>
</ul>
<p>Define with</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">FIELD-SYMBOLS</span><span class="token punctuation">:</span> &lt;fs_symbol_name&gt; <span class="token keyword">TYPE</span> <span class="token keyword">ANY</span><span class="token punctuation">.</span> 
</code></pre>
<p>Assigning field symbols:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span><span class="token punctuation">:</span> internal_table <span class="token keyword">TYPE</span> <span class="token keyword">TABLE</span> <span class="token keyword">OF</span> target_table<span class="token punctuation">.</span>
<span class="token keyword">FIELD-SYMBOLS</span><span class="token punctuation">:</span> &lt;fs_table&gt; <span class="token keyword">TYPE</span> <span class="token keyword">ANY</span> <span class="token keyword">TABLE</span><span class="token punctuation">.</span>

<span class="token keyword">ASSIGN</span> internal_table <span class="token keyword">TO</span> &lt;fs_table&gt;<span class="token punctuation">.</span>

<span class="token keyword">IF</span> &lt;fs_table&gt; <span class="token keyword">IS</span> <span class="token keyword">ASSIGNED</span><span class="token punctuation">.</span>
<span class="token keyword">LOOP</span> <span class="token keyword">AT</span> &lt;fs_table&gt;<span class="token punctuation">.</span>
<span class="token keyword">ENDLOOP</span><span class="token punctuation">.</span> 
</code></pre>
<h2 id="generic-data-access--representation">Generic Data Access &amp; Representation</h2>
<p>We can use some tricks with generic access using () to access data in different ways.</p>
<pre class=" language-abap"><code class="prism  language-abap">gv_var <span class="token operator">=</span> <span class="token string">'TABLE_NAME'</span><span class="token punctuation">.</span>
<span class="token keyword">ASSIGN</span> <span class="token punctuation">(</span>gv_var<span class="token punctuation">)</span> <span class="token keyword">TO</span> &lt;fs&gt;<span class="token punctuation">.</span>

gv_var <span class="token operator">=</span> <span class="token string">'LCL_ANIMAL-&gt;BARK'</span><span class="token punctuation">.</span>
ASSING <span class="token punctuation">(</span>gv_var<span class="token punctuation">)</span> <span class="token keyword">TO</span> &lt;fs&gt;<span class="token punctuation">.</span>

gv_var <span class="token operator">=</span> <span class="token string">'COLOR'</span><span class="token punctuation">.</span>
<span class="token keyword">ASSIGN</span> lcl_animal-&gt;<span class="token punctuation">(</span>gv_var<span class="token punctuation">)</span> <span class="token keyword">TO</span> &lt;fs&gt;

gv_var <span class="token operator">=</span> <span class="token string">'LCL_DOG'</span><span class="token punctuation">.</span>
<span class="token keyword">CREATE</span> <span class="token keyword">OBJECT</span> dog_var <span class="token keyword">TYPE</span> <span class="token punctuation">(</span>gv_var<span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>This is easy for structure components too:</p>
<pre class=" language-abap"><code class="prism  language-abap">gv_var <span class="token operator">=</span> <span class="token string">'STRUCT_ID'</span><span class="token punctuation">.</span>
<span class="token keyword">ASSIGN</span> <span class="token keyword">COMPONENT</span> gv_var <span class="token keyword">OF</span> <span class="token keyword">STRUCTURE</span> structure_name <span class="token keyword">TO</span> &lt;fs&gt;<span class="token punctuation">.</span>
</code></pre>
<p>With this strategy, we can easily print a structure by loading each component into a field symbol by using do loops and sy-index.</p>
<p>To loop internal tables, we can load each line into a field symbol instead of a strcture or other data type. To do this, we use a different keyword:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">LOOP</span> <span class="token keyword">AT</span> it_table <span class="token keyword">ASSIGNING</span> &lt;fs&gt;
</code></pre>
<h2 id="describing-data-at-runtime">Describing Data at Runtime</h2>
<p>RTTI - Runtime Type Identification</p>
<p>RTTI is a set of global classes set in a hierarchical form. At the top is CL_ABAP_TYPEDESCR, which is extended by many classes to specialize in describing certain types of objects. CL_ABAP_TYPEDESCR is abstract and cannot be instantiated.</p>
<p>Only 6 RTTI classes are not abstract. These are all for specific types, named CL_ABAP_###DESCR, where ### is the type. For example, STRUCTDESCR.</p>
<p>CL_ABAP_TYPEDESCR can be used statically to get desriptions of different data objects.</p>
<pre class=" language-abap"><code class="prism  language-abap">CL_ABAP_TYPEDESCR<span class="token token-operator punctuation">=&gt;</span>describe_by_name<span class="token punctuation">(</span> table_name <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>RTTC Runtime Tyep Creation… we can use RTTC methods to create objects on the fly.</p>
<p>FOLLOW UP TESTS:<br>
Looping a struct with field symbols<br>
upcasting (what do i have access to?)<br>
READ TABLE command<br>
Internal Table work</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

