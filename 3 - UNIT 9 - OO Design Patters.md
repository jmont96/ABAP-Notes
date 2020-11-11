---


---

<h1 id="design-patterns">Design Patterns</h1>
<p>Objectives:</p>
<ul>
<li>Understand how to define abstract methods, abstract classes, final classes and final methods</li>
<li>Understand how to use read-only and optional attributes</li>
<li>Understnad how to chain functional method calls</li>
<li>Understand how to define visibility of an instance constructor</li>
</ul>
<h2 id="abstract-classes">Abstract Classes</h2>
<ul>
<li>Cannot be instantiated</li>
<li>Contains both implementation and definition blocks</li>
<li>Super-classes are a common use for abstract calsses, since their sub classes can be instantiated</li>
</ul>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS</span> lcl_ <span class="token keyword">DEFINITION</span> <span class="token keyword">ABSTRACT</span><span class="token punctuation">.</span>
<span class="token keyword">ENDCLASS</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="abstract-methods">Abstract Methods</h2>
<p>Abstract methods have a similar concept. They can’t be implemented in the host class, but can be in a sub-class.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">Methods</span><span class="token punctuation">:</span> do_something <span class="token keyword">ABSTRACT</span><span class="token punctuation">.</span> 
</code></pre>
<h2 id="final-classes-and-methods">Final Classes and Methods</h2>
<p>Final classes cannot have subclasses.<br>
Final methods cannot be redefined.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS</span> lcl_ <span class="token keyword">DEFINITION</span> <span class="token keyword">FINAL</span><span class="token punctuation">.</span>
	<span class="token keyword">METHODS</span><span class="token punctuation">:</span> do_something <span class="token keyword">FINAL</span><span class="token punctuation">.</span>
<span class="token keyword">ENDCLASS</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="method-chaining">Method Chaining</h2>
<p>We can chain method calls together to use less code.</p>
<pre class=" language-abap"><code class="prism  language-abap">dog <span class="token operator">=</span> pet_store<span class="token token-operator punctuation">-&gt;</span>get_dog<span class="token punctuation">(</span><span class="token punctuation">)</span>-&gt;get_attributes<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="new">NEW</h2>
<p>Another way to create objects at runtime.</p>
<p>Use # to implicitly type the new object. This will automatically type the new object according to the existing object’s type.</p>
<pre class=" language-abap"><code class="prism  language-abap">go_dog <span class="token operator">=</span> <span class="token keyword">NEW</span> #<span class="token punctuation">(</span>
iv_name <span class="token operator">=</span> <span class="token string">'Doug'</span>
iv_color <span class="token operator">=</span> <span class="token string">'brown'</span>
<span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Use NEW to easily append a new object:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">APPEND</span> <span class="token keyword">NEW</span> #<span class="token punctuation">(</span>
iv_name <span class="token operator">=</span> <span class="token string">'Doug'</span>
iv_color <span class="token operator">=</span> <span class="token string">'brown'</span>
<span class="token punctuation">)</span> <span class="token keyword">TO</span> it_dogs<span class="token punctuation">.</span>
</code></pre>
<p>We can also specify a type for safety.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">APPEND</span> <span class="token keyword">NEW</span> Dog <span class="token punctuation">(</span>
iv_name <span class="token operator">=</span> <span class="token string">'Doug'</span>
iv_color <span class="token operator">=</span> <span class="token string">'brown'</span>
<span class="token punctuation">)</span> <span class="token keyword">TO</span> it_dogs<span class="token punctuation">.</span>
</code></pre>
<h2 id="type-checks-in-case">Type Checks In Case</h2>
<p>Another way to easily check object types is to use a case statement:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CASE</span> <span class="token keyword">TYPE</span> <span class="token keyword">OF</span> animal<span class="token punctuation">.</span>
	<span class="token keyword">WHEN</span> <span class="token keyword">TYPE</span> dog<span class="token punctuation">.</span>
		<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
	<span class="token keyword">WHEN</span> <span class="token keyword">TYPE</span> cat <span class="token keyword">INTO</span> go_cat<span class="token punctuation">.</span> *not required
		go_cat<span class="token token-operator punctuation">-&gt;</span>make_sound<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>
	<span class="token keyword">WHEN</span> <span class="token keyword">OTHERS</span><span class="token punctuation">.</span>
		<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">ENDCASE</span><span class="token punctuation">.</span>
</code></pre>
<p>Class Creation Visibility<br>
We can control the instance constructor’s visbility by following the Class Defintion with CREATE and your chosen visibility.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS</span> lcl_ <span class="token keyword">DEFINITION</span> <span class="token keyword">CREATE</span> <span class="token keyword">PUBLIC</span>
<span class="token keyword">ENDCLASS</span><span class="token punctuation">.</span>
</code></pre>
<p>This comes in all normal visibility options:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CREATE</span> <span class="token keyword">PUBLIC</span><span class="token punctuation">.</span>
</code></pre>
<p>This class can be instantiated from anywhere (default).</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CREATE</span> <span class="token keyword">PROTECTED</span><span class="token punctuation">.</span>
</code></pre>
<p>Only the class itself or the subclasses can instantiate this class.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CREATE</span> <span class="token keyword">PRIVATE</span><span class="token punctuation">.</span>
</code></pre>
<p>Only the class itself can instantiate this class. This is what factory methods use.</p>
<h2 id="factory-classes-and-methods">Factory Classes and Methods</h2>
<p>A factory method in a class:</p>
<ul>
<li>A static method that is public</li>
<li>When called, the method will perform an instantiation and give you back a newly created object</li>
</ul>
<p>A factory class:</p>
<ul>
<li>Possesses a friendship with another class for which it will instaniate objects.
<ul>
<li>Example: lcl_animal and lcl_animal_factory</li>
</ul>
</li>
<li>Handles all instantiation for the target class</li>
<li>Can contain a table to administrate data in order to keep track of what has been created</li>
</ul>
<p>Advantages of the factory design pattern:</p>
<ul>
<li>Can perform consistent actions before or after instantiation</li>
<li>Less code, more reuse</li>
<li>Administrate or count the amount of instances being built in your program
<ul>
<li>Can check to see if an object with same attribtues already exists in the program.</li>
</ul>
</li>
<li>Can create different subclasses based on parameters being passed in
<ul>
<li>Example: if you pass in a number of seats, create a passenger plane, if you pass in cargo amount, create a cargo plane.
<ul>
<li>This requires some parameters in a factory method to be optional</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2 id="singleton-pattern">Singleton pattern</h2>
<p>The singleton pattern is similar to a factory pattern, where you control the instantiation of an object through a static process, but a singleton method will never create more than one object. If something of the type has already been instantiated, it will do nothing.</p>
<p>Singleton uses IS BOUND to determine if the object has been created</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">IF</span> variable <span class="token keyword">IS</span> <span class="token keyword">BOUND</span><span class="token punctuation">.</span>
	<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>do_nothing<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">ENDIF</span><span class="token punctuation">.</span>
</code></pre>
<p>IS BOUND is similar to IS NOT INITIAL</p>
<p>Singleton uses a static constuctor (class_constructor), or a static variable and a static method (preffered). The static variable represents the single object that will exist, while the static method handles the logic of returning and building the instance.</p>
<p>A Static Contstructor cannot have any input params, so a singleton object is determined statically without control by the user at runtime.</p>
<p>A class_constructor is only executed once in the life of the program (first call to object).</p>
<h2 id="friendship">Friendship</h2>
<p>If we have two classes and want to share data, we can…</p>
<ol>
<li>Have subclasses that share protected data through inheritance</li>
<li>Create a friendship where we can share data that is private to the outside world</li>
</ol>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS</span> class_name <span class="token keyword">DEFINITION</span> <span class="token keyword">CREATE</span> <span class="token keyword">PRIVATE</span> <span class="token keyword">FRIENDS</span> class_name_2
</code></pre>
<p>Class 2 can now access ALL of Class 1s data, no matter what the visibility settings are.</p>
<p>Class 2 can also instatiate a class_1, object even though it is a CREATE PRIVATE object. This is where factory classes can be used.</p>
<p>The DEFFFERED keyword can be used on a defintion of a class at the top of the program so that the program knows about it. Kinda like how you have to define functions at the top with one line in C.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS</span> lcl_ <span class="token keyword">DEFINITION</span> <span class="token keyword">DEFERRED</span><span class="token punctuation">.</span> 
</code></pre>
<p>TYPE REF TO STORES THE ADDRESS OF THE REFERENCED TYPE</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

