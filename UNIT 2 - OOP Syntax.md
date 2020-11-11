---


---

<h1 id="oop-syntax-in-abap">OOP Syntax in ABAP</h1>
<h2 id="class-syntax">Class Syntax</h2>
<p>Attributes are typically private, methods are public.<br>
Protected Attributes are accessible by sub-classes, but not by outside modules.</p>
<p>Defintion:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS</span> class_name DEFINTION<span class="token punctuation">.</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">ENDCLASS</span><span class="token punctuation">.</span>
</code></pre>
<p>Implementation:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS</span> class_name <span class="token keyword">IMPLEMENTATION</span><span class="token punctuation">.</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">ENDCLASS</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="class-defintions">Class Defintions</h2>
<p>In a definition block, you can define:</p>
<ul>
<li>Types</li>
<li>Constants</li>
<li>Methods</li>
<li>Data variables</li>
<li>Static methods</li>
</ul>
<p>Can use READ ONLY on a DATA variable to make it uneditable</p>
<h2 id="visibility">Visibility</h2>
<p>Sections<br>
They must be in this order, but none of them are required.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">PUBLIC</span> <span class="token keyword">SECTION</span><span class="token punctuation">.</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token keyword">data</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>

<span class="token keyword">PROTECTED</span> <span class="token keyword">SECTION</span><span class="token punctuation">.</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token keyword">data</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>

<span class="token keyword">PRIVATE</span> <span class="token keyword">SECTION</span><span class="token punctuation">.</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token keyword">data</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
</code></pre>
<p><strong>Instance attributes</strong><br>
Exist once per instance (so can be more than one in a program)<br>
defined with…</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span>
</code></pre>
<p><strong>Static attributes</strong><br>
exist once per class (so never more than once ever)<br>
defined with…</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS-DATA</span>
</code></pre>
<p>Note: Constants are <strong>always</strong> static attributes</p>
<h2 id="methods-syntax">Methods syntax</h2>
<p>Defintion:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">METHODS</span> method_name [
	<span class="token keyword">IMPORTING</span> iv_var <span class="token keyword">TYPE</span> type_name
	<span class="token keyword">EXPORTING</span> ev_var <span class="token keyword">TYPE</span> type_name
	<span class="token keyword">CHANGING</span> cv_var <span class="token keyword">TYPE</span> type_name
	<span class="token keyword">RETURN</span> <span class="token keyword">VALUE</span><span class="token punctuation">(</span>rv_var<span class="token punctuation">)</span> <span class="token keyword">TYPE</span> type_name
	<span class="token keyword">EXCEPTIONS</span> <span class="token keyword">exception</span> <span class="token operator">=</span> <span class="token number">1</span>
	<span class="token keyword">RAISING</span> exception_class ]
</code></pre>
<p><strong>CANNOT have both RAISING and EXCEPTIONS keyword commands, use only 1 for error handling</strong></p>
<p>Implementation:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">METHOD</span> <span class="token keyword">method</span> <span class="token keyword">name</span><span class="token punctuation">.</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token keyword">data</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">ENDMETHOD</span><span class="token punctuation">.</span>
</code></pre>
<p>Static methods are defined with…</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS-METHODS</span>
</code></pre>
<p>Instance methods are defined with</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">METHODS</span>
</code></pre>
<h2 id="objects">Objects</h2>
<p>Creation:<br>
Define the variable in reference to the class type, then create the object to run the constructor with the required import variables.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span> class_var <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> alread_defined_class<span class="token punctuation">.</span>
<span class="token keyword">CREATE</span> <span class="token keyword">OBJECT</span> class_var <span class="token punctuation">(</span>params<span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>All class variables act as pointers in memory to a certain type of class that gets defined. This is why it is generally required to use TYPE REF TO when typing a class variable.</p>
<p>Anotehr option for defining class variable is:</p>
<pre class=" language-abap"><code class="prism  language-abap">class_var_2 <span class="token operator">=</span> class_var<span class="token punctuation">.</span>
</code></pre>
<p>BUT, this will act as a memory pointer, not a completely new object in memory. With this practice, both variables just point to the same object in memory and essentially equal each other through any manipulation.</p>
<p>By using CREATE OBJECT you will actually duplicate the object with a new assignmnet in memory, not just copying the address, even if you use the same DATA variable.</p>
<h2 id="garbage-collection">Garbage collection</h2>
<p>If there is no reference to an object, it will be deleted by the garbage collector</p>
<h2 id="tables-and-classes">Tables and classes</h2>
<p>If you create an internal table with TYPE TABLE OF REF TO class_already _defined, then you can append class objects into a table after you use create object. So we could add our class_var to a table by using APPEND class_name TO table_name.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span> class_var <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> alread_defined_class
	table_name <span class="token keyword">TYPE</span> <span class="token keyword">TABLE</span> <span class="token keyword">OF</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> already_defined_class<span class="token punctuation">.</span>
	<span class="token keyword">CREATE</span> <span class="token keyword">OBJECT</span> class_var <span class="token punctuation">(</span>params<span class="token punctuation">)</span><span class="token punctuation">.</span>
	<span class="token keyword">APPEND</span> class_var <span class="token keyword">TO</span> table_name<span class="token punctuation">.</span>
</code></pre>
<p>This is how we create lists in ABAP, by using internal tables.<br>
We can then loop through this internal table like an array, treating each index like a class object.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">LOOP</span> <span class="token keyword">AT</span> table_name <span class="token keyword">INTO</span> class_var<span class="token punctuation">.</span>
	<span class="token keyword">WRITE</span><span class="token punctuation">:</span> <span class="token operator">/</span> class_var<span class="token token-operator punctuation">-&gt;</span>get_name<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>
<span class="token keyword">ENDLOOP</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="accessing-methods-and-attributes">Accessing Methods and Attributes</h2>
<p>To access instance methods, we can use:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">create</span> <span class="token keyword">object</span> go_class_name<span class="token punctuation">.</span>
go_class_name<span class="token token-operator punctuation">-&gt;</span>method_name<span class="token punctuation">(</span>IMPORTING
ev_var <span class="token operator">=</span> gv_make ev_var2 <span class="token operator">=</span> gv_model<span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="functional-methods">Functional Methods</h2>
<p>A functional method is a static method that has one RETURNING parameter.</p>
<p>No exporting or changing params allowed prior to ABAP 7.4.</p>
<p>Basically, a functional method is used for getting one piece of data.</p>
<pre class=" language-abap"><code class="prism  language-abap">class_var<span class="token token-operator punctuation">=&gt;</span>get_number_of_instances<span class="token punctuation">(</span> <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Static methods are called with</p>
<pre class=" language-j"><code class="prism  language-j"><span class="token verb keyword">=</span><span class="token verb keyword">&gt;</span>
</code></pre>
<p>Instead of regular class methods, which are called with</p>
<pre class=" language-j"><code class="prism  language-j"><span class="token verb keyword">-</span><span class="token verb keyword">&gt;</span> 
</code></pre>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">object</span>-&gt;method<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>
<span class="token keyword">class</span>=&gt;static_method<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="constructors">Constructors</h2>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">METHOD</span> constructor [
	 <span class="token keyword">IMPORTING</span> iv_var <span class="token keyword">TYPE</span> type_name
	 <span class="token keyword">RAISING</span> exception_class 
	 ]<span class="token punctuation">.</span>
</code></pre>
<p>With a constructor, you can pass export params into CREATE OBJECT as instance variables.</p>
<h2 id="self-reference">Self-reference</h2>
<p>Use me instead of <em>this</em> in ABAP.<br>
Traditionally, <em>this</em> is used to get an objects attributes while working in the class module.</p>
<p>For example, we could be using the objects name attribute in a print method, where the name is display to the user.  To access name, we could use:</p>
<pre class=" language-abap"><code class="prism  language-abap">me<span class="token token-operator punctuation">-&gt;</span>get_name<span class="token punctuation">(</span> <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>This isn’t really neccessary, but is an option if things get messy.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

