---


---

<h1 id="new-badis">New BADIs</h1>
<h2 id="overview">Overview</h2>
<p>Why SAP introduced new BADi tech?</p>
<ul>
<li>Improve performance</li>
<li>Implement additional functions
<ul>
<li>Enhanced filter concept</li>
<li>Option to inherit attributes</li>
</ul>
</li>
<li>Integrates into the new enhancement framework by using enhancement points and enhancement sections</li>
</ul>
<p>Enhancement Framework includes Implicit enhancement points, explicit enhancement points and new BADIs.</p>
<p>New BADIs and explicit enhancement points are managed by enhancement spots.</p>
<p>Each enhancement spot might have multiple enhancement points or BADIs.</p>
<p>Enhancement spots can be nested, meaning there could be enhancement spots in an enhancement spot.</p>
<p>To use a BADI, you MUST create an enhacement implementation of the enhancement spot AND a BADI implementation for each BADI you want to use in the enhancement spot.</p>
<p>New BADI Syntax</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span> r_rexit <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> badi_name<span class="token punctuation">.</span>

<span class="token keyword">TRY</span><span class="token punctuation">.</span> 
	<span class="token keyword">GET</span> <span class="token keyword">BADI</span> r_exit<span class="token punctuation">.</span> <span class="token eol-comment comment">"generate handle</span>
	<span class="token keyword">CATCH</span> cx_badi_not_implemented<span class="token punctuation">.</span>
<span class="token keyword">ENDTRY</span><span class="token punctuation">.</span>

<span class="token keyword">TRY</span><span class="token punctuation">.</span>
	<span class="token keyword">CALL</span> <span class="token keyword">BADI</span> r_exit<span class="token token-operator punctuation">-&gt;</span>abc <span class="token eol-comment comment">"call method using the handle</span>
	<span class="token keyword">CATCH</span> cx_badi_initial_reference<span class="token punctuation">.</span>
<span class="token keyword">ENTRY</span><span class="token punctuation">.</span> 
</code></pre>
<h2 id="new-badi-program-exits">New BADI Program Exits</h2>
<ul>
<li>GET BADI gets the BADI handle which comes from the kernel… <strong>adapter classes aren’t neccessary</strong> anymore, but it performs the same function.</li>
<li>A bridging method is called using the BADi handle and the bridging method is determined based on the user’s CALL BADI statement</li>
</ul>
<p>To search for new BADI program exits, perform a global search in the program you want to enhancefor the keywords ‘GET BADI’ or ‘CALL BADI’</p>
<p>To implement a New BADI program exit:</p>
<ol>
<li>Display an enhancement spot</li>
<li>Implement the enhancement spot by choosing ‘implement enhancement spot’</li>
<li>Specify a name for the enhancement implementation, the BADI implementation AND the implementing class</li>
<li>Double click the class the adjust the methods to your liking</li>
<li>Activate the method and related objects</li>
</ol>
<p>There are two types of BADI implementations</p>
<ul>
<li>A BADI definition cna be linked to a fallback class</li>
<li>A BADI implementation can be defined as the default implementation</li>
</ul>
<p>Behavior at runtime:</p>
<ul>
<li>All non-default implementations are executed</li>
<li>The default is called if NO other implementation exists</li>
<li>The fallback class is the last option if nothing else has been executed</li>
</ul>
<h2 id="filter-dependent-badis">Filter Dependent BADIs</h2>
<p>Some classic BADIs were filter-dependent, but the functionality has been enhanced in new BADIs.</p>
<p>A filter allows you to create implementations based on certain values that satisfy your filter conditions.</p>
<p>In new BADIs we can now:</p>
<ul>
<li>Use numeric filters</li>
<li>Create implementations using operators in filter conditions</li>
<li>Have multiple filters for one implementation</li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

