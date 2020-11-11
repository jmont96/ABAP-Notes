---


---

<h1 id="introduction-to-web-dynpro">Introduction to Web Dynpro</h1>
<p>Objectives:</p>
<h2 id="web-dynpros">Web Dynpros</h2>
<p>Dynpro - Screen. Called in Module pools mainly but can also be called in a program flow logic.</p>
<p>Dynpro is developed using a declarative approach. Can build a dynpro meta model with some tools in the workbecnh. the source code is built and conforms to a standard architecture known as a web dynpro framework.</p>
<p>The framework allows you to place the custom source code at predefined positions within the generated code.</p>
<p>The standard framwork can be extended to meet any customer needs.</p>
<p>We can define a dynpro interface at both design time and runtime.</p>
<p>Neve rneed to write JS or HTML.</p>
<p>A web dynpro app in ABAP can address all kinds of resuse components directly.</p>
<ul>
<li>Methods of a global classes defined in your system</li>
<li>Function modules in your system or through RFC</li>
<li>Web services through a web service client object</li>
</ul>
<p>Benefits:</p>
<ul>
<li>Minimizes code and design</li>
<li>Separates layout and log</li>
<li>Supports reuse of components</li>
<li>Supports data binding</li>
<li>Compatible with multiple platforms</li>
<li>Browser based</li>
<li>Supports 508 accessiblilty</li>
</ul>
<h2 id="entities-of-a-component">Entities of a component</h2>
<ul>
<li>Windows
<ul>
<li>Navigation</li>
<li>View combination</li>
<li>Has a view controller (window controller)</li>
</ul>
</li>
<li>Views
<ul>
<li>UI</li>
<li>Layout</li>
<li>Has a view controller</li>
</ul>
</li>
<li>Component controller
<ul>
<li>Controls flow logic of a program and gets data</li>
</ul>
</li>
</ul>
<p>View controller can call component controller<br>
Component controller interacts with backend</p>
<h2 id="context-and-data-transport">Context and Data Transport</h2>
<p>Visual way to represent data</p>
<p>Each controller has nodes, which have attributes and act like a tree. Think of nodes as individual elements like a structure or could represent an internal table.</p>
<p>Build everything you need in component controller and share neccessary nodes with each view controller to be delivered to the view or window to show in elements on the screen.</p>
<p>Data transport is done through mapping not parameter passing.</p>
<p>Nodes are copied into both the view and component controllers so they are shared. The component controller has data access and can call backend services.</p>
<p>Data in each controller’s context is mapped to back the views data with controlled data from the component controller. Data binding then occurs, which is used to display dynamic data in the view layout that is backed by the view controller’s context.</p>
<p>Very similar to MVC.</p>
<h2 id="naviatgion">Naviatgion</h2>
<p>Windows have multiple views that you can navigate between.</p>
<p>All UI elements are backed by some code that controls their behavior. An exmaple is a button that does something when it is clicked.</p>
<p>Inbound and Outbound plugs are communicators that link to each and trigger a navigation to another view.</p>
<p>Outbound plugs are fired to trigger a move in navigation. Inbound plugs accept these fired triggers and finish the navigation process.</p>
<p>To define nav:</p>
<ol>
<li>Create exit and entry points for each view using outbound and inbound plgugs</li>
<li>Specify the navigation flow using navigatioin links</li>
</ol>
<p>Always have a default view (Dark blue colored in editor)</p>
<h2 id="view-assembly">View Assembly</h2>
<p>An Assembly is a subset of views visible at any time.</p>
<ul>
<li>Can nest views inside of a view container</li>
<li>Each container has a default view</li>
<li>Views in one container can navigate to views in a different container</li>
</ul>
<p>Windows and views</p>
<ul>
<li>A window is a set of all possble views that can make up a visible screen</li>
<li>A window defines which views are displayed in what combination, and how the view combination changes by firing plugs</li>
<li>A view can have container areas defined by the ViewContainerUIElement, which allows nesting</li>
<li>A ViewContainerUIElement can only display one view at a time</li>
</ul>
<p>When you create a window, remember:</p>
<ul>
<li>You must embed all posisble views that can exist in the visual interface of teh component window</li>
<li>To dipslay multiple views in parallel define the layout and position of tehv iews in a special view container ViewContainerUIElement in its layout</li>
<li>Define the nav links between the different views</li>
</ul>
<h2 id="mvc">MVC</h2>
<p>Model</p>
<ul>
<li>Business interaction layer</li>
<li>Represents data</li>
<li>Generates app data and has no care for how it is displayed</li>
<li>Business logic is not part of the Web Dynpro Component</li>
</ul>
<p>View</p>
<ul>
<li>User interaction layer</li>
<li>Visualizes the app data without caring how it was generated or where it came from</li>
</ul>
<p>Controller</p>
<ul>
<li>Binding layer</li>
<li>Binds the user and business interaction layers together</li>
<li>All intermediate processing is performed here</li>
<li>Works like a request/response model</li>
</ul>
<p>Can build customer controllers to modularize things and divide controller responsibility among multiple controllers.</p>
<p>We can make a controller’s context public so its methods are accessible by other modules.</p>
<p>Views can also be made public and be included in other modules.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

