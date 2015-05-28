---
title: 'Property Change Listeners : Adding and Removing'
author: ajordens
layout: post
permalink: /2007/05/property-change-listeners-adding-and-removing/
categories:
  - General Discussions
---
Quick lesson learned.

If you have a property change listener registered against a specific property name, **you have to use** *removePropertyChangeListener(String, PropertyChangeListener)* **and not** *removePropertyChangeListener(PropertyChangeListener)* when you want to remove it.

Basically, you cannot do the following:

> <pre>PropertyChangeListener foo = new XXX();
<br />public void enable()
<br />{<br />    addPropertyChangeListener("SomeMessage", foo);
<br />}
<br />public void disable()
<br />{
    removePropertyChangeListener(foo);
<br />}
</pre>

Truth be told it&#8217;s rather innocent looking code but I did spend a good day tracking it down through some fairly nasty table and panel hierarchies. The kicker is that by not actually removing the property change listener, you ended up queuing many copies of the *exact* same listener (basically enable() / disable() were called repeatedly based on the state of the UI).

To make a bad situation worse, have the listener make a server call. It&#8217;s not too bad when there&#8217;s only one registered, multiple that by 300 and you&#8217;ve got issues.