---


---

<h2 id="modifications">Modifications</h2>
<p>Objectives:</p>
<h2 id="overview">Overview</h2>
<p>Everything in our development systems that is SAP-built is considered a ‘copy.’</p>
<p>The system will flag you if you try to make changes to a ‘copy,’ since you might lose your changes later on after an upgrade.</p>
<p>Everything that was built in a development system will also be flagged as a ‘copy’ if the current system isnt an original (prod, for example, never has anything new created in it).</p>
<p>Changes to an original are called <em>corrections</em></p>
<p>Corrections are also recorded in a change request.</p>
<h2 id="conflicts">Conflicts</h2>
<p>Conflicts occur when you have changed any SAP object and SAP also delivers a new version of it which becomes active in the repository.</p>
<p>To fix conflicts, you have to make a modification adjustment, which can be extremely time consuming.</p>
<p>Only perform modification adjustments in you development system, but try to avoid them if possible.</p>
<h2 id="repair">Repair</h2>
<p>The developer changing SAP objects must register those changes using SSCR (SAP software change Registration).</p>
<p>Benefits:</p>
<ul>
<li>Quick error resolution</li>
<li>SAP will log all changes</li>
<li>Dependable operation, prevents unintended modifications.</li>
<li>Simplification of upgrades</li>
</ul>
<p>If you want to change an SAP standard repo object, you must provide the SSCR key and the change request number. A repair task is then created.</p>
<p>The assignment to the change request has the following implications:</p>
<ul>
<li>Change lock - only the owner can change</li>
<li>Import lock - object cannot be overwritten by an import (upgrade)</li>
<li>Version creation - system generates new version</li>
</ul>
<h2 id="post-modification-steps">Post Modification Steps</h2>
<p>After development, the programmer releases the task. The change lock and import lock are transferred to the change request to which the task belongs.</p>
<p>Only the developer can release the the import lock.</p>
<p>After completing the project you release the change request. This removes all of the object locks.</p>
<h2 id="critical-success-factors-for-modifications">Critical Success Factors for Modifications</h2>
<ul>
<li>Use smart design patterns, call a function in the customer namespace and minimize the code in the SAP program.</li>
<li>Use standard documentation</li>
<li>Do not delete SAP source code, just comment it</li>
<li>Keep a modification logbook</li>
<li>Do not modify any central basis dictionary objects</li>
<li>Release all requests that contain repairs before upgrade/support package installation</li>
</ul>
<h2 id="modification-assistant">Modification Assistant</h2>
<ul>
<li>Making modication easier</li>
<li>Records changes at more detailed level</li>
<li>Records changes in a speara lyaer making a reset much easier for rollbacks</li>
</ul>
<p>How does the assistant work?</p>
<p>The assistant keeps source code in a completely different place than the modification code (mod layer and source layer).</p>
<p>When a load is generated for runtime the two are combined to build a load, but still stay separate in layers outside of the load after it is generated. This ensures easy rollbacks when required, but still considers the modification when building the source code.</p>
<p>The Modification Assistant works at the module level.</p>
<p>There are many tools supported by the Modification assisstant.</p>
<h2 id="implementing-user-exits">Implementing User Exits</h2>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">PERFORM</span> userexit_abc<span class="token punctuation">.</span>
<span class="token keyword">PERFORM</span> userexit_xyz<span class="token punctuation">.</span>
</code></pre>
<p>These exits map to a form in another module. Includes are used to make this happen.</p>
<p>Search for them in a global program using the keyword ‘perform’.<br>
Can also search the IMG.<br>
can double click to navigate to subreport.</p>
<p>Technically a modification but SAP says they will never touch it.</p>
<h2 id="adjusting-the-modification">Adjusting the Modification</h2>
<p>Adjustments are required for anything that is modified by the customer when an upgrade is delivered.</p>
<p>During a modification adjustment you can compare the old and new versions of ABAP repo objects using teh trasnactions SPDD and SPAU</p>
<p>SPDD: Used for comparison and adjustment of Dictionary Objects<br>
SPAU: Used for adjustment of other repo objects.</p>
<p>SPDD</p>
<ul>
<li>Domains</li>
<li>Data Elements</li>
<li>Tables</li>
</ul>
<p>SPAU</p>
<ul>
<li>ABAP programs</li>
<li>User interfaces</li>
<li>Screens</li>
<li>Search helps</li>
<li>Views</li>
<li>Lock objects</li>
</ul>
<h2 id="transport-of-an-adjustment">Transport of an adjustment</h2>
<p>There will be two separate transports:</p>
<ul>
<li>One is for SPDD</li>
<li>One is for SPAU</li>
</ul>
<p>Requests with adjusted objects are used when you upgrade downstream systems and releases are generated.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

