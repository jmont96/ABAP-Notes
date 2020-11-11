---


---

<h1 id="repository-objects">Repository Objects</h1>
<p>Objectives</p>
<ul>
<li>Create, test and use global classes.</li>
<li>Define and implement global interfaces</li>
<li>Import local classes and interfaces</li>
<li>Generate UML diagrams for global classes</li>
<li>Implement inheritance in global classes</li>
<li>change display of components in global classes</li>
</ul>
<h2 id="global-classes--interfaces">Global Classes &amp; Interfaces</h2>
<p>To create a global class, we need to create the object in the dictionary or the object navigator. This is done by sortin through tabs and not 100% coding the class like in local classes. From there, we can declare all of the same components in a global class as we can in a local one, with a few additional capabilities. Bottom line, global classes are the sneed to be created differently.</p>
<p><strong>Naming Convention</strong></p>
<ul>
<li>Customer class names are typically ZCL_##</li>
<li>Customer interfaces arenamed ZIF_####</li>
<li>SAP names don’t include Z or Y.</li>
</ul>
<p><strong>Additional Information</strong></p>
<ul>
<li>We also have the ability to perform a redeifintion and can use inheritance between global classes
<ul>
<li>To have inheritance in a global class we must define the relationship in the properties of the class.</li>
</ul>
</li>
<li>Testing  global classes is usingthe test environment. We can also create instances from here if needed.</li>
<li>To show a UMl diagram for a class, we can right click on it and go to display.</li>
<li>You can also define local types and classes inside of a global class frmo hte class builder.
<ul>
<li>These are encapsulated, and you CANNOT access them from outside the global class.</li>
</ul>
</li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

