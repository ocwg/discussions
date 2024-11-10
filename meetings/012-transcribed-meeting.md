Sure, here's the transcript broken into paragraphs:

---

So just for the sake of the recording, we're going to start talking about the different types of relations to make sure that we have an adequate representation of the ways that relations might be used. So that's where we're at in the meeting. Really haven't discussed a whole lot beyond that. All right. Here we go.

I get an excellent. So yes, sets, you asked, can edges— you mentioned edges directed in this? We had initially kind of said that edges were from and to. And therefore, if you wanted to represent sort of a two-way, there's no undirected edge the way that we have specified here.

Yeah, but that's pretty common to have undirected edges and just pointing in one direction and even edges pointing in both directions. But if we talk not from the arrow view, just from the logical view, yeah, directed to undirected still—is this a semantic thing? Are these two things somehow just connected? Or is there some kind of flow implied?

So would we want to change this so that it seems like this is overly specific, then this edge is defined as if it is a directed edge? So it sounds like we change this to be—these are the two nodes that are connected. And then you can further specify that it might be from one to another, or it might be bidirectional or just undirected.

But do we really need a bidirectional edge? Isn't that the same as an undirected edge from this relation standpoint? Could be. Yeah. Yeah, that seems the same to me. OK.

So we could just add a Boolean directed, yes or no, and default is yes. Or no, well, then we still need to know which edge is the from and which is the to. Why not if we call it from and to? OK, so this is from and to, and it's just undirected. Yeah, directed is false and still from and to.

I mean, it's technically great if they still have a technical direction, although it's not meant to be a logical direction, but you can still use it for sorting edges. That's a good point. And then also if you have a...

Yeah, in other words, the two ends of the edge are logically distinct from one another using these labels from and to, which could be a helpful distinction down the road, especially in cases like if you think about how arrows work when you have an undirected line, then you have those two—you can set what the endpoint looks like for either end, but you need to know which one is which.

Yeah, I mean, to be able to distinguish between the two ends, so to speak. And another nice question is what exactly is the edge pointing to? So if it's pointing to another node, may it also point to another relation? 

Yeah, we did say that. We said this somewhere that edges can point to nodes or relations. Yeah, here it is. The from and to it contains. Yeah, from and to can be nodes or relations there.

OK, OK, OK, and we have a Boolean. Directed or not, but also common is some kind of weight on the address, which could be a double, also optional, and a label is also something. But we could also leave out the label and say that's too visual. That belongs to the arrow.

But then I would say a type on the edge is crucial to bring over the RDF land. OK, so the type makes more sense to me than a label. Yeah, I agree. And the type needs to...

Yeah, what is the type? RDF uses a URI, which is the ID system for RDF. So here it... so this would allow us to represent your RDF, but if we want to represent an edge type as another relation to carrying more metadata, then we need a new relation type, namely the edge type relation.

Which? Yeah. I don't know that I follow that 100%, and that might be something I need help with. I'm not sure. OK, let's say we have some people and they work at companies. So we have a relation and we now represent the things visually and the relation.

So we have John works at Microsoft and Jazz works at Apple. And now this "works" is something that is reused. So both relations just say that's the works relation. And now we want a central place where we sort of describe the type "works," where we say "works" is actually always a directed relation.

And you always work at a company, and what's working there is people or robots. All this metadata belonging to the works relation needs to be attached to the work relation somehow. And in order to attach stuff to things, we need to represent them as relations in our model. It's not visual, so it's not a visual node. So it's a spectral relation.

So we need... 

I think I've got you. OK, so the schema here would be relation, and we might have... maybe it has a type too. Well, wouldn't the type—wait, wouldn’t the type? Yeah, the idea and the type is then synonymous. So the type... this might be the label of the type, actually.

So the type is just a relation one, two, three, or any ID. We don't care about how to represent this type in a visual editor. You would say "works" or "works" in more German, "arbeitet bei" if you have multilingual labels. 

So... yeah, and we allow extensions to add more properties, of course, right. But to make this all work, we need to verify the relation type as being more than just a simple string.

Now, so if we have Jazz, Apple, type "works," then here we would need to say ID is "works" so that the two things are connected, that we know that. So we have—you have the actual relation, Jazz working at Apple. 

Yeah, and then you have something representing the "works" itself. 

Yeah, this is so... I'm trying to make a... 

And yeah, this is the data node. OK, so we now we just need to resolve the ID clash now. So the Jazz works at Apple has a relation ID one, two, three, four. And now here we need a different ID. 

Oh, I have a relation one, two, three, four. Sorry. OK, OK, got it. Sorry. 

Yeah, that's... or you could, you could even do it this way, like edge relation, just to make it more clear, metadata. This is the metadata. 

Or you just call it "works," if you want to, or relation—I mean, any ID. And then it doesn't matter as long as it's not the same. And then this ID should be used in the type field of the other relation. That's the link. 

Oh, you would go this direction. 

Yeah, yeah, this is how RDF people would do it because now stuff is... 

Maybe this could describe lots of different edges. So this is... yeah, and then you sort of have like the... it's like with class and instance, you have the general class of these relations, these working relations.

It's always people working at companies. And then you have the concrete relation, this Jazz working at this Apple company. 

And right, with some of the example of like, you know, started at or whatever, and some, you know, some date and...




No, this would go on the other direction because Jazz started working at Apple here. We just state that "started at" has a type of data, but we wouldn't give the date here because we would use the exact same metadata blob for Joe working at Microsoft. It's the same.

Got it, so the important part is that this is a "works." Yeah, it could be a critical thing. Maybe not call it "type" here, just "label," because we already said that this is the type of relation by using the ID on the other edge.

Got it. OK. OK, this is starting to make sense. Name is also... yeah, I think "name" is probably not a thing. That should be probably down in the properties array if we have one or the properties bag. 

So then here, we would use our, like, extension, property extension type thing, and maybe state the time from and to if we need to, right, or whatever. Yeah. 

If we wanted to have "started at" and "ended at," or, yeah, depending on the mechanism we use for property bags, which we have, right? Right. But however we’re doing that, then this could be like a custom slash. 

But isn't this custom slash works like the same as this? Like, aren’t the properties on this governed by this, kind of like they're related in some way? Like, this property of "started at?" 

Yes. But what if we have a custom color? You know, color doesn’t make sense... OK, structural... Yeah. I don’t know an example where we need a custom schema property bag on the edge itself that’s not governed by the edge type.

Mm-hmm. Yeah, it feels like the edge type is going to be... yeah. So in some ways, the schema here is custom slash works. But to your point, we’re going to want... goodness. So this feels like this needs to be the same as this, because you’re not—the label isn’t a lot. It isn’t a... it’s a logical label, not a... view... yeah, not this. 

Yeah, it "works"—that could, that would be on the arrow. That wouldn’t be described on the edge. This would be on the arrow node, just to be really clear. 

These two things are related. If I’m understanding you correctly, I’m sure about the schema link, but I’m sure we need labels because labels are really, really great for debugging. 

Mm-hmm. And, well, it feels like what you’re saying is that the edge... we need... OK, second... the edge relation might have custom properties on it that would be based on the type of relation it is, but that’s the part that I’m still not clear on. What this is... you would state, for example, that the "to" of the edges is always of type "company." That’s something on the edge. 

Yeah. You would say it's always a company. Works for... it's always a company. So if you do data input for RDF inference, you could deduce that Apple must be a company. 

Mm-hmm. Yeah. Semantic web people love that. Got it. And if you just import semantic web data, you want to represent it on the relation side. And in order to be able to do that, you need to represent the relation type and stuff like domain and range, they call it from the function.

And then also why I’m just not sure why it has to be a separate thing. Like, can't that, doesn’t this say things? Doesn’t this do exactly the same thing by saying this prop, this relation has the type "ocwg edge" and also has the type "custom works," and it has the properties, right? 

I don’t know. I don’t understand why it has to be a separate thing. Yeah, so maybe we could put all this metadata for the edge type here in the schema. 

Yeah. That feels like a more natural way based on what we’ve done with other...

Yeah, I agree. I agree. OK. So here, just as like... we thought about this and just cross it out for now. So the type we have up there would not link to an edge relation. 

But to a schema, well, it doesn’t link to anything. We’re basically saying, if you want to specify the type, this would be—I think this is how we would be communicating it—if you want to specify the type of a relation between two objects, then you add an additional schema to that edge’s schemas. And so it can have more than one type, it doesn’t have to have just one, which is... yeah, that’s one of the nice things about it maybe. 

And you know that for schemas of "at custom works," the "from" is always a person, like you said, the "to" is always a company. You could even filter or search the entire set of relations to find all of the relations that have the type "custom works." And from there, find out what all the companies are by aggregating all of the "to" nodes. 

Yeah. Yeah, I agree. Yeah, this feels good. 

Oh, so it’s... yeah, it fits nicely to the... yeah, it feels very analogous for their other schema extension stuff that we still have to figure out exactly how it works. But assuming we can do it over there, we can do it here too. 

Yeah, it's cool. Ready, that makes a lot of sense actually. Right.

And then back over to the document, the spec. So if we talked about directed and undirected edges, talked about being able to specify the type of a relation, I’m going to leave hyper edges alone for a minute and let’s go back to sets.



Question about edges? Yeah. Go for it. Yeah, please.

What about ports? So, if an edge connects to a specific port on a node, this example... the nodes don’t have ports. So it depends—either edges cannot connect to ports because edges are logical and ports are visual, or ports are, let’s say, ports are visual nodes. So we have two blocks, A and B, and both have a port, south and east. And now our edge simply goes from this port ID to this port ID. 

So the edge itself doesn’t really change at all. It just goes from a visual node to a visual node. And we have two additional relations relating the mother node with a port node.

No, exactly, like a set, probably the parent node and the child node. But there may be even a special port relation that explicitly states this is linking a normal node to a port because it’s such a common pattern. And if we can explain it, it’s easier to reuse it.

I mean, this is a very, very good example for all these kinds of edge cases. We can just say here, use a normal edge, relate your object with your port, or we could provide some built-in support for ports.

Help me understand the conceptual ports part. I don’t know that I followed the... I understand the visual ports, which would just be use, use arrow and like, or have like a version of arrow that has those properties supported or exposed.

We could, so if we have two nodes, for example, we have two big nodes and they have a port. We could just say our relation is just relating the big nodes. It’s just not even talking about ports.

Exactly. Or we could say they do relate from port to port, and then we have another relation relating the ports to the nodes. And if you really want to know which big node is logically connected to another big node, then you need to understand ports and edges so that you can actually follow all the logical links, all the valid, and now you need some ports.

Yep. I’m going to add something important here. There we are, one of the simplest examples that I can think of is in visual programming. If you have a node that sums two numbers, you have two input ports, A and B.

Mm-hmm. OK, so then conceptually, I think what you were saying is this would have a... you could just draw either one edge connecting big node one to big node two or an edge connecting the big node one to the port of big node one, another edge connecting that port to the other port, and a third edge connecting again.

Yeah, I’m super saying. So this would be like our relation between the two. So these two nodes are connected with one another, but they’re also another relation would be, let’s see, these two ports are connected to one another, use the word well so it’s short, but also this port is connected to this...

I see. I see. Yeah, it’s a lot, a lot you have to do for that pattern if it turns out to be pretty. Both have pros and cons.

Yeah. So, relation obviously, if we can somehow make the ports relation explicit, then another tool has a chance to understand it and correctly route arrows if things change. So understanding ports is kind of nice.

Yeah. No, I see what you’re saying. So what is a port for us? Obviously, you have two visual things, the big node and the port node. And now we are free how we model the relation. We could just give the big node a ports array. Then we also have captured the relation from the big node to its ports. So make it a first-class citizen in the visual world or move it into the purely relational world, and it’s both a spell—it. We just need to feel what’s better, and I don’t know.

That’s a really good question. I mean, here’s the advantage of the second. There is a slight difference. There is a slight difference, and it’s this.

If we had a... well, I’ll just use this one. Let’s call this a port relation real quick. We’ll say that this is... we’re defining... goodness. Sorry, this thing going crazy here. By the way, well, that’s fine too.

So this little port is defined, the relationship between these, this big node and so from big node one to... we’ll call this port one even though we don’t have a number for it or anything. It’s not directed. Well, I mean, I don’t know. I don’t know if it’s directed or not to think about it. If we could, let’s say, it has like a schema of OCWG/port, then you could...

Oh, oh, actually maybe... well, the port is a visual node for sure because it has a position that is rendered in some way. So there’s a place to...

Yes, I’m leaving that alone for a second and I’m trying to deal with just the conceptual for a second because I think what Michael said was really interesting. You could actually have a schema for a... conceptually, this is a React Flow/addition port, which is like the schema for it, and you could, but you could also add that on the port node itself.

Right here, right now, you are... no, I mean, on the... right now, you’re editing the port relation. Right? 

Yes. Yes. But the port itself, the port is a visual node, and the visual node has property bags and can be extended with custom schemas. So data about the port should maybe be stored on the port. Data about the relation between the port and the big node maybe goes where you are right now.

I mean, I would defer to Michael and other people who are working on this kind of tool because this feels... the fact that this port deals with addition feels like something concerning logical and not visual. It feels like something that should be represented by a relation and not in the visual world, but I defer.

Yeah. And how I think of it, the port is also visual but also a conceptual thing. But just in the case of that addition example, the port is just something that has a name, which receives a value, and another port receives a different value. The big node, which is the addition, gets its values from the ports and the edges, which connect it from other nodes, which have some value in them and send them to ports there that are relations between the nodes and the ports.

Mm-hmm. The ports themselves probably don’t have a lot in them, but I think they could be relations.

I think I understand what you’re saying. You’re saying that this thing is the thing that does addition. 

Yeah. 

And the port is just... it’s like input/output. 

Yeah. 

And is that what it is? 

Yeah. You can have two inputs, for example, two input ports, one output port. And that really depends on... if I speak for my own tooling, it really depends on what the node does. You can also have one input port, which has two output ports.

For example, if you have a node that performs a map on an array, then the input port receives an input value of type array, but there are two output ports. One of them is the map function that does the mapping in the array, and the other is the output with the result.

So how are you currently—how would you want to represent addition? Would you want to split—would you want the node... So you have an addition node that's an actual node.

Yeah. That node.

Yeah. An arbitrary set of input and output ports, and it sounds like... 

Yeah, go ahead. That might... 

Let’s start with the base case. We have a big node, which represents addition, ignoring ports for a second. So we have a big visual node, and we have some structural data about it. This is representing addition. So we said in the beginning, we are not splitting visual nodes and relations, very clearly, just fields, right. And we have definitely a visual node.

So it seems to me it makes the most sense to just store the additional metadata that this is actually doing addition in a property in that visual node, just to not have to deal with more IDs and linking and stuff. We have one thing, and it’s representing a circle and it’s representing addition. If it’s deleted, both things are gone, and they belong together. So it makes sense to just use one object.

Yeah, I think you’re right. And if that is right, then if we have ports, then it makes the most sense to put stuff in the port nodes instead of in some relation. And only put things in the relations in a very indirect way, if that’s really helpful or really between these two things.

Yeah, it feels like there would be something here. And you’re making the point that a port is like an additional node, visual node as well, that people have to know.

Yeah, the port is rendered visually, so it’s an official node. So then it might have one, two, three, four... sorry, a port. So there’s... there. This guy has one... yeah, you see what I’m saying? So like this points to that, and the other way around, sorry. And this points to that.

OK. Now I would again ask Michael, can a port be both the addition port for one node and at the same time be the subtraction port or output port for another node? Because if a port is always just either input or output, and that’s it, then we can just put that information into the port and relate the mother node and the port node in a generic way that’s not specific to code flow apps because ports are such a universal concept.

Yeah, in my case, they are not reusable. They are the ports, but...

They’re not visual, you said?

No, they are visual, but they are not reusable. They are connected to the nodes themselves.

Got it. Yeah. I mean, like you have it here, if you select the circle or you get a blue line and the markers, they clearly belong to only one object. Ports are not shared among nodes, and that’s a very common semantics of ports, which we can sort of capture once and for all and say, visual nodes can have ports. Period.

I like that.

And here’s... 

We don’t have to deal with the accidental cascading delete type stuff of like, oh, well, if you delete this, you should really do that too.

No, we still have that. We can’t get rid of that because each port has its own visual representation, which we can’t do layout. So we need to have a circle as one visual node and the small port thing as another visual node. The only thing where we are still free to remodel is where do we store it in relation, that that port belongs to that node.

Right. This thing. How do we do this piece? What’s your thought?

We could just have an array on the big node listing the IDs of its ports. That would make the easiest way to delete stuff and so on.

Gotcha. So an array up here. In the addition node.

Yeah, exactly.

Yeah.

We already have it, exactly. So in the addition node, input ports and output ports, generically, and not in React Flow schema but in the general schema. So the OCWG ports extension allows you to put ports.

I’ve got you. OK. So it looks like this. Now you’re saying we’ve added ports to this shape using this internal...

Yeah, any shape can have ports. So here are the IDs of the ports, and you already know how to render visual nodes. They can have any funny size, shape, whatever you need.

But we’ve captured it. We know what the ports are. And that’s a reusable functionality defined in OCWG.

Exactly. Just ports.

Not input and output.

Yeah, just ports. It can be specified in the nodes.

Oh, I see. Yeah, exactly, because it’s possible that you could have a port that’s not an input or output port because that doesn’t make sense. So this would need to be something like a schema at React Flow/addition or whatever that specifies this is an input port.

Exactly.

This is probably more like this.

Yeah, yeah. Actually typing is adding a schema.

That’s cool. And then there may or may not be—you could have, you know, things like if there were...

OK, that makes a lot of sense.

Yeah, OK. That feels good. So then in this case, this is an addition node, but we don’t need to specify the ports here. We have a... we now have lifted that functionality up into an official OCWG extension. And then the schema can take advantage of that. The fact that this is an addition node, it can go look up the ports that it has and then find out which ones are input and which ones are output.

Exactly.

Yeah, that’s cool.

Well, I’m glad you brought up the ports thing. It feels a lot better than this, where we would have like four relations just to model a simple two shapes with two ports each.

Yeah, and tracking down all these relations would be... OK, then in the case where, if we go back to this case, then we no longer need the port relation. We no longer need that port relation. 

What relations do we need in big...

We still need two of the edges.

Yeah.

I think you’re right.

Depending on the use case, we need left or right side.

Yeah. And then what should this port—I can picture in my mind what big node one related to big node two looks like. What is the relationship between these two guys look like?

So it goes from port one to port two. And that’s it. It’s undirected and it doesn’t have anything else. That’s it.

Well, if it’s part of a code flow editor and the output that one node computed is actually routed to the input of the next node, then maybe there is another schema attached to it stating that.

They could certainly do that. But in terms of minimal behavior, this captures the addition nature of the node, like Michael was saying. This is just saying the ports, and then the ports and the shapes are already related down here. So we don’t need... this relation is only saying when big node one and big node two are connected to each other, that connection is taking place through these two ports.

That’s interesting.

Yeah. And whether that’s actually helpful in the context of an application or not, it’s not so clear.

Oh, this is good because I was thinking about the arrow as well. The other piece you would need here is an arrow node.

Yeah, true.

And the arrow node can take advantage of the fact that there are ports here, or it’s from and to here, which is really helpful. Having those as separate nodes makes the layout for the arrow node much simpler.

What I do myself in this case is the edge—my edge has links to the nodes but has a separate property specifying the port names that are connected. So you more or less have both.

So the edge is attached to this node and this port.

Yeah. It’s double... it’s quite common modeling and helpful, but it has some redundancy.

Yeah, it’s not bad. We don’t disallow that. We just created a shorthand version that allows you to get away with less if you'd like.

The other thing is all of this works even if a purely visual tool leaves off all the relations. One of my concerns is that I think a lot of purely visual tools don’t have a rich internal semantic or taxonomy, and so when they export, they’re going to export things that just have to do with visual representation and won’t represent the underlying semantic relationships. So relations might be empty, other than things like groups needed for visual type stuff.

OK, these are great points.

Cool, we’ve got a few minutes left. The one thing we didn’t talk through is around sets, groups, frames, and many other things. Sets are simpler because they’re literally just a list of nodes that can then be extended. You can have... we can extend using our property bag extension or schema extension capability to represent logical relationships, including groups, frames, hidden groups, visualized groups.

And a set can already contain, as a member, another node or another relation. It can already recurse and form a tree.

That’s exactly right.

And the extension could define whether you actually inherit properties to your members or not. That was a case Jane brought up.

Yep. And hyper edges—I’ll leave that to Orion to figure out since it’s one of his favorites.

That is one of my favorites. I love hyper edges, but there’s no mathematical consensus on how to model them, and that’s definitely one of the challenges.

That’s the whole point of the standards. We don’t need consensus among the entire mathematical community, just our internal consensus.

Well, this is great, guys. I don’t... three minutes left. Anything last minute we want to talk about? 

I think I’m going to see if I can

 get some time with Orion, probably early December is my guess for when I’ll be able to get together with him. We’ll be working on... ideally, we could spend time on some implementation stuff. 

Max, you mentioned maybe taking a crack at collating all this information into one place to get feedback on?

Yeah, that’d be great.

The existing design decisions document is a good start and could be turned into a more spec-like document.

I noticed with the design decisions document, which is right, that it’s headed toward replacing the current spec document. They’re not connected yet, but coming from the top side, then deciding how we do this in JSON—what it looks like—because initially, we just decided what we were representing at all. The drawings in Terdraw were not JSON-focused initially; they were for deciding what belongs to what.

It can connect in the end. I can copy stuff from the existing spec into one big document.

Great. That makes me think it would be nice to have visuals since we’re describing a visual canvas. It would be nice to have JSON with a snippet of a visual showing what it looks like.

What I love to do is generate a diagram from code and use PlantUML. It’s a nice toolkit for small graphs.

And it works for me. They work fine.

What was the language again?

PlantUML.

Is that supported on GitHub, or is only Mermaid supported natively?

Only Mermaid is supported natively, but PlantUML is a richer system. 

OK, so if you’re contributing, you pick.

I write in AsciiDoc mostly, but if I do that, I write alone, so I might stick to Markdown.

I started with AsciiDoc, too, but now I’m converted to Markdown.

AsciiDoc is nice, but have you tried Typst?

Yes, that’s an interesting new typesetting system. 

I read a post about the developer behind it—it’s wild!

OK, that’s time. I’ll see you all next week!

Great, see you all.

Bye!

Bye! 

Bye, everyone!

