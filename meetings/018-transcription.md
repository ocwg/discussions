 Here's the transcript with paragraph breaks based on changes in speakers and topics:

---

This is OCWG meeting, I think, 18 and, yeah, we're cranking on the spec and writing examples for the spec and we're just having a discussion about using the spec with an LLM to have it generate examples of OCIF files. So, yeah, we'll probably be continuing on that, but Max was about to propose something that we discussed today. So, go ahead, man.

Yeah, so, last time we discussed two weeks, two times ago, we discussed about transclusion and then I was about adding it to the spec and then I realized where to sync, we have a relation for parent-child relations and that's about inheriting stuff. So, you can inherit properties, but you can also inherit resources. 

So, I realized we have transclusion already built in and we thought already about every aspect about it, it works, so instead of adding anything to the spec, I started a new document called the cookbook. The cookbook explains how to use it because there is nothing missing from the spec to do transclusion, it was just hidden there already, so that was really nice. So, we have a cookbook now and that helps to use the spec and maybe it helps LLMs too.

And then I really, or I'm curious, is it still in the 03 draft branch? Great, check that out. And then I realized the case, so we have a, we just added an oval type and we really enjoyed ourselves, yeah, that's a nice type, and then by conclusion, if you can have a rectangle note, showing an image, so the image is shown with a rectangle, nice, so what if you do an oval note and show an image, logically you probably have the image cropped in an oval shape, then I'm like, okay, effectively we are doing some kind of resource composition here, using a single visual note that by chance has on one layer as it's built-in contact the oval and as it's linked resource the image, and only because of this circumstance they can be combined, that doesn't feel right.

So, I think what the oval really might be is a note showing an SVG resource that contains an oval. Maybe we shouldn't have any other type on the visual note except a rectangle and everything else is showing a resource, like text note is a note showing a resource. So why is an oval suddenly not showing a resource, why is that suddenly built in?

If we cannot argue that then, yeah, it's weird, you're right, I think. Okay, so a couple things we talked about that are related to this, we talked about rectangle type, and then we talked about their sort of primitive shapes which we decided was one arbitrarily, and we decided there were complex shapes that we would represent with an SVG path, and that would have a resource of an SVG path that we could be arbitrary, you know, in complexity.

Almost, we decided to have a path as an SVG, but we decided not to use SVG as it is, we defined a path object, but maybe we should have used SVG or maybe we should define our own resource types instead. Why not have an oval resource type, which is simpler than SVG? The oval resource just has width and height and a stroke or something like that, and it can be rendered using SVG, but it's conceptually simpler than SVG itself, maybe. 

But why it should belong to the resource layer somehow and not to the note layer? Because it's so... Right, I think. So here's my argument from first principles, hopefully, and this might not be convincing, but if I had to steelman the case for an oval, it would be that there are certain shapes which conceptually are very common in whiteboarding examples and usually have some meaning in the actual whiteboarding app itself, and we want to make it trivial to represent those shapes in a very simple fashion without the indirection of the resource, so that would be defining whatever the platonic shapes are, rectangle, circle, yeah.

So we could decide whether triangle and other things make it, which are the favored polygons that we'd bless. But yeah, just if you open any whiteboard, many whiteboard apps, you're going to have a circle, square, that kind of stuff. And so if we're going to move all that to the resource, it feels like it makes the spec more complicated as opposed to less.

Like I'd rather be able to easily specify a circle and not have to point at a resource. And then the case that you mentioned of having an oval type that also has an image associated with it, I'm trying to think of a real-world case where that happens in a canvas today. You mentioned the one case where, like in Keynote, for example, where you can mask an image with an oval.

Well, if our oval is a visual note, then the spec doesn't forbid to use an oval on the note and an image as the resource, so then we need to describe what should happen. Well, I think this is we're getting to a principle here, potentially, which is just because something can be expressed in the spec doesn't mean that it has to have meaning. 

Like the spec doesn't have to forbid all things that don't have meaning. It can explicitly say we don't know what this means, that's fine. That would be my, if you combine one of our platonic polygons with an image, I'd say it's up to the reader to interpret what that means, how do you know what we're planning to do.

I don't have a big issue with that, but this selection of polygons that are not resources but belong to the note itself, I don't know, it feels weird, it doesn't convince me well.




Well, so now we have my opinion on the call. Now I feel like we're conflating, and I would love to hear Michael and Orion's thoughts. It feels like we're maybe conflating extensions and resources now at this point. Like an oval doesn't have to have a resource because it has a primitive—we have a primitive understanding of what an oval is. And the same goes for rectangles and potentially other polygons that we add.

Yeah, but if we go back to like the metaphor we have, the canvas is a two-dimensional plane having rectangles showing resources. So every text block we have, it's like a div—a visual note is really like a div for HTML. Every little block is showing something. 

So if we have a "Hello World," then there's a little block, it has a position, it has a size, and it's showing the "Hello World" resource. And there's another one, it shows an image. And then there's another one that shows an oval. Why is this oval suddenly built in on the top layer and not showing a resource? But the image one and the text one are showing resources. Why does this make sense?

What is the resource that the oval is showing? It could either be a very small SVG file or it could be a new kind of resource—the oval resource type. We can define our own types to make it simpler to express simple geometric stuff.

I would be okay with the second and not the first. And the reason for that is, I feel like if you express it with an SVG, one, you have to have the content of the SVG in order to, like, the path of the SVG in order to... And the other—yeah, the real reason is I want to represent polygons conceptually so that each of the different implementing canvases can say, "This is an oval on the canvas at this location, it's this size." And that can visually be represented very differently in another canvas, but they're still the same oval in the same location on the canvas.

Whereas an SVG feels like it's more about the visual representation rather than the abstract notion of... 

I agree with that sentiment. Yeah, we could define our own JSON type to carry the data for an oval, and for a polygon, for a star, whatever you need, and just represent it in JSON to carry the minimal data and mint new data types for that.

Yeah, I think it depends on where we put it. Yeah, we're probably at the point where we want to look at the syntax and compare the options, but Michael or Orion, do you guys have any thoughts before we jump into some syntax?

For me, the most natural sounds like having rect, oval, circle, polygon as part of the notes on the top level, and images, text as resources.

Yeah, for some reason, there seems like an arbitrary divide to me too, that it's like, it's hypermedia. It's no longer like a base node; assets or resources represent hypermedia in some ways. You can imagine that if you have the oval as a resource, could that resource also have an image attached, which is also a resource? Or text? It could get quite complex.

Good point, good point. 

Yeah, for that, you would need composition, right? So you have multiple visual nodes.

Yeah, and the way we currently structured it, I think the composition part is more on the top level—the node level with extensions and resources linked.

I think I'm also inclined towards having the basic shapes be top level, even though it is definitely arbitrary where you kind of... you know, how do you choose your built-in, fancy primitives and so on? I think that has some advantages when it comes to tying different kinds of geometry to different semantics, as opposed to having those as resources.

Yeah, also compactness.

So, okay, so these are the visual node shapes. You can ask, like, if you want additional shapes, right, you can write an extension.

Yeah.

Yeah. And you—yeah, I think now we're pushing in the direction of making this accessible for more... What did we call them? Conceptual canvases versus visual canvases? 

I think this decision is either going to skew us towards visual canvases, or giving more functionality to canvases that are purely conceptual or mostly conceptual.

Well, if this is happening on the visual notes only, a purely conceptual canvas will just not use it.

Clearly, conceptual canvases will still have nodes. What they may not have is—they won't have as strong of an idea—they'll have nodes and relationships between nodes. They just won't have as strong of an idea of position. 

Like, all the conceptual canvases I've used have automatic positioning algorithms. It's not that they don't have position—they do. But position isn't something that I, as the user of the canvas, am dragging things around necessarily. I'm allowing an auto-layout—like, GraphViz, for example. I can choose from multiple different algorithms to auto-layout my nodes.

Yeah, okay, agree.

Then one minor thing—if we do have, as we just decided, a visual palette of geometric shapes that, in addition, can also render resources—what is the Z-ordering of these two? Like, is the oval or the rect always on top of the resource?

That seems to make sense—that maybe it should be specified.

Yeah.

Or does it represent a frame out of which, like, whatever is out of frame isn't visible?

Yeah, I'm almost inclined to leave this to the implementer and say, "We recommend X." Well, I mean, we always have to say that we recommend X, but we don't have to make a recommendation here.

Do we have Z-index on the asset—sorry, the resource?

We did. So, the visual note has a Z-index, and the visual note says, "I'm showing a rectangle and I have a border thickness of five." I can have that. And now I'm also showing a resource—an image. Is the rectangle on top of the image or below, given sufficient size?

I think "on top" seems to make sense.

So, the rectangle should be on top, right?

Yeah.

Yeah.

Okay.

Yeah, it depends—I think I could think of it both ways.

Well, if somebody took the work to say, "My rectangle has a border, it's visually visible, its thickness is five, it's blue," and then it should be behind the image? Really? Why?

Because, um, if you have an image, you probably want it in front, but I don't know.

This example that—I would say we could actually include this as a specific example. But what I would say there is, you have two visual nodes and specify the Zs yourself.

That's one way to solve it. But usually, if you have a visual note, you can give it a rect outline—a rect shape. That's part of the extension. You can also give it a resource, maybe an image. So what's the recommended way to Z-order them? Because there's no Z-order defined in the file. Only the visual note has one Z-order, but now it has two visual things in this one node.

I think we could—so two things occur to me. One, resources probably need a Z-ordering themselves. Or we go by array?

Resources are abstract. They are just defined, and then multiple nodes can show the same resource. So it doesn't make sense to have one Z-index defined for multiple invocations of resources.

Oh, as you were saying, you only have one resource per node?

They are singular—you can't have multiple resources per node.

I think you cannot. That's right.

I'm looking at the example—you’re right.



It’s not. Maybe in that case, awesome. But I think we just default to saying the resource is behind—quote-unquote "behind"—the shape. And if you want it to be different, then create two visual nodes and adjust the Z-ordering appropriately.

Yeah.

I don’t know. Michael, you wanted it to be in front of the rectangle?

Yeah. With that rectangle example and a resource—an image that's a resource—I can imagine that the image will be drawn inside the rectangle with the border around it, clipping the image if you have a round border.

Yeah. If the rectangle is the frame, then that's actually what I’m recommending. I’m recommending that the image is behind the border, so the border would show on top, like you just said, by default.

Well, the resource should be clipped within the shape, I think, ideally, if the application can do that.

Yeah.

Yeah, okay.

What else do we have?

Regarding multiple resources per node—right now, we only allow one. But shouldn't it be possible to have multiple resources? Because I can imagine that you might want a background image as a resource but still have text drawn on top of it.

I think I like the simplicity of only allowing one.

And even more so, I think we should push people towards creating new nodes rather than stacking multiple resources in a single node. If you have a complex canvas that allows multiple resources per node, well, when you unbundle the OCWG file, make sure you create multiple nodes instead, because it’s just not a common thing.

I like both arguments. So let’s stick with having only one resource being the resource of the node. But to accommodate for Michael’s use case, which doesn’t sound too exotic, we could introduce a background extension that allows a secondary resource in the background of the visual node.

100%.

Yeah, that's a great point. That’s good. This is exactly why we have the extensions, right?

All right, very good.

I have another question regarding the Z-index. If you have multiple nodes on the canvas, we currently don’t have a Z-index on the node itself. So how can you change the order?

We don’t want to set Z-index on the node? 

The visual node has Z-index, right?

Yeah.

Sure.

Yes.

Yeah, I hope so.

You can specify the coordinate without it—just x, y—or you can specify...

Yeah, that’s position, but is the Z-axis actually defined?

I think it’s in the spec.

The Z-axis is basically the ordering.

I guess we didn’t say explicitly.

Yeah. In LDraw, how is it solved there? As far as I know, there's a special Z-index field, which is coded in a special way. Somewhere in our discussions, I posted a link that describes the algorithm.

Yeah, it was called "fragment indexing," I believe.

And that way, only that number needs to be changed. You don’t need to move the nodes to a different position in the array; you just change that number.

Yeah, but I think that’s how we expected it to work as well. You have an optional Z-coordinate, and you can put a real number in there, and sorting by these real numbers defines the Z-ordering. So there's no need to reorder the array.

Yeah.

Yeah, we could solve it like that. It’s a simple way.

I think that’s already how we solved it—there’s no array ordering anywhere, no semantic order.

Mm-hmm.

I have two questions left.

One: we once decided we could have a relation type called "layer," but we already have "set" and "group." How would "layer" be any different?

So, let’s go to examples where it's used in canvases. In TLDraw, you can have multiple canvases within a single project. In Figma and FigJam, you have the idea of layers. It basically means that everything underneath a layer can be moved as a group in front of or behind other layers.

That’s different from grouping objects together as a "set" and attaching them in a group.

Yeah.

It really is about Z-index, mostly.

All right, that’s a different semantic. That makes sense. We can add it. I like it.

Mm-hmm. Good.

So, my last question: we have a parent-child relation, which turned out to be useful for transclusion. Originally, we thought of transclusion as a node extension. Our idea was that a node could say, "I’m using an extension to specify that I’m inheriting from another node."

But it turns out we already have a relation extension that says, "These two nodes are related—this one is inheriting from that one." 

So now the question is, what’s the better modeling approach? Should it be a relation extension or a node extension? 

The nice thing about a node extension is that if a node is just showing content from another node and you delete it, it’s very clear that the relation should be deleted too, because it's stored in the same block.

Adding it as a separate relation adds more complexity to the implementation.

Interesting.

So, to recap what you were just saying: a parent-child node extension would allow us to have a separate visual node that inherits some properties from a parent node. It would be compactly represented as a node extension.

But if we used a relation extension instead, how would it be different?

It’s just a different style—it expresses the same semantics. 

In both cases, they’re extensions, not core features. Whether it’s a relation extension or a node extension, it’s up to the implementing canvas to model the inheritance relationship—copying properties, keeping them in sync, handling transclusion in the real world.

I’m not sure I have a strong opinion. I abstain.

I’m trying to visualize it: you have two nodes, one inheriting from the other. You can either put the inheritance information inside the inheriting node (as a node extension), or you can put it outside in a relation (as a separate relation extension).

The original node is untouched in both cases. The difference is whether we store the inheritance in the inheriting node itself or as a separate relation.

One thing to note: parent-child relations don’t always inherit properties. They can just represent hierarchy, without transclusion.

That’s a good point.

If we made it a node extension, that would force every parent-child relation to imply transclusion. But as a relation, it remains more abstract.

I think my slight preference is to keep it as a relation. Even though, Max, you make a good point that the visual properties being inherited are a concrete, visible thing.

Yeah, when implementing it, the node will have to check the relation and copy properties if necessary. But it still feels like a relation more than a node extension.

Okay, slight preference for relation, then.

Yeah, because for ports, we decided to put them inside the node itself, rather than as a relation.

Right, because ports are usually visual—they're attached to the node.

Though in some cases, like Michael’s use case, ports have a conceptual meaning beyond visuals. In that case, an extension might be needed to define them fully.

Yeah. In Codeflow Canvas, nodes define their own ports. The OCIF file’s port definitions aren't used by Codeflow Canvas at all right now, because ports are currently handled internally.

Okay, I’m done with my question part. 

Michael, would you like to give a demo of what you’ve been working on? I know you dropped a picture in Discord, but it might be nice to have a demo on the recording too, for those following along at home.

Just a moment—I have my tool open. I’m just switching to the directory so I don’t have to show some random subdirectories. One moment.


I have too many directories, but it’s easier on Mac, actually, than on Windows.

Max, thanks for your work in accumulating questions and bringing them to the meeting. It definitely drives the discussion productively. I appreciate that.

Let me know when you’d like a PR review of 03.

I think we’re done—yeah, you can take a look.

Okay, cool.

All right, Michael, you are sharing. We can see your screen.

I have this very simple OCIF file. It’s still 0.0.2, not 0.3 yet, but it has a couple of nodes. 

I don’t have an implementation for a circle node, but for a rectangle node, I implemented something special specifically for OCIF. So I’ve imported that file here.

Nice.

And then you see here the details. What happens is that I extend it immediately with information from Codeflow Canvas. 

I’ll give it some more information for Codeflow Canvas specifically.

So you kind of make a Codeflow node, right?

Yeah.

Because—like you were just saying—your nodes have additional meaning to them. Every node does. It has ports available to it, and all that kind of stuff.

Yeah, you have to be able to program with them. This rectangle node in Codeflow Canvas doesn’t do anything—it just passes data through to another node.

So I should be able to connect two nodes, and then when I execute it… you see nothing wrong.

That’s slow, but… yeah, you see a white rectangle. That’s because nothing is happening yet.

I should be able—I haven’t tried this out yet—but let’s see if it works.

Yeah.

I think it works.

Yeah.

I also have a number here, then it just passes through.

That’s awesome.

So you have the import direction. I saw you also had an import grid.

Yeah.

Do you want to try importing that one?

I created this OCIF file with ChatGPT, by the way.

Nice.

Yeah, I had to do some extra prompting to get it right, but it works.

What was the extra prompting? Do you remember? Like, what did it get wrong at first?

I think it didn’t put everything on the right level. 

I think these stroke properties were in the wrong place in the JSON.

Oh, interesting. That makes sense.

Yeah, it wanted to put stroke color and stroke width at the root of the node.

That’s a reason we started where we did and then pushed it down into the properties.

I’m not sure if I put this back into the chat or just left it in some examples.

I don’t remember exactly.

Yeah, I think a really fun tool would be a website where you can upload a picture of a whiteboard, and it converts it into OCIF format. Then you can export it to any of the tools that OCIF supports—TLDraw, ScalaDraw, Obsidian Canvas, etc.

The process would be: an LLM looks at the image, generates an OCIF file, and then you use an OCIF-to-TLDraw converter to load it into the tool.

That could be a fun little demo website.

I already have an export to TLDraw—it’s very basic, but I can already export OCIF files to TLDraw a little bit.

This is an awkward roundtrip—you import your file into Codeflow Canvas, and then export to TLDraw.

It’s not perfect, but let’s see if it works.

Yeah.

It’s in Dutch.

Where did I put it? In the downloads, I think?

Yeah, downloads.

That’s not today.

No.

Sort by time.

Yeah, I think I did, but it’s not there.

Oh, did it rename?

Wow.

Nice.

Oh.

Did you see that? It created ports.

Uh-huh.

It worked.

Zoom in on that.

That’s the particular node—the node with the ports.

Oh, clever.

So you created separate nodes.

Yeah, and then connected arrows to those nodes.

Yeah, I currently don’t have as beautiful arrows as TLDraw does. 

I’m working on that, but…

No one does.

I’m using Cursor to build with, and that’s difficult.

Yeah, they have a very good blog post on how they do arrows.

Maybe a separate library.

Yeah, but their arrows are really polished.

Better than TLDraw’s even?

No, not quite.

It’s hard.

But they have a good breakdown.

You can also export this to OCIF, of course.

Yeah.

Oh, wow, he saw this.

Yeah.

Not much more information there.

Wow, that’s a massive OCIF file.

Yeah.

Very cool.

This is actually running a chat completion program with function calling and streaming—it’s very cool.

But that’s a different story.

I just wanted to test how it works.

That’s awesome.

It works.

Yeah.

Thanks! I try to make progress every week.

I also tried using Cursor to generate a sample OCIF file.

Did it work?

A little bit. Let me find it.

Yeah.

Here it is.

But it doesn’t do much.

Unfortunately.

Not bad, though.

I think there are nodes here that Codeflow Canvas doesn’t recognize yet.

Yeah, we need more examples.

What domain could they come from?

Oh, it has `example/circle`—that’s funny.

I think that’s still in our spec somewhere, Max.

Do a command-F search.

I think it’s still there.

Oh, he probably pulled from the 0.2 spec.

Is this from 0.2, or is it from the 0.3 branch?

0.3, but I changed this manually because I imported the file that Cursor generated.

I couldn’t import it as-is because I’m checking for version compatibility.

Good for you.

Yeah, so I recognize if it’s valid or not.

That’s the right way to do it.

Well, I think OCIF is a really nice format.

I’ll keep iterating on it.

Max, I think you already let me know about a few things in the spec.

But anything else that was painful to work with?

I’m trying to remember…

Yeah, actually, right now, I don’t use OCIF as the storage format.

I store the OCIF file, but I use IndexedDB for storage.

So when I refresh, everything stays.

I try to keep OCIF as the source of truth.

For Codeflow Canvas nodes, I find their original OCIF data and merge them.

That makes sense.

But I think if you have two nodes that share the same resource, you need to duplicate the resource when exporting.

That’s something I don’t handle yet.

But I imagine other implementers will run into this too.

Yeah.

Maybe we need documentation on how to handle that.

Yeah.

In the cookbook, I have a section for developers.

So we should document these best practices.

Yeah, I actually found reconciling OCIF with my own system easier than I expected.

Okay.

That’s great.

Yeah, it’s just a matter of keeping things in sync.

You have to decide: is OCIF the main storage format, or do you convert it when importing/exporting?

Probably storing it as OCIF is the best way, but it depends on the use case.

Right.

Also, handling multiple nodes referencing the same resource is a challenge.

Yeah.

If you update one, should all instances update?

We discussed this before.

The idea was that multiple nodes could reference the same resource.

That’s not something I handle yet, but I can add it.

Yeah.

It shouldn’t be too hard.

You could just look through all the nodes that use the same resource and update them together.

Yeah.

I think the hardest part is getting other canvas creators to try using OCIF.

Yeah.

We need to find the right "hook" to attract them.

I think Obsidian Canvas is a great target.

It’s simple and lacks advanced features.

People who need more will want to export to other tools.

Yeah.

I think we’ll have to lead the way by writing some converters first.

That’s my guess.

Yeah.

And we can use AI tools to help us.

Absolutely.

Like I said earlier, we can get a lot done in just a few hours.


Well, guys, I do have another meeting right at the top of the hour, so I think I’m going to call it here unless there’s anything else.

Yeah, just take a look at the 0.3 draft, and if things look good, we can turn it into the next version. Then I’ll just remove the draft labels and polish it up.

Great, will do.

Yeah, and we can do that pretty quickly.

Indeed.

Yeah, I’ll try to get to that in the next 24 to 48 hours so we can finalize it. 

Because if I don’t, it’ll disappear from my brain until the next time we meet.

All right.

All right.

Sounds good.

See you all next time.

