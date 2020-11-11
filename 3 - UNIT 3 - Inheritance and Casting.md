---


---

<h1 id="inheritance">Inheritance</h1>
<p>Two objects need to have an ‘is a’ relationship<br>
Example: a dog ‘is a’ animal</p>
<p>Dog = subclass of Animal</p>
<p>Subclasses are dependent on super-classes</p>
<p>Defining a subclass:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS</span> dog_class <span class="token keyword">DEFINITION</span> <span class="token keyword">INHERITING</span> <span class="token keyword">FROM</span> animal_class<span class="token punctuation">.</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">ENDCLASS</span><span class="token punctuation">.</span>
</code></pre>
<p>A subclass can then have some extra functions and data attributes to extend the super class</p>
<p>Redefining methods (override)</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">METHODS</span> method_name REDEFITION<span class="token punctuation">.</span>
</code></pre>
<p>You cannot change the parameters that get passed into an override, just redo the functionality.</p>
<p>You cannot redefine static methods.</p>
<p>Call anything that is a public method in the super.</p>
<pre class=" language-abap"><code class="prism  language-abap">super<span class="token token-operator punctuation">-&gt;</span>public_method<span class="token punctuation">(</span> <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>One can also redefine the constructor if you want. This could be used to add extra attributes or something. In the implementation, you always have to call super-&gt;constructor as a first line in your subclass constructor.</p>
<p>Protected visibility allows usage in subclasses like public, but still acts as private outside of the class objects</p>
<h2 id="upcasting">Upcasting</h2>
<p>The type of a reference class variable is defined using TYPE REF TO.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span><span class="token punctuation">:</span> var <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> class_name<span class="token punctuation">.</span>
</code></pre>
<p>At runtime, this could potentially change if something is casted differently.<br>
basically upcasting is casting superclasses as a subclass.</p>
<pre class=" language-abap"><code class="prism  language-abap">animal <span class="token operator">=</span> dog<span class="token punctuation">.</span>
</code></pre>
<p>Upcasting is useful for storing inherited objects in a an internal table together instead of listing them all separetely. To check the type of object, we can use downcasting.</p>
<h2 id="downcasting">Downcasting</h2>
<p>Casting a subclass as a superclass to check instance type.</p>
<pre class=" language-abap"><code class="prism  language-abap">dog <span class="token operator">=</span> animal<span class="token punctuation">.</span>
</code></pre>
<p>Downcasting is mostly useful for type checking in polymorphic objects.</p>
<p>Furthermore, we are able to easily check is an object in a loop is of a certain subclass type.</p>
<p>This is an easier alternative to adding get_type() as a method to each class.</p>
<p>We can achieve this in a couple ways. First, we can use a temp variable of our target type (cargo plane in this case) and then attempt a downcast in a try/catch block. If the cast works, we know the object is an instance of our specific subclass.</p>
<p>We use ?= to attempt a downcast.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span><span class="token punctuation">:</span> temp_cargo <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> lcl_cargo_plane<span class="token punctuation">.</span>

<span class="token keyword">LOOP</span> <span class="token keyword">AT</span> gt_airplanes_table <span class="token keyword">INTO</span> go_airplane<span class="token punctuation">.</span>
	<span class="token keyword">TRY</span><span class="token punctuation">.</span>  
		temp_cargo <span class="token operator">?=</span> go_airplane<span class="token punctuation">.</span>  
		<span class="token keyword">WRITE</span><span class="token punctuation">:</span> <span class="token operator">/</span> <span class="token string">'This is a cargo plane'</span><span class="token punctuation">.</span> 
		<span class="token keyword">WRITE</span><span class="token punctuation">:</span> <span class="token operator">/</span> <span class="token string">'Index:'</span><span class="token punctuation">,</span> sy<span class="token token-operator punctuation">-</span>tabix<span class="token punctuation">.</span> 
	<span class="token keyword">CATCH</span> cx_sy_move_cast_error<span class="token punctuation">.</span>  
		<span class="token keyword">WRITE</span><span class="token punctuation">:</span> <span class="token operator">/</span> <span class="token string">'Not a cargo plane'</span><span class="token punctuation">.</span>
	<span class="token keyword">ENDTRY</span><span class="token punctuation">.</span>
<span class="token keyword">ENDLOOP</span>
</code></pre>
<p>We can also use <strong>is instance of</strong> for type checking in polymorphic objects. (This is way better and easier than trying to downcast)</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">IF</span> go_airplane <span class="token keyword">IS</span> INSTANCE <span class="token keyword">OF</span> lcl_cargo_plane<span class="token punctuation">.</span>  
	<span class="token keyword">WRITE</span><span class="token punctuation">:</span> <span class="token operator">/</span> <span class="token string">'CARGOOOOOOO'</span><span class="token punctuation">.</span>  
<span class="token keyword">ENDIF</span><span class="token punctuation">.</span>
</code></pre>
<p>Advantages of class hierarchies and inheritance</p>
<ul>
<li>Easier to maintain</li>
<li>More modular and organized</li>
</ul>
<p>Disadvantages</p>
<ul>
<li>Can be modeled poorly and create extra confusion</li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

