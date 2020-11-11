---


---

<h1 id="explicit-enhancements">Explicit Enhancements</h1>
<p>Objectives:</p>
<h2 id="enhancement-points">Enhancement Points</h2>
<p>Hooks at certain points in a program that allow you to attach custom code into a program. The program is executed as if you had hard-coded a change. The difference is that enhancement points will not be replaced by delivered code in an SAP standard upgrade. Upgrade-safe!</p>
<p>Multiple enhancements cannot guarantee an order in which they are called… the first created won’t always run first.</p>
<p>SAP offers enhancement points and sections within enhancement spots.</p>
<p>Composite enhancement spots contains other spots with points.</p>
<p>Customers can use enhancement points and sections by creating an enhancement implementation for teh realted enhancement spot.</p>
<p>We can search for existing enhancement spots</p>
<p>Using explicit enhacenments</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">ENHANCEMENT-POINT</span> ep_a <span class="token keyword">SPOTS</span> ESPOT_X<span class="token punctuation">.</span>
<span class="token keyword">ENHANCEMENT-SECTION</span> es_b <span class="token keyword">SPOTS</span> ESPOT_X<span class="token punctuation">.</span>
	<span class="token eol-comment comment">"code here</span>
<span class="token keyword">END-ENHANCEMENT-SECTION</span><span class="token punctuation">.</span>
</code></pre>
<p>Explicit enhancements are called explicit because they are coded into standard SAP programs in common spots and are ready to use without further thought.</p>
<p>Point - Can add custom code<br>
Section - exists and can add to it</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

