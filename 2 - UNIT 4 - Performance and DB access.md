---


---

<h1 id="performance-and-db-access">Performance and DB Access</h1>
<p>Objectives:</p>
<ul>
<li>Describe the use of and create DB indexes</li>
<li>Apply settings for table buffering</li>
<li>Describe buffering types</li>
<li>Set up table buffering</li>
</ul>
<h2 id="db-access">DB Access</h2>
<p>Why can’t you do database work directly (need DB interface)</p>
<ol>
<li>Don’t have authorization, since there’s only one user that can access the DB</li>
<li>Lock processes - we don’t use locks outside of ABAP</li>
<li>Foreign keys only exist at DB level</li>
</ol>
<h2 id="indexes">Indexes</h2>
<p>An index is kind of like a table of contents. They are essentially a copy of a DB table reduced to just a few fields. The index is searched first (by the DB optimizer), reducing the amount of reads that need to be made in a table by targeting a specific section.</p>
<p>Indexes are mainly used to improve performance, and can speed up read times by a lot if you are reading a ton of records.</p>
<p>There are pros and cons of using indexes.</p>
<p>Tips:</p>
<ul>
<li>Lots of inserts and updates and other transactions data will be slower if there are indexes.</li>
<li>Used mostly for access through reads</li>
<li>Indexes should be as small as possible</li>
<li>An index must contain only the most significant fields</li>
</ul>
<p>Types of indexes:</p>
<ul>
<li>Primary Index
<ul>
<li>This is automatically created when a table is activated for the first time. It will contain the key fields of the table.</li>
</ul>
</li>
<li>Secondary Index
<ul>
<li>Useful is a large table is read with selection conditions other than the key fields. Most secondary indexes are non-unique.</li>
</ul>
</li>
<li>Extension Index
<ul>
<li>Customer created index that is upgrade safe</li>
</ul>
</li>
</ul>
<p>SAP uses an optimizaer to determine what is the best access path… This basically determines whether or not to use indexes for access based on the request form the user.</p>
<p>To create an index</p>
<ol>
<li>Go into a table</li>
<li>Press the indexes button in the menu (says “indexes”)</li>
<li>Press white sheet button</li>
<li>Create index</li>
<li>Give 3 character name</li>
<li>Give desc</li>
<li>Enter options and create with specific fields in mind</li>
</ol>
<h2 id="buffering">BUFFERING</h2>
<p>Loading a part of a table or a full table into a localized buffer that reduces read time. It is MUCH faster reading from a buffer than repeatedly accessing the DB.</p>
<p>Process:</p>
<ol>
<li>Call comes in</li>
<li>Hits database interface</li>
<li>DB intercae checks to see if info is in the buffer
<ol start="4">
<li>If it is, then it is returned</li>
<li>iIf not, then the DB interface goes to the network to find the data in the database</li>
</ol>
</li>
</ol>
<h2 id="types-of-buffering">Types of Buffering</h2>
<p><strong>Full Buffering</strong><br>
The entire table will go into the buffer to preserve performance in the future.</p>
<p>When to use:</p>
<ol>
<li>If a table is smaller than 32kb</li>
<li>If keys are never used in conditional selection</li>
</ol>
<p><strong>Generic Buffering</strong><br>
If the table is too big and you can’t buffer it all, you can limit the data based on key fields.<br>
Example: You try to access key field ‘airline’ by selecting “American Airlines” All rows that include “American Airlines” in the key field of <em>Airline</em> will be buffered.</p>
<p>When to use:</p>
<ol>
<li>If a key is used in a select statement often</li>
<li>If a table is too large to use full buffering</li>
</ol>
<p><strong>Single Record Buffering</strong><br>
Will load one record that you select with SELECT SINGLE into the buffer. This should be used for accessing one record many times from a table.</p>
<p>When to use:</p>
<ol>
<li>If you repeatedly access one record or a few records using SELECT SINGLE</li>
</ol>
<p>You CAN turn buffering off if you really want to, but this is not recommend unless you are writing to a table a lot.</p>
<h2 id="buffer-synchronization">Buffer Synchronization</h2>
<p>It is possible that an application server can hold a buffer with incorrect data, since another program could have come along and edited data since the application server last buffered data. Becuase of this, we need a sync process to ensure that the buffer holds accurate data</p>
<p><strong>Problem</strong><br>
Example:<br>
AS 1 selects airline data and buffers the full table.  Now, so does AS2. Now they both have the same data in their buffers and it is accurate<br>
Suppose AS1 deletes Japan airlines from the DB and their buffer. The buffer in AS1 is up to date, but is AS2’s buffer? It will still show Japan airlines in the buffer, even though it isn’t in the DB.</p>
<p>Summary: writes can cause buffers to be inaccurate</p>
<p><strong>Solution</strong><br>
The process to sync these will check all of the app servers and make sure their buffers are okay and match with the DB.  If a buffer does not match the DB, the buffer is destroyed. Now, next time a select call is made, the buffer will be restarted with a call to the DB.</p>
<p>You can set a time between sync processes… between 60 and 360 seconds. SAP recommends 60-240 seconds to run a sync process.</p>
<p>Summary</p>
<ul>
<li>Only tables that are mostly read only should be buffered. Should avoid writes on buffered tables.</li>
<li>Tables that change frequently should not use buffers. It will slow thigns down and need a lot of sync processes running.</li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

