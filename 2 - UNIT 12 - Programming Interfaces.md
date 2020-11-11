---


---

<h1 id="programming-interfaces">Programming Interfaces</h1>
<h2 id="user-interface-overview">User Interface Overview</h2>
<p>We can use GUI Statusus and GUI Titles to add some custom functionlity to a classical report screen.</p>
<h2 id="gui-status">GUI Status</h2>
<p>A menu bar in the interface providing functions to the user.</p>
<p>Includes:</p>
<ul>
<li>Menu bar
<ul>
<li>The top row with file and edit and stuff</li>
</ul>
</li>
<li>Standard toolbar
<ul>
<li>Same on every screen in SAP</li>
</ul>
</li>
<li>App toolbar
<ul>
<li>Contains icons for frequently used functions</li>
</ul>
</li>
<li>Function key settings
<ul>
<li>Use the function key settings to assign functions like Cut  or paste to certain function keys (f1, f2, etc.)</li>
</ul>
</li>
</ul>
<p>A context menu element can be used in multiple GUI statuses</p>
<p>To set a GUI Status:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">SET</span> <span class="token keyword">PF-STATUS</span> <span class="token string">'name'</span><span class="token punctuation">.</span>
</code></pre>
<p>We can then create the status (if it doesn’t exist) by using forward navigation on the name.</p>
<p>A Status can be a normal screen, a dialog box or a context menu.</p>
<p>A Status is created in the menu painter within the ABAP workbench.</p>
<h2 id="function-keys">Function Keys</h2>
<p>We can define shortcut function keys to make different keys do stuff. For example, we could make F1 mean ‘T’ and then that will bring up the Time dialog… we could also link this to an Icon.</p>
<h2 id="gui-title">GUI Title</h2>
<p>A translatable title at the top of the transaction.</p>
<p>We can set the GUI title in a PBO module of a screen:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">SET</span> <span class="token keyword">TITLEBAR</span> <span class="token string">'title'</span><span class="token punctuation">.</span>
<span class="token keyword">SET</span> <span class="token keyword">TITLEBAR</span> <span class="token keyword">WITH</span> variable<span class="token punctuation">.</span>
</code></pre>
<h2 id="gui-status-function-processing">GUI Status Function Processing</h2>
<p>The OK field of the screen holds the function that is being called in the GUI Status</p>
<p>You can find the called function by using a case statement targeting the ok_code in PAI:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">DATA</span> ok_code <span class="token keyword">LIKE</span> sy<span class="token token-operator punctuation">-</span>ucomm<span class="token punctuation">.</span>

<span class="token keyword">MODULE</span> user_command_100 <span class="token keyword">INPUT</span><span class="token punctuation">.</span>
	<span class="token keyword">CASE</span> ok_code<span class="token punctuation">.</span>
		<span class="token keyword">WHEN</span> <span class="token string">'BACK'</span><span class="token punctuation">.</span>
			<span class="token keyword">LEAVE</span> <span class="token keyword">TO</span> <span class="token keyword">SCREEN</span> <span class="token number">0</span><span class="token punctuation">.</span>
	<span class="token keyword">ENDCASE</span><span class="token punctuation">.</span>
<span class="token keyword">ENDMODULE</span><span class="token punctuation">.</span>
</code></pre>
<p>The ok_code ABAP data field still contains the old function code after processing… this can cause some problems down the road…</p>
<p>To prevent this, you must initialize the identically named ABAP field in a PBO module:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLEAR</span> OK_CODE<span class="token punctuation">.</span>
</code></pre>
<p>REVIEW<br>
Subscreens don’t have to be in tabs. Subscrens are in a main screen and can be adjusted dynamically (hidden, for example).</p>
<p>Blocks are only on selection screens for organization</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

