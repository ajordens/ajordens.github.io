---
title: ValueIsAdjusting Is Your Friend
author: ajordens
layout: post
permalink: /2007/08/valueisadjusting-is-your-friend/
categories:
  - General Discussions
---
Funny story, and a lesson on something to watch out for when dealing with Swing tables and event listeners.

**Scenario:**

Given a JTable, suppose you want to add some functionality to select all the wells on the table. Of course, it&#8217;s not just as simple as selecting every well, you only want to select the wells that have *contents*.

**Pseudo code:**

> setSelectedWells(table, wells)
> 
> {
> 
> table.clearPreviousSelection()
> 
> for well in wells:
> 
> table.selectCell(pair.x, pair.y)
> 
> }

Pretty simple right? Swing complicates the matter a bit further with column and row selection models so the equivalent of table.selectCell() actually involves the setting of selectionIntervals on the underlying row and column *ListSelectionModels*. 

If you&#8217;ve worked much with Swing components, you&#8217;ve no doubt realized that it&#8217;s very easy to perform operations that generate significant #&#8217;s of events. Not a slight on Swing, it&#8217;s a powerful (and fairly complex) GUI toolkit and it&#8217;s important to understand it&#8217;s eventing framework whenever you&#8217;re writing non-trivial pieces of code.

The above example is no different, as your changing selection intervals on the row and column *ListSelectionModels* you&#8217;re going to be generating a change event. If you&#8217;re doing this in a loop, you&#8217;re going to be generating multiple events per iteration (one for row, one for column). However, you still won&#8217;t see a problem until you have a handler tied to those selection events. Suppose your handler performs a quick(?) operation that takes a tenth of a second. Regardless of whether or not the business logic is backgrounded or executes on the EDT, you&#8217;re going to see a significant slowdown with any significantly sized table. Take a table w/ 384 possible placement locations, depending on the implementation you *could* theoretically have 384*2 event notifications generated (again, one for row and one for column). If the response to each of those notifications took a tenth of a second, you have what aggregates to a 77s operation. 

To cut to the chase, Swing allows you to treat a situation like this (changing selections on a per iteration basis) as a single batch through the ListSelectionModel&#8217;s ***ValueIsAdjusting*** flag. What this flag essentially does is provide a hint to the handler/listener that the source of the event is still adjusting. If a source value is still adjusting, chances are that a response is not necessary until it&#8217;s reached a final state. This is fairly typical of a drag operation, where you&#8217;d want to respond when the user finishes their drag operation, not after each element is selected. Using the *valueIsAdjusting* flag is easy, simply set it to true before prior to your selection event generating logic, and to false when your done (or better yet, store the current state of *valueIsAdjusting* before and restore it after). Whenever valueIsAdjusting changes (true -> false or vice-versa) an event will be generated, so you don&#8217;t even have to do anything else.

Just making this change in the system I&#8217;ve been working on turned a 100s operation into a .2s operation. The **funny part** was that this seldom used operation (*wonder why it was seldom used?*) had actually been in the system for years. 

As the community moves towards more consistency in our usage of Swing (motivated by the availability of frameworks like the *Swing Application Framework*), one hopes that the learning curve diminishes and application developers are able to focus more on their writing of domain-specific code and less on the intricacies of the UI underpinnings.