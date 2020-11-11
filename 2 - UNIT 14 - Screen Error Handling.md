---


---

<h1 id="error-handling-in-screens">Error Handling In Screens</h1>
<p>In ABAP, it is good practice to handle errors using dialog messages and field input checks.</p>
<p>Can use CHAIN command to check groups of fields in PAI of screen painter:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CHAIN</span><span class="token punctuation">.</span>
	<span class="token keyword">FIELD</span><span class="token punctuation">:</span> field_1<span class="token punctuation">,</span> field_2<span class="token punctuation">,</span> field_3<span class="token punctuation">.</span>
	<span class="token keyword">MODULE</span> check_input<span class="token punctuation">.</span>
<span class="token keyword">ENDCHAIN</span><span class="token punctuation">.</span>
</code></pre>
<h2 id="messages">Messages</h2>
<p>Types of messages</p>
<ul>
<li>A: Termination
<ul>
<li>The process terminates, the user must restart trasaction</li>
</ul>
</li>
<li>X: Exit
<ul>
<li>The process terminates with short dump message_type_x</li>
</ul>
</li>
<li>E: Error
<ul>
<li>Process interrupts, user must retry entry</li>
</ul>
</li>
<li>W: Warning
<ul>
<li>User may correct entries but doesn’t have to</li>
</ul>
</li>
<li>I: Info
<ul>
<li>User can continue without doing anything really</li>
</ul>
</li>
<li>S: Success
<ul>
<li>Success message</li>
</ul>
</li>
</ul>
<h2 id="field-checks">Field Checks</h2>
<p>Automatically checked in ABAP</p>
<ul>
<li>Mandatory field checks
<ul>
<li>Makes sure they are filled out</li>
</ul>
</li>
<li>Field format checks
<ul>
<li>Type checks and so on</li>
</ul>
</li>
<li>Fixed values
<ul>
<li>Domain checks. The help function can help the user choose possible options when needed</li>
</ul>
</li>
<li>Foreign key check
<ul>
<li>Can only do this check if a screen field refers to a dictionary field for which a check table is defined</li>
</ul>
</li>
</ul>
<h2 id="field-input-checks-with-error-dialogs">Field Input Checks With Error Dialogs</h2>
<p>The field is placed into PAI, the module then follows the Field and can display a message from the module.</p>
<p>The module is processed only for the fields you speficy.</p>
<p>If the error occurs, the same screen is returned but does not re-process the PBO step.</p>
<p>Only the specified field is ready for input after an error… this is an issue</p>
<p>You can use multiple chain statements for different checking methods</p>
<p>Fields can be recycled and used in multiple chain blocks</p>
<p>After changes are made prior to error throwing, changes can be made by the user. Now, PAI is not completely reprocessed, but instead picks up where it left off adjusting to the user’s changes.</p>
<p>To summarize, PAI will begin where the first reference is the the input field that was changed.</p>
<p>Example: If B is changed after an error in check_bc, PAI continues on line 2 of this example.</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token number">1</span> <span class="token operator">-</span> <span class="token keyword">FIELD</span> A <span class="token keyword">MODULE</span> check_A<span class="token punctuation">.</span>
<span class="token number">2</span> <span class="token operator">-</span> <span class="token keyword">FIELD</span> B <span class="token keyword">MODULE</span> check_B
<span class="token number">3</span> <span class="token operator">-</span> <span class="token keyword">CHAIN</span><span class="token punctuation">.</span>
<span class="token number">4</span> <span class="token operator">-</span> <span class="token keyword">FIELD</span> B<span class="token punctuation">,</span> <span class="token keyword">C</span><span class="token punctuation">.</span> 
<span class="token number">5</span> <span class="token operator">-</span> <span class="token keyword">MODULE</span> check_bc<span class="token punctuation">.</span>
<span class="token number">6</span> <span class="token operator">-</span> <span class="token keyword">ENDCHAIN</span><span class="token punctuation">.</span> 
</code></pre>
<p>Using the ON INPUT keyword we can choose to only call the module if the fields have changed from their initial value:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">MODULE</span> module_name <span class="token keyword">ON</span> <span class="token keyword">INPUT</span><span class="token punctuation">.</span>
<span class="token eol-comment comment">"If we use a chain...</span>
<span class="token keyword">MODULE</span> module_name <span class="token keyword">ON</span> <span class="token keyword">CHAIN-INPUT</span><span class="token punctuation">.</span>
</code></pre>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

