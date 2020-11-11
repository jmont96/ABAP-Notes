---


---

<h1 id="screen-programming">Screen Programming</h1>
<h2 id="user-dialogs">User Dialogs</h2>
<p>A form of interaction between the user and the program</p>
<p>Examples:</p>
<ul>
<li>Exntering data</li>
<li>Choosing a menu item</li>
<li>Clicking a button</li>
<li>Clicking or Double-clicking a list entry</li>
</ul>
<h2 id="single-screen-transaction-model">Single-Screen Transaction Model</h2>
<ul>
<li>Input and data screens combined into one window</li>
<li>Switch between create, change and display</li>
<li>Direct access to each object</li>
<li>System retains context after saving</li>
</ul>
<h2 id="abap-program-types">ABAP Program Types</h2>
<p>ABAP program types can be complete or imcomplete, just like data types.</p>
<p>Types:</p>
<ul>
<li>Complete types - Can be executed
<ul>
<li>Executable Program (1)
<ul>
<li>Can be ran like as a report</li>
</ul>
</li>
<li>Module Pool (M)
<ul>
<li>Must have a transaction code to execute</li>
<li>Uses a lot of includes and PBO/PAI modules</li>
</ul>
</li>
</ul>
</li>
<li>Imcomplete types - Cannot be executed by themselves
<ul>
<li>Function Group (F)
<ul>
<li>Contains function mdoules, local data types, global data objects and screens.</li>
</ul>
</li>
<li>Include Program (I)
<ul>
<li>Can contain anything</li>
</ul>
</li>
<li>Interface Pool (J)
<ul>
<li>Contains a global interface which in turn can contain local data types and constants</li>
</ul>
</li>
<li>Class Pool (K)
<ul>
<li>A class pool contains a global class which in turn can contain constants, local data types, local classes and interfaces</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2 id="program-organization">Program Organization</h2>
<p>Includes: Always start with MZ, or SAPMZ for SAP standard</p>
<ul>
<li>TOP: Global declarations</li>
<li>E01: Events</li>
<li>F01: Form routines</li>
<li>I01: PAI Module</li>
<li>O01: PBO Module</li>
</ul>
<h2 id="intro-to-screen-programming">Intro to Screen Programming</h2>
<p>A screen is a container of elements that we want to display through input and/or output fields.</p>
<p>Advantages</p>
<ul>
<li>Data entry with consistency checks backed by ABAP dictionary</li>
<li>User-friendly dialogs with many UI elements</li>
</ul>
<p>How do screens work?</p>
<ul>
<li>The screen is loaded from reposityory into the runtime environment</li>
<li>You can have one or more screens</li>
<li>The first screen is typically displayed, then the processing block is executed afterwards. We use PBO and PBI to handle code before and after the screen is displayed. PBO is the code before the screen is displayed, and PAI is after the screen is executed</li>
<li>Elements on the screen could have attributes like active, available for input, hidden, etc.
<ul>
<li>These attributes can be dynamic or static</li>
</ul>
</li>
<li>Each screen belongs to a program, so different programs could both have a screen 100.</li>
</ul>
<h2 id="screen-attributes">Screen Attributes</h2>
<ul>
<li>Admin
<ul>
<li>Program</li>
<li>Screen num</li>
<li>Desc</li>
<li>Screen group</li>
<li>Status</li>
<li>Orig. language</li>
</ul>
</li>
<li>Type
<ul>
<li>Normal</li>
<li>Subscreen</li>
<li>Modal</li>
<li>Selection Screen</li>
</ul>
</li>
<li>Size
<ul>
<li>Static</li>
<li>Dynamic (expandable and movable)</li>
</ul>
</li>
<li>Sequence
<ul>
<li>Next screen</li>
</ul>
</li>
<li>Settings
<ul>
<li>Cursor position</li>
<li>Runtime compression</li>
<li>Context menu</li>
<li>Etc.</li>
</ul>
</li>
</ul>
<h2 id="screen-components">Screen Components</h2>
<p>A screen consists of:</p>
<ul>
<li>Flow logic… PBO and PAI</li>
<li>Screen mask with UI elements for I/O</li>
<li>Screen Attributes</li>
</ul>
<h2 id="creating-a-screen-and-screen-elements">Creating a Screen and Screen Elements</h2>
<p>Screen creation starts in the screen painter tool, where we can add:</p>
<ul>
<li>Screen attributes</li>
<li>Screen layout (in the layout editor)</li>
<li>Element attributes</li>
<li>Flow logic</li>
</ul>
<h2 id="data-visibility">Data Visibility</h2>
<p>Data in the screen must be the exact same as in ABAP for a screen and its ABAP program to be able to communicate.</p>
<p>In screen processing:</p>
<ul>
<li>The ABAP processor controls the program flow in a module</li>
<li>The DYNP processsor controls the flow logic and prepares data to be displayed on the screen</li>
</ul>
<h2 id="modify-screens-at-runtime">Modify Screens At Runtime</h2>
<p>At the beginning of PBO, the runtime system reads the current screen into a system table with the line type SCREEN. This table contains the dynamically modifiable attributes of each screen element.</p>
<p>To change these elements, we can loop through the table in a PBO module:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">MODULE</span> modify_screen <span class="token keyword">OUTPUT</span><span class="token punctuation">.</span>
	<span class="token keyword">LOOP</span> <span class="token keyword">AT</span> <span class="token keyword">SCREEN</span><span class="token punctuation">.</span>
		<span class="token keyword">IF</span> <span class="token keyword">screen</span>-group1 <span class="token operator">=</span> <span class="token string">'SEL'</span><span class="token punctuation">.</span>
			<span class="token keyword">screen</span>-input <span class="token operator">=</span> <span class="token number">1</span><span class="token punctuation">.</span>
		<span class="token keyword">ENDIF</span><span class="token punctuation">.</span>
		<span class="token keyword">IF</span> <span class="token keyword">screen</span>-name <span class="token operator">=</span> <span class="token string">'FIELD1'</span><span class="token punctuation">.</span>
			screenactive <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">.</span>
		<span class="token keyword">ENDIF</span><span class="token punctuation">.</span>
		<span class="token keyword">MODIFY</span> <span class="token keyword">SCREEN</span><span class="token punctuation">.</span> <span class="token eol-comment comment">"Executes the change</span>
	<span class="token keyword">ENDLOOP</span><span class="token punctuation">.</span>
<span class="token keyword">ENDMODULE</span><span class="token punctuation">.</span>
</code></pre>
<p>We can query the screen-name and screen-group targets to find our elements for changing.</p>
<h2 id="designing-screen-sequences">Designing Screen Sequences</h2>
<p>You often need multiple screens for complex transactions. In each transaction code we create, there will be an initial screen that you specify.</p>
<p>Each screen from the initial will lead t another screen based on the screen’s attributes. This is the static sequence, but we can also interrupt this sequence dynamically at runtime.</p>
<p>To temporarily overwrite the value assigned to the next screen attribute of a screen:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">MODULE</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
	<span class="token keyword">SET</span> <span class="token keyword">SCREEN</span> <span class="token number">300</span><span class="token punctuation">.</span>
	<span class="token keyword">LEAVE</span> <span class="token keyword">SCREEN</span><span class="token punctuation">.</span> <span class="token eol-comment comment">"Terminates current screen and goes to PBO of screen 300.</span>
<span class="token keyword">ENDMODULE</span>
</code></pre>
<p>To do this in one statement:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">LEAVE</span> <span class="token keyword">TO</span> <span class="token keyword">SCREEN</span> <span class="token number">300</span><span class="token punctuation">.</span>
</code></pre>
<p>To insert a screen or a sequence of screens in a program:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">MODULE</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
	<span class="token keyword">CALL</span> <span class="token keyword">SCREEN</span> <span class="token number">300</span><span class="token punctuation">.</span>
	<span class="token eol-comment comment">"returns here after 300 is done</span>
<span class="token keyword">ENDMODULE</span><span class="token punctuation">.</span>
</code></pre>
<p>This will build a stack where the newly called screen is pushed to the top. After the screen is used, you can return to the line below CALL SCREEN in the PAI Module:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token eol-comment comment">"Screen 300 PAI Module</span>
<span class="token keyword">SET</span> <span class="token keyword">SCREEN</span> <span class="token number">0</span><span class="token punctuation">.</span> <span class="token keyword">LEAVE</span> <span class="token keyword">SCREEN</span><span class="token punctuation">.</span>
<span class="token eol-comment comment">"OR</span>
<span class="token keyword">LEAVE</span> <span class="token keyword">TO</span> <span class="token keyword">SCREEN</span> <span class="token number">0</span><span class="token punctuation">.</span>
</code></pre>
<p>The cursor of a screen is automatically placed in the first input field. We can overwrite this in the PBO module of a screen:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">SET</span> <span class="token keyword">CURSOR</span> <span class="token keyword">FIELD</span> field_name<span class="token punctuation">.</span>
</code></pre>
<p>A dialog box is a floating popup modal as a screen.</p>
<p>To call a dialog box, we need to set the coordinates:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CALL</span> <span class="token keyword">SCREEN</span> <span class="token number">100</span> 
	<span class="token keyword">STARTING</span> <span class="token keyword">AT</span> &lt;col&gt;&lt;row&gt;
	<span class="token keyword">ENDING</span> <span class="token keyword">AT</span> &lt;col&gt;&lt;row&gt;<span class="token punctuation">.</span>  <span class="token eol-comment comment">"Ending is optional</span>
</code></pre>
<p>This can determine the size dynamically for a dialog popup modal.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

