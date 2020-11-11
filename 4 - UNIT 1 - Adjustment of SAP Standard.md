---


---

<h1 id="adjusting-sap-standard-software">Adjusting SAP Standard Software</h1>
<p>Objectives:</p>
<ul>
<li>Describe the options for adjusting the SAP standard system</li>
<li>Describe enhancement types</li>
</ul>
<h2 id="options-for-changing-sap-standard">Options for Changing SAP Standard</h2>
<ul>
<li>Customization
<ul>
<li>Configure specific business processes and functions for your system based on an Implementation Guide (IMG)</li>
</ul>
</li>
<li>Personalization
<ul>
<li>Allows screen properties to be adapted and simplified</li>
<li>No coding needed</li>
</ul>
</li>
<li>Modification
<ul>
<li>Directly changing SAP repository objects in teh customer system</li>
<li>Not upgrade safe</li>
</ul>
</li>
<li>Enhancement
<ul>
<li>Enhancements allow you to adapt SAP Repo objects in an upgrade-safe way
<ul>
<li>Customer Exits</li>
<li>Business Transaction Events</li>
<li>BADIs</li>
<li>Explicit and Implicit enhancements</li>
<li>Dictionary Items
<ul>
<li>Tables</li>
<li>Data Elements</li>
<li>Domains</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>Customer Development
<ul>
<li>New object in the repo created by the customer in their namespace (Z or Y)</li>
<li>Upgrade-safe</li>
</ul>
</li>
</ul>
<h2 id="decision-tree">Decision Tree</h2>
<p>Can customizing satify the customer request?<br>
If yes then use customization and personalizing</p>
<p>Is similar functionality available in SAP standard? If No, then use Customer Decvelopment or CSP (complimentary software program) solution</p>
<p>Can and enhancement satisfy the customer? If yes then do an enhancements, if not then do a modification at worst case scenario.</p>
<h2 id="enhancement-types">Enhancement Types</h2>
<ul>
<li>Abap Dictionary Enhancements
<ul>
<li>Tables</li>
<li>Data Elements
<ul>
<li>Can change labels and stuff, but that’s discouraged</li>
</ul>
</li>
<li>Domains</li>
</ul>
</li>
<li>Program Enhancements
<ul>
<li>Adding custom code to a program</li>
</ul>
</li>
<li>Menu Enhancements
<ul>
<li>Has to be pre-programmed by SAP</li>
</ul>
</li>
<li>Screen Enhancements
<ul>
<li>Has to be pre-programmed by SAP</li>
</ul>
</li>
</ul>
<h2 id="table-enhancements">Table Enhancements</h2>
<p>Use an append strcture or A CI_Include (customizaiton include)</p>
<ul>
<li>Append structure will add fields using append functionality</li>
</ul>
<h2 id="program-enhancements">Program Enhancements</h2>
<p>Can use an enhancement call, which calls an object in the customer namespace to perform some functionality.</p>
<h2 id="menu-enhancements">Menu Enhancements</h2>
<p>Use customer exits and BADIs</p>
<ul>
<li>These are merged into the GUI status and can be identified using a ‘+’</li>
<li>You can define text for menu enhacements</li>
</ul>
<h2 id="screen-enhancements">Screen Enhancements</h2>
<p>A screen exit provides the option to include additional screen elements on an SAP screen without need for a modificaiton. can use append fields<br>
To do this:</p>
<ol>
<li>Define subscreen area</li>
<li>Program corresponding calls in the flow logic</li>
<li>Provide the framework for data transport</li>
<li>Include the sreen exit in an enhancement (customer exit or BADI)</li>
<li>Maintain documentation</li>
</ol>
<p>Bustiness Transaction Events (BTE) using function modules. BADIs use methods.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

