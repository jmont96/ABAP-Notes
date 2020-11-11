---


---

<h1 id="web-dynpro-controllers">Web Dynpro Controllers</h1>
<h2 id="controllers">Controllers</h2>
<p>Types of Controllers</p>
<ul>
<li>Component controller
<ul>
<li>Drives functionality of the dynpro component</li>
<li>Visible to all other controllers</li>
<li>Only one in each components</li>
<li>Has no visual interface</li>
<li>Instantiated by WD runtime at start of WD application</li>
<li>Lifetime is equal to lifetime of acomponent</li>
</ul>
</li>
<li>Customer Controller
<ul>
<li>Optional</li>
<li>Can be used to encapsulate subfcuntion of the component controller</li>
<li>Coding in one custom controller should not depend on existence of other custom controller</li>
<li>Delayed until first method of controller is called</li>
<li>Cannot be deleted explicity</li>
</ul>
</li>
<li>Config Controllers
<ul>
<li>Special customer controller</li>
<li>Only neccessary if the component implements special configuation and personlization functions</li>
<li>only one in each components</li>
<li>any controller can access it, but it can’t access other controllers</li>
<li>Instatiated as the first controller of the components</li>
<li>Lives as long as the component</li>
</ul>
</li>
<li>View ontrolers
<ul>
<li>View constsi of a layout part and a view controller</li>
<li>Handles the view specific flow logic like checking user input and handling actions.</li>
<li>Delayed until first mehtod is called</li>
<li>Can be deleted with the component</li>
</ul>
</li>
<li>Window controllers</li>
<li>Each window has one use to handle the data pased thru the inbound plugs when it is reused as a child controller</li>
<li>can call method of the controller fmor the inbound plug methods of teh window</li>
<li>delayed until first method call</li>
<li>cannot be deleted explicity</li>
</ul>
<p>Every controller has WDDOINIT() and WDDOEXIT() methods as well as other hook methods and additional methods that you can add</p>
<p>Implications of one controller C1 using another Controller C2:</p>
<ul>
<li>Controller C1 can map context nodes of controller C2</li>
<li>Controlle rC1 can call methods of controller C2</li>
<li>C1 can access public attributes of C2</li>
<li>C1 can handle events of C2</li>
<li>All controllers use the component controller by default</li>
<li>A view controller cnanot be used</li>
</ul>
<p>To share info between controllers, one controller must declare the use of another controller. This is used for creating a mapped context node or for accessing user-defined method and public attibutes of another controller for whatever reason you need. You may NOT declare use of a view controller, as this is bad MVC practice.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

