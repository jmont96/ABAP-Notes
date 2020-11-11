---


---

<h1 id="data-types-in-the-dictionary">Data Types in the Dictionary</h1>
<p>Objectives:</p>
<ul>
<li>Create domains for data elements</li>
<li>Create data elements</li>
<li>Create simple and nested structures in the ABAP Dictionary</li>
<li>Create table types in the ABAP Dictionary</li>
<li>Create Deep Strctures</li>
<li>Define Type Groups</li>
</ul>
<p>To access Dictionary</p>
<ul>
<li>Use SE80</li>
<li>Use SE11</li>
</ul>
<h2 id="data-types--domains">Data Types &amp; Domains</h2>
<p>All data types created in the dictionary are global.</p>
<p>These will all become data types eventually that are usable in your programs.</p>
<p>Domains</p>
<ul>
<li>Technical info that backs a data element
<ul>
<li>Length</li>
<li>Type</li>
<li>Decimals</li>
</ul>
</li>
<li>Domains cannot be used directly in programs or tables</li>
<li>Makes up the technical setting’s format and output characteristics</li>
</ul>
<p>Data Elements</p>
<ul>
<li>Defines data types that can be used in screens, search help, ABAP programs and complex data types</li>
<li>Specify technical properties using domains</li>
<li>Semantic info includes documentation, labels, input history, etc.</li>
</ul>
<h2 id="local-objects">Local Objects</h2>
<p>Packaging vs local object</p>
<ul>
<li>Package is used to organize different programs and modules</li>
<li>Local objects are stored locally on your system
<ul>
<li>Cannot be used in transport requests</li>
<li>Can’t be moved to a production system</li>
<li>STMP means local object - package is $TMP TAW10-04
<ul>
<li>Can be moved thorugh a package change to remove status of being a local object</li>
<li>Can also be copied into a package</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2 id="creating-flat-structures">Creating Flat Structures</h2>
<p>We can include different attributes into a structure component by using nests.</p>
<p>When we have a nested struct, you can access the components attributes (sub-components) by using dashes</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">WRITE</span><span class="token punctuation">:</span> person_struct<span class="token token-operator punctuation">-</span>name<span class="token token-operator punctuation">-</span>first<span class="token punctuation">.</span>
<span class="token keyword">WRITE</span><span class="token punctuation">:</span> person_struct<span class="token token-operator punctuation">-</span>address<span class="token token-operator punctuation">-</span>city<span class="token punctuation">.</span>
<span class="token keyword">WRITE</span><span class="token punctuation">:</span> person_struct<span class="token token-operator punctuation">-</span>features<span class="token token-operator punctuation">-</span>eyes<span class="token token-operator punctuation">-</span>brown <span class="token punctuation">.</span>
</code></pre>
<p>These are just some examples, nesting can be done by using a struct as a component, or by using .include and then typing it with a struct.</p>
<p>Let’s sat we use .include… now we can skip the title of the component struct!</p>
<pre class=" language-abap"><code class="prism  language-abap"> <span class="token keyword">WRITE</span><span class="token punctuation">:</span> person_struct<span class="token token-operator punctuation">-</span>first
 <span class="token keyword">WRITE</span><span class="token punctuation">:</span> person_struct<span class="token token-operator punctuation">-</span>city
</code></pre>
<p>FOLLOW UP<br>
What would happen if I nested three sturctures with .include?</p>
<h2 id="table-types">Table Types</h2>
<p>Internal Tables are defined by table types.</p>
<p>Definition:</p>
<ul>
<li>A line type that represents a row of the internal table</li>
<li>Access mode - Standard, sorted, hashed or index table</li>
<li>Primary key defintion and key category
<ul>
<li>Hashed table always has unique key</li>
<li>Sorted table can be unique or not</li>
</ul>
</li>
<li>Secondary key (optional)</li>
</ul>
<p>Special Table Types</p>
<ul>
<li>Generic table types
<ul>
<li>Define only some attributes of an internal table
<ul>
<li>Differentiating attributes - what makes something a generic table?
<ul>
<li>The key is not specified</li>
<li>Access mode is ‘index’ or not specified</li>
<li>The key category is not specified</li>
<li>Secondary keys are not permitted</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>Range Tables
<ul>
<li>Used for complex areas in an internal table</li>
<li>Row type consists of Low, High, Option (operator) and Sign</li>
</ul>
</li>
</ul>
<p>How to build a table type</p>
<ol>
<li>Use data type in SE11</li>
<li>Enter table name and hit create</li>
<li>Select ‘table type’ radio button nad continue</li>
<li>Give a line type</li>
<li>Select initialization and access info in tab</li>
<li>Select a promary key</li>
</ol>
<h2 id="deep-structures">DEEP STRUCTURES</h2>
<p>Has a complex component in one of the field components<br>
like a table or something.</p>
<p>To define with complex component attribute, you need to go to extras -&gt; enhancements to make it enhancable.</p>
<h2 id="type-group">Type group</h2>
<p>Type pools like icons… don’t really use these lol.</p>
<ul>
<li>Use se11 to create a type group</li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

