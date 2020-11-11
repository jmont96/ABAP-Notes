---


---

<h1 id="program-call-and-memory-mgmt">Program Call and Memory Mgmt</h1>
<p>Objectives:</p>
<ul>
<li>Explain shared objects</li>
<li>Use shared objects</li>
</ul>
<h2 id="shared-memory">Shared Memory</h2>
<p><strong>Fast access to large amounts of data</strong></p>
<p>Examples of the use of shared objects in memory:</p>
<ul>
<li>Fill shopping cart and look at it later</li>
<li>A person writes a blog and lots of people read it</li>
</ul>
<p>Every app server has a shared memory area (SHMA transaction).</p>
<p>We can define different areas and instances of data within those areas.</p>
<p>On an app server, user sessions outside of the area can still access the data from an area.</p>
<h2 id="shared-objects">Shared Objects</h2>
<ul>
<li>Shared objects should be used for cross program buffering of data that is read often and rarely updated</li>
<li>Concurrent read access is supported by shared objects</li>
<li>Access is controlled by a lock mechanism, and only one person can shared update objects at a time</li>
<li>Data is saved as attributes of objects</li>
<li>Memory bottlenecks cause runtime errors and have to be caught to avoid errors</li>
</ul>
<h2 id="creating-an-area">Creating an area</h2>
<p>In the shared memory area (SHMA) we will create an area that can contain classes generated based on the area name. There will be a root that points to an area root class that will point to another node with data.</p>
<p>An area handle provides an address for the area instance</p>
<p>Object generation in shared memory:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span> <span class="token keyword">handle</span> <span class="token keyword">type</span> <span class="token keyword">ref</span> <span class="token keyword">to</span> cl_my_area
<span class="token keyword">DATA</span> go_root typ <span class="token keyword">ref</span> <span class="token keyword">to</span> cl_my_root
<span class="token keyword">DATA</span> go catalog <span class="token keyword">type</span> <span class="token keyword">ref</span> <span class="token keyword">to</span> cl_my_class

go_handle <span class="token operator">=</span> cly_myarea<span class="token token-operator punctuation">=&gt;</span>attach_for_Write<span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span> instatiate the <span class="token keyword">handle</span>

<span class="token keyword">create</span> <span class="token keyword">object</span> go root <span class="token keyword">area</span> <span class="token keyword">handle</span> go_handle<span class="token punctuation">.</span>
<span class="token keyword">create</span> <span class="token keyword">object</span> go_catlog <span class="token keyword">area</span> <span class="token keyword">handle</span> go_handle
go_root<span class="token token-operator punctuation">-&gt;</span>go_cat <span class="token operator">=</span> go_catalog<span class="token punctuation">.</span> <span class="token operator">-</span> link catalog
go_handle<span class="token token-operator punctuation">-&gt;</span>set_root<span class="token punctuation">(</span> go_root <span class="token punctuation">)</span><span class="token punctuation">.</span> <span class="token operator">-</span> <span class="token keyword">assign</span> root <span class="token keyword">object</span> <span class="token keyword">to</span> <span class="token keyword">handle</span>
go_handle<span class="token token-operator punctuation">-&gt;</span>detach_commit<span class="token punctuation">(</span> <span class="token punctuation">)</span><span class="token punctuation">.</span> <span class="token operator">-</span> releases the lock
</code></pre>
<p>REVIEW:</p>
<p>Area points to a root class that points to a data class in the DB table. You make some methods to access it with a class and then we can load into shared memory.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

