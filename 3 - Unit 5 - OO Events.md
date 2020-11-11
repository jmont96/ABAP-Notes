---


---

<h2 id="oo-events">OO Events</h2>
<p>Objectives</p>
<ul>
<li>Implement event-controlled methods</li>
<li>Trigger and handle event</li>
<li>Register for events</li>
<li>Explain visbility sections in event handling</li>
<li>Implement events in local interfaces</li>
</ul>
<h2 id="event-controlled-method-calls">Event-Controlled Method Calls</h2>
<ul>
<li>A class can emit an event message to different recipient/handlers.</li>
<li>This is similar to listeners in other languages (On_object_created())</li>
<li>There can be static and instance events</li>
<li>Events can also be defined in interfaces</li>
<li>You basically define a method that is kinda like a listener for an event to happen somewhere</li>
<li>The listener can be located in the host class or in another class</li>
<li>An event must be raised from within the class hosting the event in its DEFINITION block</li>
</ul>
<p>Defined in a host class as:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">EVENTS</span> vehicle_created<span class="token punctuation">.</span>
</code></pre>
<p>Triggered to emit in the implementation host constructor (or elsewhere) by:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">RAISE</span> <span class="token keyword">EVENT</span> vehicle_created<span class="token punctuation">.</span>
</code></pre>
<p>Listener method defined in using class by:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">CLASS</span> lcl_rental <span class="token keyword">DEFINITION</span><span class="token punctuation">.</span>
	<span class="token keyword">METHODS</span><span class="token punctuation">:</span> on_vehicle_created <span class="token keyword">FOR</span> <span class="token keyword">EVENT</span> vehicle_created
			<span class="token keyword">OF</span> lcl_vehicle <span class="token keyword">IMPORTING</span> sender<span class="token punctuation">.</span> 
<span class="token keyword">ENDCLASS</span><span class="token punctuation">.</span>
</code></pre>
<p>Note: You have to use ‘sender’ here as an import.<br>
Sender is the address of the object that raised the event, so you have access to all of the objects methods and other information.</p>
<p>Implemented in a listening class’s constructor as:</p>
<pre class=" language-abap"><code class="prism  language-abap"><span class="token keyword">SET</span> <span class="token keyword">HANDLER</span> me<span class="token token-operator punctuation">-&gt;</span>on_vehicle_created <span class="token keyword">FOR</span> <span class="token keyword">ALL</span> <span class="token keyword">INSTANCES</span><span class="token punctuation">.</span>
</code></pre>
<p>FOR ALL INSTANCES will respond to an event raised by any instance of the class, but we an target a certain instance of a class by listing its name.</p>
<p>Every object or class that defines and event has an internal table known as a handler table. All of the handler methods that are subscribed to this event are then stored in that table. When an event is raised, this table is scanned to know the locations of each subscribing handler method.</p>
<p>Visibility of events can be controlled just like anything else.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

