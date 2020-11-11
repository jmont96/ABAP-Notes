---


---

<h1 id="class-based-exceptions">Class Based Exceptions</h1>
<p>Objectives:</p>
<ul>
<li>Explain, handle and debug class-based exceptions.</li>
<li>Define global exception classes</li>
<li>Raise class-based exceptions</li>
<li>Propogate exceptions</li>
<li>Explain hierarchy of predefined exception classes</li>
<li>Explain different way of handling an exception</li>
<li>Retry after exceptions</li>
<li>Implement resumable exceptions</li>
<li>Map exceptions</li>
</ul>
<h2 id="class-based-exceptions-1">Class-Based Exceptions</h2>
<ul>
<li>An exception is represented by an exception object</li>
<li>An exception object is an instance of an exception class</li>
<li>The attributes of the object contain information about the error that occured.</li>
<li>Raise by using RAISE EXCEPTION or a TRY/CATCH block at runtime.</li>
<li>We can build our own classes, but many already exist in SAP.</li>
<li>Naming exceptions typically starts with namespace + CX_
<ul>
<li>For local, use LCX_<br>
All exception classes are derived from one base class, CX_ROOT</li>
</ul>
</li>
</ul>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">TRY</span><span class="token punctuation">.</span>
	<span class="token keyword">CATCH</span> exception_class_1
		<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> action <span class="token keyword">if</span> <span class="token keyword">exception</span> <span class="token keyword">is</span> caught<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
	<span class="token keyword">CATCH</span> exception_class_2
		<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>action <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
	<span class="token keyword">CLEANUP</span> <span class="token punctuation">(</span>if there <span class="token keyword">is</span> <span class="token keyword">no</span> <span class="token keyword">exception</span> <span class="token keyword">handler</span><span class="token punctuation">)</span><span class="token punctuation">.</span>
<span class="token keyword">ENDTRY</span><span class="token punctuation">.</span> 
</code></pre>
<p>To complete this, you need to make sure that the method used in the TRY/CATCH raises the exception.</p>
<p>To determine where an exception occured in your program, use:</p>
<pre class=" language-abap"><code class="prism  language-abap">get_source_position<span class="token punctuation">(</span> <span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<p>We can load a caught exception into a data object, and then use that object to get data from the exception:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CATCH</span> exception_name <span class="token keyword">INTO</span> exception_var<span class="token punctuation">.</span>
	<span class="token keyword">WRITE</span> exception_var<span class="token token-operator punctuation">-&gt;</span>get_text<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="raising-class-based-exceptions">Raising Class-Based Exceptions</h2>
<p>To raise a class-based exception:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">RAISE</span> <span class="token keyword">EXCEPTION</span> <span class="token keyword">TYPE</span> cx_exception <span class="token keyword">EXPORTING</span> attr <span class="token operator">=</span> iv_var<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
</code></pre>
<p>This is the correct way to do this, but if the exception object is defined in our program, but don’t need as much detail:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span><span class="token punctuation">:</span> exception_var <span class="token keyword">TYPE</span> <span class="token keyword">REF</span> <span class="token keyword">TO</span> exxception_class<span class="token punctuation">.</span>

<span class="token keyword">TRY</span><span class="token punctuation">.</span>
	<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">CATCH</span> error <span class="token keyword">INTO</span> exception_var<span class="token punctuation">.</span>
	<span class="token keyword">RAISE</span> <span class="token keyword">EXCEPTION</span> exception_var<span class="token punctuation">.</span>
	
<span class="token keyword">ENDTRY</span><span class="token punctuation">.</span>
</code></pre>
<p>This means any time we load our error into an existing exception variable, we don’t need to re-declare the exception while raising it.</p>
<h2 id="exception-handling-strategies">Exception Handling Strategies</h2>
<ol>
<li>Continue after an ENDTRY after correcting the situation or issuing a warning</li>
<li>Remove the cause of the exception and use a RETRY or a RESUME</li>
<li>Raise and propogate the exception so it is handled appropriately and the program ends.</li>
</ol>
<h2 id="retry">Retry</h2>
<p>The RETRY command will re-run a try-catch block from the top of the TRY.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">TRY</span><span class="token punctuation">.</span>
	<span class="token keyword">CATCH</span> exception_class<span class="token punctuation">.</span>
	<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> Remove what causes the error <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
	<span class="token keyword">RETRY</span><span class="token punctuation">.</span>
<span class="token keyword">ENDTRY</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="resume">Resume</h2>
<p>To use a resume:</p>
<ol>
<li>the exception must be caught using the addition BEFORE UNWIND in your CATCH statement</li>
<li>The exception must be raised with RAISE RESUMABLE in all propogated areas</li>
</ol>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

