# Meeting 4 Transcript

Date: May 21, 2024

There we go. That's the sound.

So yeah, a quick bit of context for those that are new here.

So the kind of the singular goal of this group really is not just a kind of interest group.

I mean, people are here for canvas-related reasons, right? And we're interested in this stuff.

But what we really want to do is we want to take the assortment of canvas-based tools that we have existing in the world today.

And we want to make them talk to each other and interoperate to the extent that that is technically and organizationally possible.

So we have interest in that from some quite significant projects like TL draw, Excalidraw, Stately, and others.

And hopefully in the future, we can extend that to further revealed places like, for example, the Blender nodes system or all these other tools that have these kinds of interfaces.

And to quickly touch on what we kind of mean by canvases.

We can kind of think of this spectrum, something like a visual structural spectrum where on the one side, you have entirely structural representations where the topology is really the only thing that matters and where you're not really representing anything spatially.

Some diagram tools kind of work this way where you're really just describing a system, and it's laid out automatically.

And there's probably better examples, but on the other end of the spectrum, we have something like Photoshop where it's entirely spatial and entirely visual.

You lose any kind of semantic relationships between objects or shapes on the canvas.

And so what we would like to do is kind of take that middle chunk and build a spec that is extensible and simple and works as a baseline for a bunch of these different tools.

There's a question for you there in the chat. Yes, I think that's the answer.

So yeah, that's really the goal. And we're trying to push somewhat fast on this because we don't want to rely on passive interest.

So I think we're shooting to have real functional interoperability between some of these tools in about a six-month timeframe from when we started, which was, I guess, a couple of months ago now.

We've made some progress on demonstrating interoperability between TL draw and Obsidian. I'm working on a TL draw-Excalidraw interoperability.

And what this group usually tries to do on these calls is take issues that are coming up in defining what should be in the spec and how that should work and then kind of hashing those out.

This one is a little bit different in that we've had a bit of a chunk of time when me and Jess have been both busy, and prep has been somewhat minimal.

But we do have a large amount of discussion points that came up on the last call, although I was slightly, if I'm being entirely honest, relying on a bunch of those same people from the last call being on this one, and we actually have a bunch of new faces, which is great.

So I'm wondering where I should take us here. Let me just check the chat.

Orion, I actually have a suggestion.

So maybe you should talk about where you're at with the Excalidraw-TL draw interoperability and how you're thinking about executing on that first piece.

Because I think even that might motivate some questions and conversation.

And then beyond that, while you're working on that piece, I can put on the canvas a couple of different kind of large conversational headings that we've been talking about, and we can maybe pick and choose from those once you've gone over your overview.

Yeah, let's do that. And also, as a little note to ourselves, I think we should do that as a document for future calls where if we want to give people the kind of high-level rundown of what's already been discussed so we don't end up returning to hashing previous discussions, I think that'd be a useful artifact for us to do at our next sync.

So yeah, on the TL draw-Excalidraw front, I believe this repo is up on the OCWG GitHub. I'll double-check that and put it up if it's not.

But what I've been working on is a very simple proof of concept of syncing a subset of those two schemas that is interoperable between those two systems around this shared file format that we're iterating on in these calls.

We're hoping that that file format is a future version of the JSON canvas that Obsidian developed, but as it stands, that format is not really expressive enough for many of these tools to use and is very geared towards Obsidian specifically.

And so where I'm at with that now is that I have a working sync between each client, the TL draw client and file format, and Excalidraw and the file format there.

I have a subset of the schema supported that includes text shapes, rectangles, edges between shapes, and a handful of other basic things like color properties.

The thing that's missing, though, for this experiment is actually just a better way to handle kind of concurrent reading and writing to that file, because files are not exactly meant to be worked in that live sync context.

And so basically, the remaining piece to do there before we have a working demonstration is just to probably put a server in the middle around the file, have the two clients talk to the server instead, and then we don't have to deal with kind of bad read and write state and issues like that.

We do also on the GitHub have the TL draw-Obsidian sync, which was the first thing that we made, mostly to produce a GIF.

So it's very minimal, but it does work.

Okay, yeah, I will, after this call, push changes. And as with this, if people have a project that they have technical experience with and you have the time to build out basic interoperability between tools, that would be great, because the more examples of this kind of stuff we have, the more evidence we have to decide on these...

What's the way to say it?

There's a bunch of spec decisions that are, at first glance, kind of arbitrary. And so especially for those figuring out what these tools actually need specifically can help take these hard-to-make decisions and give us something to work with for those.

So open invite to join in on this effort.

Jess has stressed multiple times the importance of getting quite quickly to working functional software, especially when it comes to group momentum and stuff like that, right?

No one's paying you to be here. You're turning up of your own volition, which is fantastic.

And I think we all want to kind of respect that. And part of that means getting stuff working as quickly as we can so that we can kind of share this sense of progress being made and not turn into a decades-long bureaucratic standards body. That's not exactly what we want to do.

So I'll leave that update there.

Jess, do you want to run us through a couple of these?

Yeah, sure. So these are a selection of topics that we've discussed in past meetings, and we have more or less some thoughts on how we might handle some of these things.

So there's... I will go through these four topics.

And if you have one that you're particularly interested in, you can either raise your hand or comment in the chat, or you can go through and tag some, like put something on the document of like, I'm interested in this one or whatever.

And I also was not watching the chat. So if there's something... Yeah. All right, cool.

Michael was saying, I want to work on interop between TL draw and my own project, which is a visual programming system, and see if we can use TL draw for improving the layout of flows that I build in my own tool. That's a really interesting idea.

So the four topics that are up here real quick: external file handling and asset management is right now the way that, if you've looked at JSON canvas and Obsidian, Obsidian is all about laying out notes on a canvas.

And those notes live inside of an Obsidian vault. And so they are literally local files alongside the canvas files.

And so when it does references, when you put a note on the canvas, they just put the file name of the local file that should be in that spot.

Now, obviously, if you distribute the JSON canvas file, you're not distributing the note.

And so the content doesn't go with the JSON canvas. It's not embedded in any sense in the JSON canvas file.

So there's a big question of when you have multimedia, what do you do here in terms of handling external files, images, documents? TL draw, for example, when you export a TL draw, they base64 encode any images that you dropped into a TL draw.

So that's one potential option, but the spec should be permissive here, but also like, here's how you should embed images, documents.

Another one topic is fallbacks of the overlap of basically you have this giant Venn diagram of the feature set that's supported by various canvases.

And what do you do when a feature is supported in one canvas and not another, like say freehand text is a key, pretty key part of TL draw, but it may not be supported in this other canvas.

How do you have a fallback for that? How do you tell that canvas to support that feature, demonstrate that maybe there was something here that I can't render?

And so that maybe people don't draw on top of it, or do you just leave it completely out? There's some open questions here.

Schema and extensibility is something that we've talked about, about how do we define the minimum number of basically base objects?

And what we're thinking right now is that every node has some type, and that type, it has a schema, and that schema is something that could be extended beyond the spec, right?

So that we don't have to account for all types within the specification.

We basically create the spec in such a way that it's got a hole in the node schema for you to insert whatever schema type you would like, and then we can kind

 of handle...

We're basically breaking the overall spec into a spot where the spec can be extended in all sorts of interesting ways, kind of similar to MIME types or application types in HTTP.

And the final one, which I'm actually really interested in talking about because David's on the call, is handling shapes without an XY.

So we talked about up here, this canvas spectrum, structural canvases that are not visual often have the key information is about the relationships between nodes, and they often have layout algorithms that are automated.

They'll have a, you know, organize these in a force-directed way or think Graphviz and some of these other automated tools, but shapes have not been manually placed on a canvas in the same way that I just placed these shapes manually on the canvas.

So there's no explicit XY for the different objects on the canvas.

So the big question, this is an open question for me, I have rudimentary answers to the other three things on this board.

This handling shapes without XY, I do not have an answer for and would be very curious.

And the way that I would frame this is, imagine David's Stately AI generates a state diagram for your code base.

And then you want to bring that into TL draw or Excalidraw or some other canvas and you want to annotate that before passing that on to a teammate.

When you open that Stately canvas, let's say you've exported from Stately into this JSON canvas 2.0 format.

I don't think those objects have XY coordinates, or maybe they do, and this is an open question for you, David.

Would they have XY? And if they don't have XY, how should we force your tool to write XY for those things before you write to JSON canvas?

Should we allow for nodes that have no XY coordinate and then force the tool that imports the JSON canvas to have some sort of intelligent layout or just stick them all on 00?

This is my open question/problem.

Right now, it does not export. I mean, there's no reason why it couldn't, but right now it doesn't.

And that's because with the nature of state machines and state charts, the nodes and edges are all relational.

So it's not, you know, in the studio editor itself, you do have XY coordinates, but it's not a strict requirement.

So if we were to copy-paste a structure from Stately to somewhere else, then ideally it would be some sort of automatic layout algorithm that just puts things together based on those relationships between nodes and edges.

Gotcha.

If I could freeze one of your state diagrams in time, like you're at the stage where you want to move something out of Stately and export it to another program.

At that frozen point in time, that snapshot, you're saying it would be reasonable for Stately to assign XY coordinates to those things because they do.

Sure, yeah, yeah, that's totally reasonable to do, but not necessary.

Got it. Yeah, and I think the more that I think about how to interface between these two, I'm trying to think of what other solutions there would be to bringing in a Stately diagram into TL draw via this intermediate format.

I think there's kind of, it seems to me that there's kind of two options, and maybe there's a third or a fourth and someone else can enumerate other ways of solving this problem.

It seems like it's either the structural editor, when writing to JSON canvas, must assign XY to nodes, or a visual editor, when importing a JSON canvas that does not have XY coordinates for nodes, will have to have some automatic layout algorithm that it applies to do that initial XY organization so that it can work with in TL draw because there's no such thing as a node in TL draw that doesn't have an XY, similar for, you know, Miro or Excalidraw.

Are there any other ways that we could solve this problem?

Oh, go ahead. Yeah.

Well, it's not a solution, but it's interesting.

Is it possible to differentiate the jobs to be done here? I mean, in one sense, we're talking about opening a file in another interoperable system versus copying a portion of a file and adding it to another system.

So, you know, I'm not sure if those should be treated separately, but if so, one could be easier to accomplish than the other.

But in thinking about your question specifically, there's a concept of, I'm going to say it wrong, but quaternions.

It's essentially like you can imagine every cluster has its own center of gravity, so that's its XY axis, is sort of based off of what might be considered the main anchor for the thing that you're copying and pasting.

So it stays, the elements that are being copied over stay in roughly the same related area, but then whatever it's jumping into doesn't matter as much, which still there's, you can imagine all kinds of problems and it might need to have some sort of interstitial, hey, I'm about to put this into stately, do you want it to look like this before I apply it?

Those are three thoughts.

One of the discussions that we've had before is on whether X and Y coordinates should be kind of imposed by the schema from this bit of discussion.

I am kind of leaning towards the idea that for simplicity's sake, they maybe should be.

In the very worst case, you end up with, you know, something at zero, zero, like being assigned some default values.

It would impose work on especially the more structural canvas tools like stately to provide that data, which might live in UI state or somewhere that's not really part of some or internal format.

But that seems like it might be the better approach compared to kind of doing the opposite of that, where you put the onus on every one of the tools to potentially have to deal with laying stuff out themselves in some way, even if that was really basic.

Yeah, but part of this discussion around this kind of work in progress, JSON canvas 2.0, whatever ends up being called, is figuring out what is the truly minimum set of properties or fields or pieces of information that you need for the base spec.

We've had discussions before about how we handle extensibility and how we do schema versions and types and that kind of stuff, and a lot of that stuff seems super possible, and there's good precedence for that as well.

The more stuff we can get rid of, the better.

But I'm wondering if X and Y is really not one of those things, or X, Y, and Z in the case of a three-dimensional canvas, which we hope this will support as well.

Would it make... I know I've got a couple of TL draw screens open, and I've got chunks of information. There's no real order.

But would it make sense to have something like a metasex SAM model where it's kind of like, here's a loose... I see these things are roughly marked together, but here's another overlapping rectangle.

How many rectangles of semantic similarity do you want to copy and paste over?

And then treating that as kind of like an invisible semantic block that's underneath these canvases. Would that help with interop?

I don't know if that even made sense, but...

I think that's something that we're thinking about as sort of the application layer.

We hope that you could make utilities and experiences like that on top of whatever specification that we're working on.

The idea would be that you could pull a canvas, an export from many different canvases, and then explore that canvas in the way that you were just describing, like are there additional semantic layers and all that kind of stuff.

See that. So the focus of this group is on enabling that experience that you're talking about as opposed to actually building it.

Yeah, of course. Yeah, makes sense.

There is a related topic that we've discussed a little bit in previous meetings of the concept of groups. How do you handle grouping objects, sometimes called frames in certain tools?

I think they call it frames in TL draw. I'm trying to remember.

There are frames, but you can also reparent shapes and you have a parent-child relationship, which functions kind of similarly.

Yeah, exactly. And so how to define those in the spec is going to be an interesting challenge.

Yeah. I think, like you said, in the name of pragmatism, it probably makes sense to require X and Y for nodes right now because it basically says if you're in the structural end of this spectrum over here and you want to play ball with the JSON canvas spec or whatever spec we come up with, whatever we call it, if that means you're going to need to assign X, Y when you do the export.

And that will allow you to basically move from there.

Now, when you bring in a canvas from, say, TL draw or something like that that already has nodes laid out, you're free to use your force-directed layout pool or whatever to ignore the X, Y's that are there.

That's what you would like and redistribute them around the canvas. That's totally up to you.

But when you do export, you're going to need to do that because I think that puts less pressure on some of these other tools to handle things with no X, Y.

Makes sense to me, too. I also think about tools like Obsidian where it's basically just text-based notes.

And even if that were to export X and Y, you try to import that to TL draw, which renders text a bit differently, different sizes, and all of a sudden your X and Y's overlap.

And then TL draw could decide, you know what, I'm going to try to respect the relationships between the nodes, but I'm going to give them my own X and Y so that they're evenly spaced out and not overlapping.

Yeah, I mean, that gets to this question of how to handle bounds, not just whether we do or not, but there's unfortunately kind of a big decision space there, especially when we think about whether rotation is supported because there's a potentially really large difference between the axis-aligned bounds of a rotated shape on a canvas when compared to the local

 bounds of that shape.

Maybe the answer is to make that optional and maybe wouldn't be bounds, it'd be like a width and height property.

And that gets to some of that stuff you are mentioning, David, where we have these kind of local differences in how text is rendered, even if there's a widely shared set of text properties and that kind of stuff, which I don't think we actually want to impose.

We want to have somewhat reasonable handling of something like a paragraph of text across different tools, which I think means that we want it to stay as legible as possible.

And either way, we're going to impose some work on these different tools to support this format, right?

If we don't have any bounds and we just say, okay, just draw the text however you want and figure out the rest, that's one route.

If we did strictly impose a kind of a width and height or some kind of bounds there, then the onus is on the tool to actually make sure the text is rendering correctly in that unknown size.

And if they have, say, some reset font sizes, for example, then that could be really problematic.

But it could introduce challenges because the local schema of that tool doesn't actually support the rendering in a way that would be most legible.

That's one of the places where I'm least sure about this is how to handle bounds.

One other place where that's important is the treatment of unknown objects on a canvas.

So let's say Stately has, you know, introduces like a new special kind of edge with its own schema and a bunch of, you know, it has like types for like ports or whatever it is.

In that situation, if you drop that into something like TL Draw and it has no idea what the shape is, having bounds can be really useful there because it gives you something.

It lets you say, hey, I don't know how to render this thing. I don't know what it is, but I do know that this is the space on the canvas that it occupies.

As opposed to just having an XY point saying there's something at this position.

That's one of the places that I'm least sure.

I feel like bounds should be optional depending on the schema of the object that you're presenting because there are some objects that you want to just say it exists right here at XY and then leave it up to the other thing to interpret.

But then there are other times where you're like, no, no, no, this actually does have a width and height that it makes a lot.

We want to encode those bounds, but I feel like the, and especially like the thing where you were talking about rotated shapes and then like imagine fully arbitrary bounds, right?

Of, you know, as an ordered series of points that enclose the bounds for an object.

I feel like those things should be handled through the schema and extensibility model.

And that way you can have, you can even have different canvases that have different types of bounds support, right?

And like this canvas, for example, this, the way this came up was that was really interesting is Canopio for text objects does not specify a width for text objects.

It renders the width based on the font, like the size of the font.

And so when Canopio was importing Obsidian Canvas or exporting to Obsidian Canvas, it would, it, you know, it was required to set a width, like basically there were problems both ways.

When it was importing a file from Obsidian, there would be a text file, a text object that had a width and it's like, I don't know what to do with that width, so just throws it away.

And then in the other direction, when it's exporting a text object, it doesn't calculate width.

It just says, here's the XY location, here's the text and the font size and all that kind of stuff.

And it's renderer automatically takes care of that.

And so it had to, it was forced to like calculate a width height for that object when it didn't really need it internally.

And that would, if we went down the schema and extensibility land, what that would allow for is like Obsidian text objects to be their own schema and Canopio text objects to be their own schema.

And then those two, you could basically write a mapping between those two schemas that say, you know, whether they're, if you're available to move back and forth between the two.

So I don't know if that makes sense.

Yeah, so for safety too, we have, you know, parent nodes and so their widths aren't explicitly defined.

It's just the width of, or the bounds of whatever the children are, and that happens recursively.

I put down here constraint-based because I think that the least common denominator here is going to be some sort of constraint system, optional though, but you know, the ability to say, hey, the width of this depends on the width of that, or the distance between this node and that node is actually dependent, or it's like fixed to this length.

So, you know, you might not even need X and Y, you just need to know where they laid out.

Okay.

You know, you could determine the position of the other one based on, you know, those constraints.

David, are you basically describing like a force-directed type layout system, like an automated layout system, where you basically decide how to lay things out based on how the renderer, how wide a thing needs to be based on how the renderer is going to render it at that point?

Somewhat, yeah, but I think that, you know, at least for an initial version of this spec, we might not want to go full, like, everything needs to be defined in terms of constraints rather than fixed limits.

But the fact is you can define like, hey, this has a fixed width and height, and those itself could be the constraints.

So, or this is at position X and Y.

Gotcha.

Okay, cool. So that, those might be like relative with their heights based on like their parent node or something along those lines.

Exactly.

I'll have to think about that. It feels like we're getting into HTML at that point, or you have like, and relative positioning and oh my gosh.

We're just going to reinvent Flexbox.

Wait, actually, hold on. Steve said something in chat, and I'd actually like to make sure I'm understanding what he's saying. So he said having an Obsidian schema and other schema for basic text would be the antithesis of interoperability.

Can you say more about that?

Yeah, I heard you say that you'd have different schemas for text, and it's worrisome because you'd have to have every tool know about every other tool just to import something basic like text.

And that would be worrisome to me.

Yeah, that's actually a really good point, and I think text feels like one of the things that should be, like we talked about having potentially namespacing the schemas.

It feels like text would be one of the things that would be core to, would be part of the core specification, such that you basically have to support what, but could still have, I guess the way we would support width and height in this case for things like Obsidian would be that there'd be optional parameters of width and height that you could then use.

That's a good point. Text probably doesn't actually, is probably a really bad example of something that we would want to have a schema for and probably should be core.

So this is, I'm just going to go straight into the worst possible idea, so it's on the table and nobody has to worry about having a dumb idea.

If the most important thing was to get something done, you know, in like six months, right, then what I'm, a couple of thoughts is, first off, that's quite a task because there's so many different ways that people use a canvas, and there are different things that are important to them at different times.

I just pasted over some boxes and arrows from Excalidraw into TL draw, and of course it just came out as text, right? I don't care about the X, Y layout, all I wanted to retain was the relations, the little arrows that were connecting, right?

So if we're going for an ugly, complex solution, not a beautiful one, then I'm looking at what Jess wrote about the fallbacks as perhaps being the most interesting near-term feature of like, hey, you got this thing, either you're going to open the file or you're going to copy a bunch of it into something else.

And just imagine for a moment, yes, it's a modal, it's a separate application for a thought experiment that goes, okay, I see a bunch of text boxes, is that correct?

Or, you know, like, do you want to retain that these boxes connect to these other boxes? Should I focus on the arrows? Should I focus on the X, Y?

You know, like that kind of like, here's what I can read and understand pretty safely as a fallback, but here's what I'm not getting at all, so just warning, you know, and then that's the kind of thing that could improve over time.

So maybe like, it's more about installing packages in these apps that like give proper errors, or, you know, just to even let you know this is what's not going to come in, maybe you want to take a snapshot of that.

That's wide open space, but I'd love to hear your thoughts. I think fallback though is really promising.

So I don't think that that's the worst idea at all. It's something that we talked about before of how should fallbacks work.

And I think a really promising solution there as an escape hatch, and it doesn't have to be a thing that every tool offers to their users, but being able to take some shape with an unknown schema to that tool and just rendering that as a text box or even potentially an editable text box.

Which will get, which you can try and, so if you're like, oh, I actually,

 I know that this tool, like it only doesn't understand because this other tool has this extra thing, which it doesn't know about.

Let me just get rid of that field. Try and add it again.

Like, for example, the tools that have typed edges versus ones that don't, for example.

I think that's like a really interesting fallback. One of the biggest reasons is that it's a universal fallback, right?

Like, as this is always text under the hood, it means that you can reliably fall back to text from any unknown schema.

Yeah, even in the, it'd be interesting if I had a system that could say, okay, I can't read any of this mess, but I can tell that it's OPML.

So why don't you go into Anthropic and give this prompt, you know, assuming that you want, you know, this output, and it may not be great, but it'll get you, you know, maybe a little bit closer.

You know what I mean? Like, the fallback system could integrate an idea of a system making a best guess of what it's looking at before we get to a point of a perfect solution of interop.

I think you made a good point about a good fallback giving a good incremental path to adoption where you can have quite a large gulf of schema mismatches where tools don't really know what the other tools are saying outside of some basic types like text, for example.

And that can then prompt you to be like, oh, hey, actually, the local schema that I'm using in this tool and these other tools that people that my users are interoperating with, this is something that doesn't need to be its own type.

There's enough commonality to kind of unify those or to take some, you know, base arrow thing and say like, hey, the schema of this is normal arrows, but also we have this one extra property for some, an edge type or something like that, or like allowable ports or something local to the domain that that tool is working in.

Yeah, absolutely.

Yeah, because like the other part of this, which is such an interesting working group, you know, when you're pulling something from one tool to another, your needs are very likely not to be the same as they were when you first made it in the other tool.

So maybe color coding is important, but maybe not.

Yeah, exactly. That does raise one point that's been a recurring thing that's come up is the need as something that's very hard to enforce, but the need for these different tools to basically respect data that they don't know about.

So, for example, if you take something in TL draw and you chuck it into stately, and you get, you know, this very reduced feature set, obviously like intentionally, right, because stately and TL draw have very different purposes.

You want to then be able to do some stately things, have those changes reflected in the underlying canvas, and then be able to take it back to TL draw and have, even though the TL draw stuff might not have, you know, synced up, right, because like it wasn't being updated, to still have those things that you had before reappear in TL draw.

I think without that, it becomes kind of untenable.

And that's not a perfect solution by any means, right, like you're going to get state that is kind of redundant, right, like if you take something from one tool to another, you delete some things, then you go back to the original tool.

Maybe the deletions that you did, they weren't propagated to other stuff that really should have been deleted, because the tool that you are in when you made those deletions didn't know about the semantics of some connections that would have normally meant that you could get rid of those things.

So not perfect, but I think it's a pretty important principle, and also when it comes to extensibility, it's quite important.

It's not too dissimilar to how email evolved as a protocol where people were passing emails around with extra data, even when they were kind of, you know, using homebrewed protocol extensions and stuff to do new things with email.

And without that being preserved through, you know, like a forwarded email or something, then a lot of the modern features that we have, like rich text, for example, probably wouldn't have evolved so easily.

The ideal experience is, correct me if I'm wrong or flesh this out, is it like hitting export and then picking a file format, different than say like OPML, but you know, that kind of thing and saying, okay, this is the structure I want it to be in, or is it like just replacing copy and paste when you're in a canvas?

I think there's probably different tiers. Where we would like to get to first is a file, right? So for the tools that want to adopt it, you'd be able to go, you know, into a menu, say in TL Draw, like you can do this with TL Draw's format already, right?

You can take what you're looking at here, you can export that as a JSON file, you get a file out of it, you can also copy specific ones, yeah, copy as JSON in that case.

And so we would like to get to a place where you end up with a file that represents an entire canvas, and you can take that out of one tool, put it into another, and back again.

I think the way we are building this should also support copy-paste in terms of the spec itself, where the tools support that is like a very different thing.

It would effectively require that a tool commits to the spec for their own copy-paste functionality, right? Because you can't retroactively kind of, when you copy out of a thing, you can copy multiple mind types in a single copy.

So they would need to commit to making it one of their copy types that it would copy, and then the receiver can then look at the different types that are being pasted in and say, yeah, give me that one, or give me those two, or give me those three.

At least that's the way it works on macOS.

So that's how you get like rich text and plain text copy from a program.

And there's two things that are inserted in the copy buffer or in the paste board or whatever location.

There's one that's got the rich text and one that's the plain text, and based on the destination, it gets to choose which one to take.

Is MIME type the only way you can choose that? Because couldn't they potentially both be the same type as far as MIME types? Like I can say like if they were both JSON, right?

It's not strictly MIME type. I'm just using that as a reference that you would basically be able to say, you know, text slash rich text, text slash plain text or whatever.

And we could say canvas slash JSON canvas and maybe even put a version number.

But yeah, the destination would then be able to say, yep, I accept that one. I'll try and paste this in.

Okay, that's really good to know. I didn't know that was an option.

So that kind of brings me to the second thing I was going to say then, Alan, is that we want to start with a file format for an entire canvas.

I would love to see that rapidly extended to copy-paste in the places where people want to do that.

I think that's eminently possible, especially when we are localizing schemas and types and versions to kind of subtrees or individual shapes.

If all of that exists at the canvas level, at like the root, then that's not so possible.

But if that's localized to individual shapes, then you can do it on a shape-by-shape basis.

That sounds wise. Yeah, with the file format, because to your earlier point of like if two people are collaborating and working in two different tools, it is the closer you get to sync is a nightmare.

But if you're saying, okay, we have to, here's the file, open up this file and now do some work, you know, that's more sustainable.

Okay. Notice we're at the hour or at the time we normally wrap up.

One other thing I'd like to point out too, in terms of like the timeframe, I know we had said, you know, six months or so was like sort of general timeframe.

We're also trying to get something going much faster than six months from now.

And as Orion pointed out, how I've said several times that working software is king when you're actually building, designing a specification, an interoperable spec, getting real tools interoperating with one another as soon as possible is the way that you actually develop the spec, not by kind of sitting in endless meetings and trying to think through all the different ways that this might work.

And so we want to try and make some good decisions, but we also want to get tools working together as soon as possible.

So Orion and I will be in Berlin next week together. And I think is Philip still here? Yeah, Philip is still here. He mentioned in chat that he'll be there as well for the Local First conference.

So we'll see you there. And our plan is on Friday to actually sit down and do some work on an initial draft spec that we could potentially implement for, say, TL draw, Excalidraw, but can also be implemented for other tools as well.

So we'd like to get something working in the next few weeks.

The other thing I was going to mention is to Michael from Codeflow and then also Jen mentioned Blender work.

If you guys want some help in getting started, let me know. Reach out to me. I'm happy to sit and meet with you guys and talk about how we're thinking about it or help you work through some of the things.

All right. The last thing I'll say is that I'll definitely commit to having a working demo of TL draw-Excalidraw interoperability before the next call.

Ironically, I think the reason I didn't quite get to that this time is because I'm actually doing tons more

 TL draw stuff now.

Yeah. Great. Awesome. Cool. I have a question. I don't know how many meetings you guys have had now, or you guys mentioned you guys have been working on it for a couple months.

I'm curious if there's more documentation on what's actually included, what are you guys looking to offer as far as functionality, etc.

I know part of that's obviously in this call, but I'm curious if there's some sort of confluence or documentation of just what you guys are thinking, what you're hoping to support, and what your goal is overall with it.

Are you looking to build something massive that the biggest diagramming tools in the world are going to use, or is this something for personal projects, etc.?

So the main resource right now is the GitHub repo. It's github.com slash ocwg, and there's also a canvasprotocol.org website.

But most of this is linking out to other things. The canvasprotocol.org website is intentionally thin.

Where you'll find the most information is under discussions under OCWG.

So there's both meeting recaps from previous meetings that have links out to the YouTube recordings for those meetings, but more importantly, there's these different topics around how to handle different use cases.

So there's a topic about coordinate systems and text formats and that kind of different thing.

So if you're curious about specific things, you can dive into these different topic areas, or you can open a discussion post yourself, and myself and Orion will certainly see it, and often other folks in the community have seen it as well.

And yeah, there's been what the next step from here will be this meeting will turn into a recap post that will have some of the content summarized from the meeting, and then any work that Orion and I do next week will also end up as a discussion post here.

There is also a Discord. If you haven't managed to find that yet, you can find it through canvasprotocol.org Discord.

If you want to real-time chat with people about this stuff, it's a great place to do that.

But we try to make the source of truth the GitHub discussions, and everything else is sort of a copy of that to make sure this is as public as possible.

All right, cool, cool. I appreciate it.

Yeah, no problem.

All right, guys. Thanks y'all for being here. We appreciate you all making time for it.

And yeah, if anybody has anything that they're working on in this area and would like support in that, Orion and I are available to jump in for that kind of thing.

Otherwise, we're going to be continuing to push forward on trying to get the Excalidraw TL draw piece going, and then some sort of draft specification that we can actually poke at that looks somewhat real.

Thanks, y'all.

Thanks.
