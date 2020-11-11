---


---

<h1 id="implicit-enhancements">Implicit Enhancements</h1>
<p>Objectives:</p>
<h2 id="implicit-vs.-explicit">Implicit vs. Explicit</h2>
<p>Implicit enhancement points provide you with option to add a source code enhancement to SAP code in methods, functions and programs without preparation by SAP. More flexible than explicit, but still upgrade-safe!</p>
<p>What can we do with these?</p>
<ul>
<li>Add interface params</li>
<li>Add additonal attibutes in SAP classes</li>
<li>Pre and post processing functions for global SAP methods</li>
<li>Replacement for global SAP methods</li>
</ul>
<p>Like mentioned before, we don’t need preparation by SAP developers and don’t need to ever make modifications with implicit enhancements!</p>
<p>To create one:</p>
<ol>
<li>First show where they are in the code by clicking button in menu</li>
<li>Implementation can be created by putting your cursor on the enhancement and choosing ‘Create Enhancement Implementaion’</li>
</ol>
<h2 id="implicit-enhancement-options">Implicit Enhancement Options</h2>
<ul>
<li>Adding optional paramters to method interfaces, can’t use returning or exceptions</li>
<li>Defining additional attributes and methods</li>
<li>Defingin a pre method a post method for an SAP method (alternatively, define an overwrite method)</li>
</ul>
<p>Implicit Enhancement Points</p>
<ul>
<li>Adding additional logic</li>
<li>Implementing addition methods</li>
</ul>
<h2 id="class-enhancements">Class Enhancements</h2>
<p>Possibilites</p>
<ul>
<li>Add new methods or add functionality toexisting methods</li>
<li>Adding parameters to methods</li>
<li>Changing the way methods are triggered or executed using pre and post methods</li>
</ul>
<h2 id="pre-and-post-methods">Pre and Post Methods</h2>
<p>Methods called before, after, or instead of the SAP method to which they are linked. When an overwrite method is created, it is not possible to have pre OR post methods for the same original method.</p>
<p><strong>Pre Methods</strong></p>
<ul>
<li>Executed before the original method</li>
<li>Used for initialization, validation, or preparation</li>
</ul>
<p><strong>Post Methods</strong></p>
<ul>
<li>Executed after running the original method and the pre method</li>
<li>Used to enhance the data coming from a method to add extra features</li>
</ul>
<p><strong>Overwrite Methods</strong></p>
<ul>
<li>Act as a replacement of the original method</li>
</ul>
<p>The chain pre-method-&gt;methodxyz-&gt;post-method can be interuppted at runtime (parts aren;t executed) if:</p>
<ul>
<li>If an exception is thrown by methodxyz</li>
<li>If an exception is raised within the pre method</li>
</ul>
<p>When pre post and overwrite methods are created, the system will make a local class n ame lcl_enhancement_name. You can access this through the CORE_OBJECT reference.</p>
<p>This class can implement the following interfaces:</p>
<ul>
<li>IPR_enhancement_name for pre</li>
<li>IPO_enhancement_name for post</li>
<li>IOW_enhancement_name for overwrite</li>
</ul>
<h2 id="restrictions">Restrictions</h2>
<ul>
<li>Pre methods don’t have exports</li>
<li>Post methods don’t have exports but instead have changing params</li>
<li>The returing param of a functional method becomes a changing param</li>
<li>Overwrite methods have the same signature as the original method</li>
<li>You can’t change the parm defintion of these methods</li>
</ul>
<h2 id="advantages-of-pre-and-post-methods-over-implicit-source-code-enhamncements">Advantages of pre and post methods over implicit source code enhamncements</h2>
<ul>
<li>Higher abstraction due to separate address space</li>
<li>Less adjustment effort during upgrade</li>
<li>Methods are stored in a local enhancement class</li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

