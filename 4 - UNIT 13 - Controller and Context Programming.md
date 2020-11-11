---


---

<h1 id="controller-and-context-programming">Controller and Context Programming</h1>
<p>Objectives:</p>
<h2 id="controller-methods">Controller methods</h2>
<p>Controllers include a few standard hook methods provided by SAP. These are great for event processing, as they all run in a certain sequence through the life of a controller. They are intially empty, but you can add whatever you want to them. If you need extra functioanlity, you can also create your own custom methods aside from the SAP standard hooks.</p>
<p>Standard Hook Methods for ALL Controllers</p>
<ul>
<li>WDDOEXIT()
<ul>
<li>Controller cleanup method</li>
<li>Last method processed in controller lifecycle</li>
</ul>
</li>
<li>WDDOINIT()
<ul>
<li>First method processed</li>
<li>Initialization method</li>
</ul>
</li>
</ul>
<p>Standard Hook Methods - Component Controller</p>
<ul>
<li>WDDOAPPLICATIONSTATECHANGE
<ul>
<li>Executed when suspending and resuming the app</li>
<li>Suspension can happen with the firing of a suspend plug, and resumed with a resume plug</li>
</ul>
</li>
<li>WDDOBEFORENAVIGATION
<ul>
<li>Executed before the nav stack is processed</li>
</ul>
</li>
<li>WDDOPOSTPROCESSING
<ul>
<li>Last method processed in phase model before the UI is sent to the client</li>
</ul>
</li>
</ul>
<p>Standard Hook Methods - View Controller</p>
<ul>
<li>WWDDOBEFOREACTION
<ul>
<li>The first method processed after a client event has been triggered</li>
<li>Usually holds code for input checks</li>
</ul>
</li>
<li>WDDOAFTERACTION
<ul>
<li>Processed after action handler method has been processed</li>
</ul>
</li>
<li>WDDOMODIFYVIEW
<ul>
<li>Last view controller method to be processed</li>
<li>Used to manipulate the UI element hierarchy dynamically (only method with access to this)</li>
</ul>
</li>
<li>WDDOONCONTEXTMENU
<ul>
<li>Processed when the user right mouse clicks on UI Element</li>
</ul>
</li>
</ul>
<p>Standard Hook Methods - Window Controllers</p>
<ul>
<li>WDDOONOPEN
<ul>
<li>Processed when the window is sent as a dialog box before the box is opened</li>
</ul>
</li>
<li>WDDOONCLOSE
<ul>
<li>Processed before dialog box close</li>
</ul>
</li>
</ul>
<h2 id="additonal-methods">Additonal methods</h2>
<p>Types:</p>
<ul>
<li>Ordinary methods</li>
<li>Event handler methods</li>
<li>Supply functions</li>
</ul>
<p>Methods defined in the comp controller may be exposed to th compoent interface</p>
<p>Supply functions cannot be called explicity from the course code of the controller methods, only at WD runtime. Don’t have to load a supply function with data.</p>
<p>Supply functions are mainly used to fill context nodes at runtime.</p>
<p>Supply functions are called when:</p>
<ul>
<li>Context nodes are accessed</li>
<li>The context node is initial</li>
<li>The context node has been invalidated in the previous step</li>
</ul>
<p>Supply functions can only access data that is in the corresponding parent node.</p>
<p>Any method created will be public and can be accessible by other controllers (except in a VC, where methods are only available for use in the view).</p>
<h2 id="phase-model">Phase model</h2>
<p>App start: only one view is processed - default is START_VIEW<br>
If you nav to a new view, it will be the RESULT_VIEW which has an action handler method and an inbound plug handler method<br>
finish this</p>
<h2 id="controller-attributes">controller attributes</h2>
<p>Standard</p>
<ul>
<li>WD_context and WD_THIS
<ul>
<li>present in any WD controller (except interface controller)</li>
<li>WD_this
<ul>
<li>Self reference to the local controller interface</li>
<li>Used to access public controller attributes in any controller methods</li>
</ul>
</li>
<li>WD_context
<ul>
<li>Refernce to the context of the associated controller</li>
</ul>
</li>
</ul>
</li>
<li>WD_cOMP_CONTROLLER
<ul>
<li>Reference to the compoent controller object</li>
<li>only present if component controller is defined as used controller</li>
</ul>
</li>
</ul>
<p>CAn also define your own attibutes</p>
<h2 id="accessing-context-at-runtime-with-controller-methods">Accessing Context at Runtime with Controller Methods</h2>
<p>First, you need some data:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span> lc_nd_flights <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> if_wd_context_node<span class="token punctuation">.</span>
<span class="token keyword">DATA</span> lo_el_flights <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> if_wd_context_element<span class="token punctuation">.</span>
<span class="token keyword">DATA</span> ls_flights <span class="token keyword">TYPE</span> wd_this<span class="token token-operator punctuation">-&gt;</span>element_flights<span class="token punctuation">.</span>
<span class="token keyword">DATA</span> lt_flights <span class="token keyword">TYPE</span> wd_this<span class="token token-operator punctuation">-&gt;</span>elements_flights<span class="token punctuation">.</span>
</code></pre>
<p>Navigate from node CONTEXT to node FLIGHTS via lead selection</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_nd_flights <span class="token operator">=</span> wd_context<span class="token token-operator punctuation">-&gt;</span>get_child_node<span class="token punctuation">(</span> <span class="token keyword">name</span> <span class="token operator">=</span> wd_this<span class="token token-operator punctuation">-&gt;</span>wdctx_flights <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Get element at lead selection:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_el_flgihts <span class="token operator">=</span> lo_nd_flights<span class="token token-operator punctuation">-&gt;</span>get_element<span class="token punctuation">(</span> <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>If lead selection is not set, ELEM_FLIGHTS will be initial:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">IF</span> lo_el_flights <span class="token keyword">IS</span> <span class="token keyword">INITIAL</span><span class="token punctuation">.</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">ENDIF</span><span class="token punctuation">.</span>
</code></pre>
<p>Get single attributes from the context:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_el_flights<span class="token token-operator punctuation">-&gt;</span>get_attribute<span class="token punctuation">(</span>
	<span class="token keyword">EXPORTING</span> 
		<span class="token keyword">name</span> <span class="token operator">=</span> <span class="token string">'CONNID'</span>
	<span class="token keyword">IMPORTING</span> <span class="token keyword">value</span> <span class="token operator">=</span> lv_connid <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Get all statically declared attributes:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_el_flights<span class="token token-operator punctuation">-&gt;</span>get_static_attributes <span class="token punctuation">(</span>
	<span class="token keyword">IMPORTING</span> 
	static_atributes <span class="token operator">=</span> ls_flights <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Get all statically declared attributes of all node elements:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_nd_flights<span class="token token-operator punctuation">-&gt;</span>get_static_attributes_table<span class="token punctuation">(</span>
	<span class="token keyword">IMPORTING</span>
		<span class="token keyword">table</span> <span class="token operator">=</span> lt_flights <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Set value of single attribute:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_el_flights<span class="token token-operator punctuation">-&gt;</span>set_attribute<span class="token punctuation">(</span>
	<span class="token keyword">EXPORTING</span>
		<span class="token keyword">name</span> <span class="token operator">=</span> <span class="token string">'CONNID'</span>
		<span class="token keyword">value</span> <span class="token operator">=</span> <span class="token string">'0405'</span> <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Set values of all statically declared attributes:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_el_flights<span class="token token-operator punctuation">-&gt;</span>set_static_attributes <span class="token punctuation">(</span>
	<span class="token keyword">EXPORTING</span>
		static_Atributes <span class="token operator">=</span> ls_flights <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Create new element for node FLIGHTS:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_el_flights <span class="token operator">=</span> lo_nd_flights<span class="token token-operator punctuation">-&gt;</span>create_element<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Set attribute values:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_el_flights<span class="token token-operator punctuation">-&gt;</span>set_attribute<span class="token punctuation">(</span> <span class="token keyword">name</span> <span class="token operator">=</span> <span class="token string">'CARRID'</span> <span class="token keyword">value</span> <span class="token operator">=</span> <span class="token string">'LH'</span> <span class="token punctuation">)</span><span class="token punctuation">.</span>
lo_el_flights<span class="token token-operator punctuation">-&gt;</span>set_attribute<span class="token punctuation">(</span> <span class="token keyword">name</span> <span class="token operator">=</span> <span class="token string">'CONNID'</span> <span class="token keyword">value</span> <span class="token operator">=</span> <span class="token string">'0400'</span><span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Bind element FIRST_ELEMENT to node:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_nd_flight<span class="token token-operator punctuation">-&gt;</span>bind_element<span class="token punctuation">(</span>
new_item <span class="token operator">=</span> lo_el_flights set_initla <span class="token operator">=</span> abap_false <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Set field values of a local structure:</p>
<pre class=" language-abap"><code class="prism  language-abap">ls_flights<span class="token token-operator punctuation">-</span>carrid <span class="token operator">=</span> <span class="token string">'AA'</span><span class="token punctuation">.</span>
ls_flights<span class="token token-operator punctuation">-</span>connid <span class="token operator">=</span> <span class="token string">'0017'</span>
</code></pre>
<p>Bind structure to node:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_nd_flights<span class="token token-operator punctuation">-&gt;</span>bind_structure<span class="token punctuation">(</span>
new_item <span class="token operator">=</span> ls_flights
set_initla_elements <span class="token operator">=</span> abap_false <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Bind internal table to node:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_nd_flights<span class="token token-operator punctuation">-&gt;</span>bind_table<span class="token punctuation">(</span> new_items <span class="token operator">=</span> lt_flights set_intial_elements <span class="token operator">=</span> abap_true <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>Remove element from collection:</p>
<pre class=" language-abap"><code class="prism  language-abap">lo_nd_flights<span class="token token-operator punctuation">-&gt;</span>remove_element<span class="token punctuation">(</span>
element <span class="token operator">=</span> lo_el_flights <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

