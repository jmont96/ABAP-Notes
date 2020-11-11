---


---

<h2 id="object-oriented-programming">Object Oriented Programming</h2>
<p>Function groups in a procedural language are fine, but they don’t allow you to easily have multiple related objects by using programs. This is why OOP exists, we can design objects and then have as many of them as we want very easily.</p>
<p>Can instantiate multiple class objects into memory and use them in a program somewhere.</p>
<p>Procedural: separatetion of data and functons</p>
<p>OOP: encapsulation of data and functions</p>
<h2 id="classes">Classes</h2>
<p>Definition:</p>
<pre class=" language-abap"><code class="prism  language-abap"> <span class="token keyword">CLASS</span> class_name DEFINTION<span class="token punctuation">.</span>
 <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token keyword">data</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
 <span class="token keyword">ENDCLASS</span><span class="token punctuation">.</span>
</code></pre>
<p>Implementation</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS</span> class_name <span class="token keyword">IMPLEMENTATION</span><span class="token punctuation">.</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token keyword">data</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">ENDCLASS</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="objects">Objects</h2>
<p>Objects are a direct abstrction of the real world. They are modules made up of data and methods. The data acts as attributes of a real-world object, like a name, while methods work like actions, providing the object with functionality, like speak.</p>
<p>Example:</p>
<p>Dog:<br>
Data: name, color, weight, height, breed.<br>
Methods: run, walk, bark, jump.</p>
<h2 id="advantages">Advantages</h2>
<p>In OOP, processes can be designed and implemented in a much better way than in procedural langauges. We can share components instead of reusing similar code, and create relations that would be impossible without features included in OOP.</p>
<p>Advantages of using OOP:</p>
<ul>
<li>Improved software structure and consistency</li>
<li>Reduced maintenance</li>
<li>Easier to understand, since it relates to the real world. This leads to better involvement of the customer or user into analysis and design processes.</li>
<li>Simpler and more secure extension of the software</li>
</ul>
<h2 id="design-process">Design Process</h2>
<p>Class Diagrams include three sections separated by horizontal lines.</p>
<ul>
<li>Class name (capitalize first letter ALWAYS)</li>
<li>Attributes with data type (name:string)</li>
<li>Methods with a return type (get_name():string)
<ul>
<li>Use :void for methods that don’t return anything</li>
</ul>
</li>
</ul>
<p>Relationships</p>
<ul>
<li>Diamond (open): Aggragation
<ul>
<li>Special relationship of a whole part
<ul>
<li>Example: A car
<ul>
<li>A vehicle contains wheels, so wheel points an open diamond at the vehicle class</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>Diamond (solid): Composition
<ul>
<li>One object cannot exist on its own
<ul>
<li>Example: Airbnb Rental
<ul>
<li>The rental booking can’t exist without the rental home, so the rental booking class points a filled diamond at the rental home class</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>Arrows: Inheritance</li>
<li>Multiplicity:
<ul>
<li>0…star means 0 to many.</li>
<li>1 means 1.</li>
<li>1…star means 1 to many.</li>
<li>0…1 means 0 or 1.</li>
</ul>
</li>
<li>Lines:
<ul>
<li>An association of some type. Can be recursive, meaning it points back at itself.</li>
<li>Recursive example: the Person class
<ul>
<li>2 parents can have 1 to many children, both are people. You’d probably split this up into 2 subclasses, though.</li>
</ul>
</li>
</ul>
</li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

