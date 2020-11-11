---


---

<h1 id="interfaces">Interfaces</h1>
<p>Objectives:</p>
<ul>
<li>Explain the use of interfaces</li>
<li>Create generalizaton and specialization relationships using interfaces</li>
<li>Implement polymorphism using interfaces</li>
<li>Implement downcasts with interfaces</li>
<li>Integrate different submodels using interfaces</li>
<li>Create and use interface hierarchies</li>
</ul>
<h2 id="why-use-interfaces">Why Use Interfaces</h2>
<p>A client can use an interface, which holds definitions and data that are accessible anywhere in a program. These shared components are useful for modularity and consistent use across classes and programs.</p>
<p>Interface users do NOT share a superclass like inheritance. Think of interface use as a ‘Implements’ relationship where inheritance can be an ‘Extends’ relationship.</p>
<p>Interfaces are mainly meant to hold shared services that can be used by many different objects.</p>
<p>In a diagram, a dashed line in a shows that an interface is used</p>
<p>The interface always only contains definitions for methods</p>
<h2 id="syntax">Syntax</h2>
<p>Definition</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">INTERFACE</span> lif_interface_name<span class="token punctuation">.</span>
<span class="token keyword">Methods</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">ENDINTERFACE</span><span class="token punctuation">.</span>
</code></pre>
<p>To use an interface in a class</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS</span> class_name <span class="token keyword">DEFINITION</span>
	<span class="token keyword">PUBLIC</span> <span class="token keyword">SECTION</span><span class="token punctuation">.</span>
		<span class="token keyword">INTERFACES</span> lif_interface_name<span class="token punctuation">.</span>
<span class="token keyword">ENDCLASS</span><span class="token punctuation">.</span>

<span class="token keyword">CLASS</span> class_name <span class="token keyword">IMPLEMENTATION</span><span class="token punctuation">.</span>
	<span class="token keyword">METHOD</span> lif_interface_name<span class="token token-operator punctuation">~</span>attribute<span class="token punctuation">.</span>
	<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
	<span class="token keyword">ENDMETHOD</span><span class="token punctuation">.</span>
<span class="token keyword">ENDCLASS</span><span class="token punctuation">.</span>
</code></pre>
<p>Can also use aliases for interface components.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">INTERFACES</span> lif_interface_name<span class="token punctuation">.</span>
<span class="token keyword">ALIASES</span> display_data 
<span class="token keyword">FOR</span> lif_interface_name<span class="token token-operator punctuation">~</span>display_information_in_a_list
</code></pre>
<h2 id="generalization--specialization">Generalization &amp; Specialization</h2>
<p>All components in an interface are public. Interfaces cannot control visibility like classes can.</p>
<p>Generalization: Combining common data into a shared resource, like an interface.</p>
<p>Specialization: Data is unique to one required object, so a new module is created for the object. A good example is subclasses.</p>
<h2 id="compound-interfaces">Compound Interfaces</h2>
<p>Interfaces can include other interfaces to create a hierarchial effect.<br>
Basically, you can call another interface from an interface definition and steal all of its methods. Essentially, just another way of doing an include.</p>
<h2 id="when-to-use-interfaces">When To Use Interfaces</h2>
<p>No suitable way to link classes in terms of inheritance or relationship<br>
safe generic method of access<br>
separation of the protocol interface<br>
helps organize and inmprove modularity</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

