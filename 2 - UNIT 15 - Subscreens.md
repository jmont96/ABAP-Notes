---


---

<h1 id="subscreens">Subscreens</h1>
<p>A screen tool used for modularization and reuse of screen components.</p>
<h2 id="overview">Overview</h2>
<p>Choose a small area on the main screen in the screen painter and make it a subscreen area.</p>
<p>Now, this subscreen can be changed dynamically.</p>
<p>All subscreens are contained in a subscreen area filled at runtime</p>
<p>Subscreen attributes:</p>
<ul>
<li>Scrollable, minimum size, resizeable</li>
<li>Size, switch, start position, name</li>
</ul>
<p>Can’t have titlebars or function keys</p>
<p>Create a subscreen area in the screen painter with the layout editor.</p>
<p>Calling a subscreen dynamically in PBO:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CALL</span> <span class="token keyword">SUBSCREEN</span> &lt;sub_area&gt;
	<span class="token keyword">INCLUDING</span> &lt;program_name&gt; &lt;screen_number&gt;
</code></pre>
<p>You cnan also do this from PAI, but not with including:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CALL</span> <span class="token keyword">SUBSCREEN</span> &lt;subarea&gt;
</code></pre>
<p>Visibility fo Data<br>
create a vraiable for the screen…</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span> dynnr <span class="token keyword">TYPE</span> sy<span class="token token-operator punctuation">-</span>dnnr <span class="token keyword">VALUE</span> <span class="token string">'0110'</span><span class="token punctuation">.</span>
</code></pre>
<p>Can also get subscreens from external programs.</p>
<p>Typically, one uses a function for this that saves data in the subscreen to be used among many screens</p>
<p>The main program could export data to a function call in a PBO module. Then display a screen, then call a subscreen. Then in PAI, call the same subscreen then call another function to import data in a module.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

