All right. Welcome to OCWG meeting number 11. And yeah, we can go ahead and jump in. I think Max, you had said you've been doing some work. You want to talk about the stuff you've been working on?

Yeah, I think it will be a good point in the discussion right now because I tried to summarize the design decisions we took so far and tried to figure out which are most open. And yeah, and identify two topics that we need to somehow resolve. Yeah, maybe I start with the open topics and then build up why they are open.

So the open things are like, what is the role of JSON schema for OCWG? I mean, JSON schema is nice to describe formally the structure of a document. But what we want to have is a composite structure. So we define the base structure and then we have extension points where we define how the extension works, and then applications can define how their part works. So we can only say that there are things that we don't know about and that somewhere else it needs to be described.

And to sort of validate a whole document using JSON schema, I think it's just not possible just out of the box using JSON schema because this is the use case. It's breaking what JSON schema can do. JSON schema works if you say, "Okay, here's an object, and it has some additional properties which we don't know, so we just ignore them all." That's fine, we can validate that. And then we could have a JSON schema for the sub-node and say this defines its own schema. In order to validate it, you need to actually copy all this stuff and validate it using that schema given there.

But then you are no longer validating the whole schema, the whole document. You cannot say, "Validate this given this information." We need some custom code in order to validate stuff. So, yeah. And we don't know which applications will be in the extension, so we cannot list them.

So I understand what you're saying, Max. You're saying that there's two options here, and neither one of them are very satisfying. One is that we could have a schema, a JSON schema, that defines sort of the base capabilities of the OCWG spec. But then there's these extension points. And the only thing we could do with a singular JSON schema is basically ignore all of the extensions, like not validate them. We could just say it's okay if there's stuff over here, but we can't say anything about it at all.

Yeah. One other option is to say, "Here's a list of schemas which we know, and one of them must match on the node." So then we wouldn't have to maintain a registry for all existing schemas. This is not what we want.

Gotcha. So then just to represent this other idea, you'd have the base JSON schema, and then you'd have these other JSON schemas for each one of these other extensions basically. And then you'd use the "oneOf" to include the sub-schemas and have them validate the nodes.

Gotcha. You use what to include the sub-schemas?

"OneOf." That's a keyword in JSON schema. So with a JSON schema, you can say this node needs to match "oneOf" those schemas. So it's with a capital "O" and "O minus" the keyword. And it's just "oneF," so it's "oneOf" these ones.

I got it. And yeah, I see what you're saying. So we'd have to include—and the problem is, we have two problems there then. We, in order to use sub-schemas with this option too, we would need to include all possible schemas like sub-schemas or in our schema that you would be able to look up the schema from some registry that we've maintained.

So validation of the whole document including extension out of the box is just not possible using JSON schema. It's too flexible. And JSON schema is still nice to describe structure. And then we have a little conflict between having a nice JSON syntax, very compact. I mean, we discussed what those property bags are just using property prefixes. The property prefixes are certainly harder to model in JSON schema to say everything that has this property prefix, so it matches this regular expression as these properties or belongs to this app or can be looked up in that schema. Actually, that cannot even be expressed in JSON schema.

So we could make a very boring JSON structure, very verbose, and easy to describe a JSON schema, or more compact and clever syntax that also has more shortcuts to state some other things, and then making the schema more complex. So this is a trade-off decision where we have to find a balance.

Gotcha. And was this one of the ones that you were saying that you were trying to write up the decisions we've made thus far?

Yeah, I put them in the stack repo, in the pull request, in the stack repo, in the pull request branch.

Great.

And there, in the file "decisions," not the SVG, the middle one's in the Markdown file. And this is where we made a list of these open issues, and then the design decisions we took so far, and what we did use from them, and what inspiration we took into account and everything. You can walk through this in order to enlighten ourselves.

So JSON schema, that's one thing where we have to sort of take a decision as a group. How important is JSON schema for us? Is it a nice binary user that's good as possible, or we tune the syntax so that JSON schema works better? It will not work excellent ever because of our flexibility, but we can tune it.

There is no other tool besides JSON schema to describe the structure of a JSON document. I mean, the only other option would be to say JSON is just a carrier, and JSON linked data is a message, and then we describe our structures in RDF, what structures we actually have encoded. But frankly, I think we would alienate more JSON developers because JSON-linked data and this RDF set brings a complexity that's not helpful for the goal of interchange here.

Yeah, I agree. At that point, we've gone so far afield from the obsidian JSON schema world, where there's this human-readable, not even JSON format, more like YAML, and then we've got all the needle-like RDF and JSON.

Okay, so that's for JSON schema. We keep that in our mind.

In the other issue, we just mildly related the structures. I mean, we have decided very well on resources and on nodes, and on embedding schemas and handling assets, and I think that's all quite understood. But structures, where we discussed about groups and arrows and sets, if you think more about structures, this is encoding semantics of the app. You have a group, you delete the group, all the items in the group are gone, so we want to capture that. But in some tools, if you delete the group, the items are not gone.

This is a group, and then it becomes really hard for arrows. So we have the simple case: we have an arrow, it connects two things. So in the visual part, we have a node A, we have a node B, and we have an arrow C, and then we have a structure that says actually that arrow that is depicted in C is actually starting in A and ending in B.

So what's the implication? If you delete the arrow C, then this linkage structure should probably also be deleted. If you delete the linkage structure, should the visual arrow also be deleted? We've talked about these as relations before.

Yeah, relations, sorry. That's the same.

Yeah, that's one definitely. Okay, relation, right? So these interaction semantics for the relations are tricky, and also they are not completely decoupled from the visual part, because as we saw in the arrow example, you actually could see the relation.

Then for groups, I found in the note that a typical group in PowerPoint is just a logical group, but the group in Obsidian Canvas is a spatial group. It's a rectangle, and what's inside is in the group. I found in your note, I think. So an Obsidian Canvas group resembles much more a node than a relation, somehow. And these structures are really tricky.

Maybe these relations are like special nodes. So we also have the case of invisible nodes, hidden nodes. So in some tool, you had a node that was visual. The user decided to hide it. It's still there. It still has a positional color, stroke, a freeform hand drawing, everything like a visual node, but it's hidden currently. So is it still a node, or do we have to migrate all that stuff into a relation in order to not show it because nodes are always displayed?

I think I understand the arrow one, and I have some thoughts on that one. Can you restate the second example you were saying with hidden nodes? I'm not sure that I'll follow the problem there.

Yeah, if we have a node that is hidden, which is, I think, a reasonable thing that the user can hide a node, then it's no longer visible. So how do we encode that? Currently, we should have a relation that says, "I'm pointing to only this one node in order to make it hidden," and the tool that cannot hide nodes has to show it, or we have to even pull all the data that the node had into the relation in order to hide it because the node should not be visible. So the data needs to be hidden in a relation.

So that relation you want to say... Yeah, what you're hitting on is the way that we defined nodes are the visible things on the canvas, and relations are invisible things on the canvas.

Yeah, and a visible thing that becomes an invisible thing, and so it should be represented by a relation. I don't know that... That one, to me, maybe I'm oversimplifying it, but I had never thought of that problem before, and coming to it immediately, it makes it feel like the fact that it's hidden, it isn't really a relation. It is a visual—you're basically saying, "I want this visual artifact to still be around but not appear." And that's just an implementation detail of the visual layer. It's not actually a relation at all, is mine.

I think that would be a good resolution for that special case. Yes, I agree.

Okay, and then so I have a question about these relations and structures in groups. Is there going to be a way to specify that a node is a child node of another node, or that a node is a parent node of another node? Because these parent-child relationships are very common in game engines, in GLTF, and I don't know about infinite canvas tools, but to me, parent-child relationships are very important. And I did mention before that I might want to implement this in a GLTF engine. If it didn't have parent-child relationships, that would severely limit how useful I think that would be.

Yeah, that's the perfect next point because, of course, a group in many tools—a group can contain other groups. And that's one way to encode nesting. So our current natural way to encode parent-child relationships among nodes would be to say, either we have a group that has some members, and among the members is another group containing yet another node, so that implicitly forms a tree, or we would add a new relation type, the parent-child relation, add that into the relations part. The visual nodes themselves don't know about that relation, but the relation part adds the structure there.

That would be sort of the current natural way to do it too.

And yeah, given other tools, I've seen it might feel unnatural for people to split relations and nodes. And I thought about this split. So we have resources, and we have nodes. And the split makes a lot of sense because some nodes display the same resource over and over and over again. So we have an N-to-N relationship. One resource can be displayed in a number of places.

So what kind of relationship do we have between nodes and relations? Theoretically, a large number of relations could reuse the same nodes. But if we would promote relations somehow to nodes themselves, I'm not sure that's a good idea, but let's discuss it. These relations might become simpler or feel more natural. So we could embed structural relation properties into the node and say, "Yeah, actually, now nodes can contain other nodes and can have a parent node." And then it would be more compact and also conceptually easier.

I mean, all the other tools I've browsed through during my research don't do the split. You just have a visual node, and you can say, "Actually, I have children." And then maybe if you have a group which is not visible, you say, "Okay, I'm a visual node. I have children, but actually, although I'm a visual node, I don't have a position and I don't have size." So that informs the relation what is a visual node. Then a visual node is more a node. Those children that don't have a position just inherit that position from their parents, for example.

So if we would go that route and say, "We just have nodes," then all the visual properties become like an extension part. Yeah, some of the nodes are actually visual, then they have visual properties, and some of the nodes maybe are not visual. They have no position, no dimension or something. So we would have, I don't know, node types.

I mean, in the end, it's different ways to express the same thing. If you have a node that is type visual, type structural, that's more or less like having nodes and relations in the first place, but still, it might be easier to grasp if we combine it more.

Yeah, that's interesting. I'm not sure that I'm understanding the same problem, understanding the problem's gravity in the same way. So you clearly have been digging into this for a little bit.

I think to remind all of ourselves of the design decision that got us here or the design principle that got us here was we wanted to be able to support both conceptual canvases, so things that have—where the visual representation is secondary, and the semantic relationships are primary. And so an example would be like React Flow or that kind of thing, where you have a code flow diagram where you may not manually specify the locations of the nodes, but you let that... You have sort of auto-layout engines and that kind of stuff that are based on the semantic relationships between the different tools, between the different nodes. And so we were hoping to have a concept, which we're currently calling relations, that would model the semantics without at all entangling the visual representations.

And so that was how we ended up here. It may not be a good idea, but you're pointing out some problems.

My very simple thinking about this is that relations always can optionally point to a node, or potentially based on the type of relation, it might be able to optionally point to a set of nodes. But that—to kind of say, "This semantic thing is tied to that visual thing." But that is sort of an optional pointer to further give more semantic information about the way—and I guess we'd need to get into some specific cases in order to demonstrate that.

But the way that I was thinking about it too is like groups even mean different things. They're represented differently in different canvases, right? So you pointed this out with Obsidian. I came across the same thing. Obsidian groups are more like a node. And I would actually argue that they are a node. They're not actually a relation at all.

And you might argue—you might represent them with both a group node that's Obsidian-typed and a group relation that happens to point to that, but you could get rid of one and still have the other. And then it really comes down to, like, how do we encourage implementers of this to represent—how do we help people represent their canvas in OCWG in a way that could be consistently interpretable by other people who are sort of reading the canvas, which I think is maybe where you're getting to.

Yeah, what you just mentioned, that the distinction between visual things and non-visual things is sometimes not as clear. I mean, arrows are another example, especially connectors or

 ports. Ports are also stumbled upon them. So what is a port? A port is a visual thing. It's like a corner of the rectangle. The relationship is that actually this node is always auto-computed based on that other node. And you can attach an arrow to it, which I'm listing in this other relation. We have an arrow attached to the port.

Right. It does work to split it up. 

But also, maybe it's a cumbersome split. Yeah, maybe I suggested it in the beginning. Like I said, maybe we're wrong, and it's not a good idea. But it does feel like what we will end up doing is taking—we will end up with an analog node, it's an exact analog of the relation thing, which is like a semantic node that is non-visual. And it happens to now be in the nodes array, as opposed to in the relations array. But we need the same thing.

And I'll give you another example of like—it's almost the same. There's still one difference, namely this deletion semantics. If you delete a node, it's gone. So let's say if the node has an ID and it contains members, because it's actually a group, and if you delete the node, it's gone. If you have the Obsidian Canvas node example and you delete the visual node, then the relation part still lingers around, and you need additional computation to consolidate. If this is deleted, that should be deleted. And it's this unit of having a node with all properties attached to it that's maybe the thing we can gain.

Right, I think it might—go ahead, Michael, go ahead.

You can convert from a system that has nodes inside them to the relation. Yeah, the expressivity is the same.

I have already my system as a test. And what experience have you made? Did you like it? Did it feel like a good idea or cumbersome?

Yeah, it's... there's a converter, a converter layer in between. So it feels a bit... I can show it how it looks, and that's more maybe better than just talk about it.

So while Michael's pulling that up, I do want to mention a really important difference between parent-child relationships and other relationships is that the parent-child relationship is a special case where the child nodes inherit the transform of the parent. So this isn't necessarily the case for other relationships, like with an arrow. If you just have arrows connecting nodes, then the arrow would just move as it needs to connect the nodes. But it's a parent-child relationship—it's a very direct one, the parent and the child have a transform relationship. And that is important because it affects the rendering of the scene.

Yeah, exactly. We haven't even—I don't think we're even yet... I think we have not tackled relative positioning, and we're thinking that everything will be like a global position. But that actually might—there might be some problems for that because some tools might actually only store the offsets within, like, a group or something like this.

Another consideration is the composability of open canvas documents. If you want to combine two open canvas documents into one, you probably don't want them to be overlapping each other. So you might want to give an offset. So conceptually, that is itself a parent-child relationship. So if you're going to have parent-child relationships in that case anyway, you might need this as a fundamental feature.

Yeah, I think the parent-child relationships, yes, I think we need to figure out how we're going to model those. The current plan is to use a relation that would be an edge that specifies "this child is related to this parent." And then you would model that as these two nodes have that relationship through that relation object, which to Max's point ends up being an entirely different kind of thing than a node. And does it need to be a different kind of thing? Should that just be a field on a node that allows it to point to a parent?

Yeah, but Michael, go ahead, take it away.

Yeah, in my tool, this is a node, a container node, but it has all these elements in them and connections and nodes. All these are nodes. A connection is just a node with a different node type, but these are inside this container. You can see the JSON storage for here. So these nodes... that’s this. And if I collapse all these nodes, that's everything that's in the canvas itself. And on the right side here is the OCWG representation—not the exact latest spec version, but something that I made some time ago. But the relations are in here. So this set describes this container with these child nodes, and all these nodes are in one big list together with all the other nodes.

So as a format that's used to port information from one to the other, I think this is probably fine. But I think this reads more easily. You can't see, because this is one big list, you don't know if this is a child node or an open node. You can only see that if you look it up under the relations. So if this is less human-readable, I think, then if you have a structure like this...

Yeah, but as a format that you use for sending a canvas between all the canvas applications, then of course that’s done, I think this could work. But yeah, that makes sense.

So yeah, there's a level of indirection. It's like if you want to know whether a node is part of or related to any other nodes, then you have to go look it up in relations. But again, this is only for groups, right? Like, "off" has a relationship to "toggle" inside your group, and "toggle" has a relationship to "on," and those have to be looked up as well, right?

Yeah, I think because I specified my own schema over here. So I think I also put it under the properties, I think.

Gotcha, they're part of the properties more than itself, right?

That's also what I do myself in my own format.

Interesting. Max, this is more your... I guess this is kind of making your argument here of like his instinct is to have the relationship between the nodes stored on the node itself, rather than going to create a separate edge relation to model the relationships between those things.

But yeah, I do have something that might need to be stored in relations. Let’s see if I can... This is a more complex flow, but this has hidden dependencies. Yeah, and they are computed by application, and a node determines these hidden connections by looking at, for example, this "calculate centroid"—that's a function name. So they are like computed relations.

Yeah.

But if you want to store this in OCWG format, then you might want to have those relations as well, but in the relations node.

I think my instinct here comes from working with text editor formats. So I was working with a text editing format called "standoff," which...

My instinct is to think of relations as annotations on top of the visual layer. Like there... and this is—here’s a good example of this: in an Excalidraw, there is no explicit "this node is related to this node by this arrow." When you draw an arrow, there's... they don’t have any notion of... on the actual arrow object, they don't have any notion of "from this node to this node." It just has like points where the arrow starts and ends. So they kind of, in my view, they have a deficient view of arrows on the canvas, right?

Like, that there's clearly—if I'm drawing in Excalidraw, I draw an arrow from this object to this object, I’m saying they have a relationship, and there’s some from-two relationships between these two things. Excalidraw just drops that on the floor entirely in their internal model, like they don’t have that concept.

On the other hand, TL draw does. TL draw has this rich notion of like, it goes from this node to this node. It also has some things about the computed point at which the arrow arrives into the shape, and all that kind of stuff, which is the stuff that Excalidraw has. And so in my view, TL draw is a better-annotated canvas for semantic information than Excalidraw is. But that’s going to be up to the individual implementers of the canvas—whether they think of their canvas as something that is visual, or if they think of the semantic information that's embedded in the visual, and try to represent that semantic information in some way when they're exporting it for OCWG, and then also deal with that semantic information in some way when they're importing it from OCWG.

So I think I'm still seeing the value in pushing, especially this one that you're showing right now, "K-means clustering," where you can have an arbitrary number of from-two relations between any node. That makes me want to put them somewhere else, right? Where I could even truncate all of—like, ideally, you would be able to drop the relations node, the relations array completely, and load it into a canvas, and it would appear exactly the same.

Now, it wouldn't function the same, right? If you tried to grab a group and drag that group, the group object might be completely gone—the grouping, all of those relationships are gone—but it should look exactly the same.

Max, you've been thinking about this more deeply.

Yeah, the two tricky cases are connectors and ports.

Connectors. Okay, so what is a connector? It's like, we have, let’s say, a binary connector. We have two nodes, then we have a path traveling on the canvas, reaching another connector, another node. Now, the interaction semantics are that node is moved and the path is recomputed according to some rules. Canvas tools differ quite a lot on these rules, like whether they use straight lines or these clever round lines that switch around at a certain point, and whatnot, and that use another connector point inside to define the connection behavior. Or, like in PowerPoint, where you have control points on the connector.

So how would we model control points on the connector?

You have a— I mean, those are definitely nodes, right? Like, that’s—you can see them. I don't understand how that's our relation problem. Tell me more.

Oh,

 it's more like a property of the connection itself, the connection type because... you mean...

Okay, yeah, it could be modeled as a relation. So that means if you move the nodes, you see the relation, this was actually an auto-computed connector. Now, if you can rerun the routing algorithm, and if you don't do some sensible fallback, like, let the user draw the connector again.

Shouldn't the position of the connector just be anchor points, and an anchor point being a number from zero to one, where zero is, for example, on the left side or the top side, and one is the bottom or the right, and there’s—this is a 2D coordinate, so there’s two of them. So like, zero, zero would be at the top corner.

There’s more. You don’t only have rectangles, like you can have polygons or even more complex shapes, and different tools handle connector points differently. Sometimes you can define your own connector points using sort of relative coordinates within the thing.

Yeah, now the rules definitely differ all over the place on this one.

But you don’t have to do it on the edge. You could do like 0.25, 0.25 or something.

Yeah, so this is... yeah, one way, like to draw it—it has a special control point in the middle where you can change how the arrow is bent, I think.

Michael, the middle of the arrow, make the shapes bigger, and then you'll be able to— I know what you're trying to do. The shapes have to be bigger in order to do it. Now if you have a bigger shape, now you’ll be able to drag that connection point to like any arbitrary spot.

Yeah, that’s what I was trying to do.

Again, this is what we’re talking about. It seems to me to be a purely visual thing that has nothing to do with relations. Like what you're doing right now, none of the things that you just did change the relationship from rectangle to oval. The relation object would stay the same in both cases—that never changes.

Where would I encode the information where these control points are defined? And where would I add these?

It would be encoded on the node, and Orion and I did some work on this exact problem because he was very familiar with it from... because he just witnessed Michael showing the weird way that TL Draw does this. So he was saying, “Here’s what it would look like for a TL Draw.” Basically, the TL Draw arrow needs to have some additional information in it that allows it to, when it’s pointing to an object, to be able to define exactly the XY inside of that object where it’s anchored to. 

And that algorithm, when pushed into another tool, it’s not going to look the same. Of course not, because there are too many different algorithms, clearly. There are too many different algorithms, and so we’ll—but we still need to round-trip the information that TL Draw put in, so that when we go back into TL Draw, we still have the same arrow as possible.

Yes, so these control points need to be stored in the arrow. So these are extensions of the arrow, but the arrow is a visual thing. So the TL Draw arrow has special coordinates, which are located in the nodes that are referenced to by ID. So suddenly the TL Draw arrow is referencing other nodes by ID. Isn’t that what relations are usually doing, referencing nodes by ID?

Kind of, yeah. But we never said that relations—sorry—we never said that nodes can’t reference other nodes.

Yeah, exactly.

Yeah, so I don’t have a problem with saying, “You know, this is... I’m pointing into this.” And I think the way that TL Draw does this internally, by the way, is like a relative coordinate system within that shape that it’s pointing to. So we’re going to encode, “This is the node that you're pointing to, and here’s the relative coordinate within that node,” because that’s just the way that TL Draw does this.

That’s basically what I was suggesting with the anchors. It’s just a relative coordinate system.

Yeah. And again, I think all of this is visual. You can do all of these things without representing a relation. And you can also have a relation that represents, for example, an arrow—a relationship, an edge—from square to oval, and that’s just a semantic relation that has no visual—that may not have a visual representation on the canvas. In this case, it does because it has the arrow, but that’s where I was kind of getting at with the idea of having a pointer from the relation to the visual node. Like, we could have relations have an optional pointer to nodes that says, “Here’s the node that visualizes this relation.”

Again, it feels like these semantics need to be somewhere... so Max, right, we’re thinking of like a static format. Why do you think we need to encourage implementing authors to implement specific deletion semantics? Is that why you’re hoping to think through this?

Yeah, what's happening? We have tool A exporting stuff, loading it in tool B, user interacting with tool B, adding nodes, exchanging nodes, deleting nodes. So it would be great if we would not leave like orphan data from the point of view of application A, which is quite tricky. And that's exactly what makes these relations—what makes them important to define them very precisely with regard to deletion semantics.

For example, we might end up having two kinds of groups. One is the group that deletes its members, and one is the group that will just disappear if you delete it. And then sometimes you want to express this or that, I’m not sure. But on the general discussion, whether we have nodes versus relations or merge them or not, I think it's also fine to keep them separate.

Given all the discussions we had now, we can say, yeah, there are nodes, they are meant to be visual, they can be hidden, they can refer to other nodes, so they can carry quite a lot of relational information if they need to. But we encourage tool authors to put purely structural stuff into the relations array, to try to split visual information from more structural information.

This is about an option. I mean, I think it's fine. And then this would ease using Open Canvas for non-visual tools, actually, I think, because you don't have to artificially create nodes in order to hold anything. But the distinction is not that hard, because a relation also needs to have an ID so that it can be reused in other relations. So it’s too similar for beings, but we built them for different purposes.

Yeah, I’m with you. It is a challenging divide, but yeah, this is exactly where I had written in my notes of, like, I think maintaining relations enables support for more semantic-first tools. It makes it easier on them because they're not having to deal with all these sort of visual nodes. They can just say, “Here are the semantic relationships.”

Now, whether this is a nice semantic representation or not, and whether there should be pointers to nodes and that kind of stuff, there are some open questions still.

Good stuff. Michael, when you've had a chance to review the doc, let me know. I'm also going to take a quick glance at it in the next couple of weeks. Maybe we can go ahead and get the design decisions merged in.

I think one of the ways that I've done design decision docs in the past is using... there's this format called Architectural Decision Records (ADRs) from Michael Nygaard. I think he originally pioneered it, and he kind of has a, "Here were the conditions that we... here were the goals, here were the options we considered, here were the things we chose," and then there are the implications of the choice. It’s like, “Because we chose this, the following...” And that doesn’t mean that all those implications are positive, right? It’s not about a positive or negative thing. It’s like, “We made this choice, and therefore here are the therefores.” 

But I think what you've got is plenty formal for kind of the stage of the process right now. But in the future, we could use some format like that. We could propose a design decision. Maybe we do that with relations, for example, since that seems like one of the ones that's up in the air. And then we can kind of iterate on it from there.

Maybe we can also try to reformat it to add ADR.

They can be pretty short. It’s not a bulky format at all. I think there's like three different sections.

Cool. Good stuff. We're at one minute past our normal meeting time. Does anybody else have anything to cover or discuss before we break?

I will go in the sunrise... I'll let the AI sunrise... Oh, meeting... tell me what’s wrong with this spec, AI. 

Let’s improve it!

Yeah, improve it, exactly. What are the areas where this is going to break? Read the TL Draw documents, or docs, and read the Excalidraw docs, and write me a—write me a sample file that matches the Excalidraw doc. That'll be interesting.

I’ll add it to that though. It is important for the design documents that we explicitly list compatibility goals and interoperability goals, because we want to... we don’t want to just straight-up copy one tool’s format, of course, but we want to ensure that anything we do is implementable in every tool we intend to support. So we should probably list explicitly some tools in the design document like TL Draw, Excalidraw—that we want to be compatible with those.

That’s a really good point, yeah.

That's actually a tricky thing. If we go just for the base, let’s say we are extensible, then we are a form of doing nothing. We just say we have positionable nodes that don’t do anything, can’t do anything, that’s it. Or we add more features from other tools so that they are no longer extensions but core, then we need to define explicitly what they mean. And where do we end? This is actually not so easy.

It’s not trivial, but at the same time, I think there’s sort of the leading whiteboard tools that we all kind of know. I think we could pretty quickly get to a set that we're like, "Let’s at least have these in core. Maybe we add new things in core later, but just having shapes and arrows and text is probably good enough to get started." And then you kind of... then we have, to your point, then an OCWG

 file is something, right? It’s not just nodes that are positionable, but you at least have a few things that you can build up.

I would also argue that images should be in the base spec too because images seem pretty fundamental.

I can give you... And it's also good to note that there's plenty of things that we can think of that are pretty much a solved problem by now, but we don’t want to have them in the base spec. For example, physics. If we want to have objects in your canvas moving around and bouncing around and stuff, that's really cool, but that should definitely be an extension because there are a lot of open canvas tools where that's not a feature at all.

That’s, by the way, one of the extensions that I could build because I’ve been working on that in the GLTF side, so I could pretty much just copy-paste it and change it around to work with canvas elements.

That would be really neat. There are several people—Orion Read and others in the sort of open canvas, or the infinite canvas space—that have done a lot of physics-on-a-canvas work. There’s some fun stuff. People like building sand simulators and that kind of thing, falling sand simulators, inside of a canvas, and pretty wild.

That’s awesome, Aaron. Maybe this year at 21 Days of Code during December, you can work on a thing.

Good stuff. All right, guys, until next time. We’ll be following up after this.

Yep!