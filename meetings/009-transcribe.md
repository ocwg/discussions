Hey guys, welcome to OCWG meeting number nine, Open Canvas Working Group, and we're working on building an interoperable infinite Canvas standard. I'm going to go ahead and share my screen where we have a TL draw. We're taking notes. Oh, before I do that, a couple shout outs, thanks to Orion who's not here for facilitating the last meeting that I was not able to attend, and Michael for stepping in to help with some of the organizational and facilitation stuff, including writing up the summary of meeting number eight, which you can find on GitHub. That was very helpful for me in prepping for this meeting to be able to go get the summary from the previous meeting.

I'm going to go ahead and share my screen and share the TL draw. In case you're watching this recording and you're curious about this, you can find some information about OCWG on our website at canvasprotocol.org, or you can go straight to github.com/OCWG to find the GitHub organization, and then that will have links to previous meetings and meeting discussions. So this link here will take you to the previous discussion or sorry, the meeting summary for meeting number eight, and you can catch up on where things are there. And those meeting discussions on GitHub also have links to the recordings, which are on YouTube and the transcripts for previous meetings.

What we're actively working on right now is the spec for OCWG, and so you can find that at OCWG/spec. And then we're trying to do most of our work, even though we have a Discord for chat interactions between this group, we're trying to keep most of our things that we work on in public on GitHub discussions so that they're discoverable for people, they're also not kind of walled off behind Discord, and you can share a URL to them and all the goodness of the web. So if you have media stuff, feel free to discuss it in Discord, but anything that's media should eventually arrive in a GitHub discussion where it has like more accessible, cool.

So I'd love to give people who it's their first time in the meeting a quick chance to introduce themselves, maybe just talk about what you're working on and what you are interested in, why you're interested in OCWG. I'm pretty sure, Erin, I don't know if you were at the last meeting and would like to introduce yourself, but give you that opportunity. Everybody else I know has been at a meeting already.

Yeah, so I was at the last meeting, and I don't exactly remember who was at the previous meeting, but I heard you say that you weren't. So yeah, about me, I am somebody who's working on GLTF extensions with OMI Group, and the goal here is to increase imp to our probability for 3D content because the current status codes that you have to like reset up a lot of stuff every time you move it from one app to the other. To make an analogy with the canvases that would be like, if you tried to bring from one canvas app into another and you just had to like take each PNG file and move them over one by one. And that is very unfortunate, that kind of sucks.

So the idea here is that we can come up with a format that's interoperable so that we can just have that one format for exchanging data. And I think that the open canvas working group is a really cool idea. I think that we do need some kind of format like GLTF, but for 2D content, because GLTF is absolutely 3D only. And I might be interested in making a good old implementation of OCWG depending on whatever this format is called, I guess open canvas, whenever it's like getting to a more mature state and have a good idea of what's going to be in it. I have commented a little bit on it, and I also opened an issue about like the legal stuff, because that's probably something that used to be figured out pretty early on. But I look forward to this, yeah.

Very cool. So glad you're joining Erin. And yeah, discovering the GLTF community through Gen was, yeah, absolutely. It was so confirming in many ways because there were ideas that we had arrived at that just gelled so well with the way that GLTF is both structured from an extension standpoint and run. Yeah, I feel like there's still a lot we can learn from that community in terms of things that you all have already run into and how we should prioritize our time and effort. So glad you're here.

Very cool. Well, speaking of the legal and licensed stuff, maybe we can just start there in terms of the proposed agenda, and then we can dive into the other agenda items. I see there's one from Max, and then there's also just talking about where we're at with the draft schema. Erin, do you want to give us an overview of the issue that you created in GitHub and talk to discuss a little bit?

Yeah. So the issue text opens up with a bunch of questions, basically asking what is the legal umbrella which OCWG is under? I'm like, what license is it under to contributors need to sign a CLA or agree to an agreement? And these things are pretty important to figure out early on because everything that gets contributed is going to have to like be under this umbrella. And if all the legal stuff isn't figured out now, it can be difficult to figure out later. And if it's not ever figured out, then it could be difficult to get anybody to adopt this. And it's not just about like the license of like the work itself. It's also about like patents and stuff. You want to make sure that when you're building a standard, nobody is submitting something that's like under a patent. So like OMI operates under the W3C and the W3C requires that you sign an agreement that basically says that if you contribute something to the W3C, it's not going to be patent infringing.

Gotcha. Yeah, so the very short answer to all of your questions is that Orion Reed and I had the idea for this several months ago and initiated it and there is no legal structure whatsoever. And in terms of open canvas or the group, not opposed to doing the work and to setting something up, but it was just not something that was high on our list of concerns. I think one thing we were trying to be very intentional about was being as open as possible with the community aspect of things. So that kind of led to some of the decisions around making things available open source on GitHub, making sure that all of our communications are public in terms of meetings or recorded transcripts or public, and making sure that they're announced publicly, everything in Discord. There's like a single admin channel that's private where we'll do like logistics conversations that would be extremely boring to other people, but I have no problem with making that public even.

So I think that's been one of the principles from the beginning has definitely been as be as open as possible, but I think I like the framing of what you're coming out with this legal piece of like by doing the legal paperwork, we can ensure that it continues to remain open and viable. It's like, it's a way of maybe formalizing some of that openness. So that's a great point.

And I do applaud you, I applaud you for committing to this openness, because a lot of other groups, both open standards, open source, tend to operate with some level of closed doors. Chronos, MSF, Guido, Blender, I'll do this.

Gotcha. Yeah, no, it's been, it feels good to work this way. I think my inspiration has been a group called Vision that works on a couple of different specs that you can spec, there's a, oh gosh, what's the other, there's a couple of different specs that they've worked on. And I watched the way that they worked and said, hey, this works really well. Just borrow everything I can from them.

I don't have any special expertise in licensing. And I don't know if anyone that's on the call now has a good sense of that, or maybe Erin, this is something that we could learn from the GLTF community. Like is there a pattern that we should follow that GLTF has already gone through here?

I am not a lawyer. So I can't speak to the exact specifics, but I would indeed start by researching what is, what is it that the W3C does, what is it that the Corona group does, what is it that these other organizations do, and that might be a good starting point at the very least. It's possible that like you could just straight up copy paste like the W3C agreement and like just change the wording to refer to OCWG and then like, you'd be good. I don't, I don't know exactly what changes would be required if any.

Okay. I know someone in my network that I can ask in case, unless there is somebody on the call that has like special expertise and desire to like tackle this area. And also, Chronos is spelled with a H up to the K.

Gotcha. I was just noting that's what took me a long time to type it. I was like it's either CR or CHR or KR, but I did not guess KHR. Is Chronos the group that is, is that the group that surrounds GLTF?

Yeah, so there, Chronos is one of the bigger standards organizations. So they make GLTF the core spec, and there's a, of course, other groups like OMI that builds extensions on it, but Chronos also does things like they open GL, Vulcan, OpenXR, like so they do a lot of things actually.

Gotcha. I thought that name sounded familiar. I used to be a game developer literally 20 years ago. So yeah, I don't know if Chronos was around then, but OpenGL certainly was written a lot of that code, but a long time ago, interesting.

I appreciate bringing that up. Go ahead, Steve.

I think we do have to be aware of, when we're looking at the different standards that have this kind of process, we should be aware of the industry and the climate of that industry. I participated in telecommunication standards before, and there, companies got great pleasure out of assuming that everything they contributed was patented. When they got something in, they were like, “Yes, we got it in. Everyone has to pay us now.” But other industries might not have such a climate, so it does depend on the kind of industry that we're in, on how needed this is.

Yeah, that’s a great point. I think one of the—if you look at a lot of the companies that are interested in OCWG right now, a lot of them are themselves either open source companies or SaaS companies that take advantage of open source. So you’d have Obsidian, obviously TL draw, Excalidraw, React Flow, and these different open-source frameworks for canvases. And then you have the world of SaaS products like Miro and Muse and that kind of stuff that are open. But all of those companies, those SaaS companies, generally leverage open source and expect it to have a non-commercial license—the ability to use it without having to pay an organization. 

So I think, in terms of the industry that we're in, the industry will be very favorable to— I think the W3C is a great comp, actually, that we should look into, where it's expected that you're contributing to sort of a public good rather than something that you can guarantee patent revenues for your submissions to it. But yeah, like I said, I have a friend who’s very—this is what he does: open-source licensing. So I can reach out to him and see what his thoughts are on this.

Any other thoughts from anybody around this topic, particularly?

Yeah, I had a question regarding the patents. How do we know if we use something that's patented?

We don’t.

Yeah, yeah, that's true.

The basic thing to do is—there are licenses for code, for data, for documents, and our spec will be a document, and some of the examples might turn a bit more data-rich, but it’s mostly a document. For documents, all this copyright stuff is the easiest. There are certainly just agreed-upon licenses. Rule number one of licenses: choose a pre-existing license, do not roll your own license. It makes it too hard for other people to find out what the license actually is. MIT license might work. The most important thing if you want to give your work away for free is to waive any liability you can, like just disclaim it as "at your own risk." That's the most fundamental thing, and you can reuse it. And then there are some vanity clauses like, "Yeah, but if you use it, put our name somewhere." And the license that are just like, "Use it, do whatever you want." If we are that open, then licensing should be almost trivial.

And about the patents, there's no way we can foresee whether something we invented was invented elsewhere and is now patented.

Well, at a minimum, I'm not exactly sure the full extent, but at a minimum, we need to have something that asserts that if you are contributing to OCWG, to your knowledge, you are not contributing something that's patented.

That's a good idea.

You don’t need to scan the entire globe for patents to prove to yourself that it’s not patented. As long as you're not intentionally submitting patented stuff.

Yeah, basically you're pushing the liability onto the contributor, is my understanding of how that works. It’s like the contributor is basically saying, "I’m asserting that as far as I know, this is patent-free, that there are no patent violations." And so if someone does it in malice, they would be the one who’s responsible, the contributor who’s responsible.

Yeah, if you can have a proof set about it, at least you can try.

Yeah, I think in other words, they would be the one that you would have to try and prove it with, right? They would be the legal—well, we’ll see. Like I said, I don’t know that much about it. I should stop talking. 

But it’s a great thing to bring up, Erin, to make sure that we’re not running into unexpected roadblocks in the future that make it difficult for people to adopt. In fact, I think we might already have an MIT license in the spec directory. For some reason, I recall when I was sitting down to work on this with—nope, okay, we just had a README. I think Orion and I very briefly discussed throwing a license in there and then decided not to, which is—I'm glad we didn’t in retrospect. We can actually have a little bit more formal thought around that. But I think MIT was definitely the assumption, Max, when we were thinking about it.

Yeah, MIT is great. I don’t know of any problems with it.

I linked in the chat that OMI is using the W3C software and document license from the W3C because it's all under the W3C.

What are the advantages of that versus MIT?

I think they’re both very good, so just whatever.

MIT is great.

Great. That’s awesome. All right, well, moving on to the next item. Max, you want to talk about your set of things?

Yeah, I think we tend to mix some issues a little bit, and if we separate them, it makes it easier to think about them. So first of all, at the high level, what is an open canvas representing? What is it? Before we think about how can we store it in JSON?

So in my view, an open canvas in the simplest form is maybe like, you have little boxes on the screen, rectangles, and they show something that’s coming from somewhere. So we call these boxes items, and what they show, we call them resources, and that’s a super simple mental image that might serve as a guiding metaphor. And then of course, what are these rectangles showing? Well, some of them are showing images, some show scribbles, some show text, some show an arrow—whatever things you can see are in items. So we have items and resources, and resources are by resources as we know them already.

You do a REST request, get somewhere, you get back the resource or a representation of it. Now what we want to have is we want to store some resources in the JSON file, and some resources which are too large, we store them next to the JSON file on disk, and some resources that change too often or are even too large for that, they remain at their URL. So resources have different places where they can be stored. 

Now we only have to find out, okay, do we store resources in the JSON file? How do we store them next to the JSON file and somewhere have their metadata? How do we store items? And then we also have some structure between items, so don't forget that. But we have very few conceptual things that we actually want to store.

And then it's always about, okay, how do we store properties about items? And now we are in the field of extensible JSON. How can we have several tools dealing with the same item, deleting data from each other? 

And I looked around a little bit and brought up a proposal for JSON namespaces, posted it on Macon news only to get back here, that exists already, that's called JSON link data. And then I looked closer into JSON link data, and it's kind of true. I think we just want a subset of JSON link data because JSON link data really offers, I think, what we need, but more than we need. So I have to look into it more, but I think we can use a non-confusing subset that makes a huge difference without messing up our syntax.

I can very quickly, with a few sentences, go over how GLTF does references to these external resources, the files. So what works is that if in places where an external file is needed, there’s a URI property. And this URI property can be set to any kind of URI, but generally it’s referring to a file on the file system, and that file path is relative to the file. So you can set up the folder structure wherever you want. You can do like a subfolder for all the assets or you can just dump everything next to it or really anywhere else that you want. But you just have to specify where it is in the URI, and then the way that you give it context for what that is is just dependent on the context in which the URI is used.

So for example, GLTF has an images array, and each image is like a sub-JSON with a URI property and maybe a few other properties.

When you're saying GLTF has an images array, you mean that a GLTF node can refer to a set of images?

Let me just write it out here so that we're all on the same page.

Is images a top-level thing in GLTF?

Yes. So I didn’t include the absolute top document braces, but you could just put them there. 

And how does the reader know whether you're reading an image PNG or an image JPEG or what kind of resource you have to contact here?

Yeah, so what you do is you would have the URI here, and it can be inferred, but then you can also, in some cases, have a MIME type property, like `image/png`, just like that. And the MIME type is actually required in some other contexts. For example, if you want to store just like a buffer of data or store something without a file extension, that way it can understand what that data is.

Got it. Yeah, that makes sense. I think the difference with us would be that we would basically be saying—I think the way that we’ve discussed it so far, Max, look in your clarification here—is that we would have a nodes array, and a node, and that’s basically what you've been calling items in your description just now. That's the same thing. And then each item or node can reference a single resource, and that resource having a URI and a MIME type is more or less what I was hearing you say.

Yeah.

Cool.

Yeah, for the local file, do you use a file protocol or just a naked file path?

I think—oh, I see. Would you use this? I think what he's asking is, is it `file://` and then the local relative URI, or is it just the right thing?

It’s not, it actually is referring to a file that’s relative to the current file, but you could also do `http://` if you wanted to use remote.

Yeah, that’s a shame. So conceptually all resources have a location, a URI, and a content type, but in some contexts, you can deduce that this must be a local file. So this is a file scheme, or it has this extension and it was never given a content type, so it’s probably, if it’s `.txt`, this will be `text/plain`. So there are some MIME type mappings, some magic to shorten stuff.

We also want that because if we have like a normal text label in the main file, we don’t want to have to say, "This is actually content type text/plain." I'm saying that the content is actually "hello," so there we don’t even want to have a URI. We just want to include the resource in line in its completeness so that the content "hello" is enough.

It’s interesting that they made the choice to decouple the resources from the images, the implication being that multiple nodes can point to the same image.

Yeah, we should do the same.

And actually, what I wrote here, by the way, is a simplification because in GLTF, a node can't refer to an image. A node might refer to a mesh, which has a material, which has a texture, which has an image. And in GLTF, there are a lot of layers like this, and a lot of those layers may be just unnecessary for open canvas. But like the base layer here, of just having an image that refers to this, I feel like that’s meaningful, especially if you want to embed the image within the document. Like if you have, instead of a URI, you might have just like a stream of bytes here, you know, and that way, you want to be able to refer to it within the file without duplicating those actual bytes.

Yeah, that makes sense. I’m thinking about it from the user’s perspective. I just can’t think of—obviously, I could imagine features in a fictitious infinite canvas, but I’m having trouble imagining or thinking of a use case with an existing infinite canvas where the same resource exists in multiple places, effectively transcluded or whatever. Like the same resource is being used as the resource for multiple items.

This is common in GLTF. I don’t know about a canvas, but I would be surprised if you wouldn’t want to allow that as a thing to do.

Yeah, even if you duplicate an image, you know, a thousand times, of course. Like in a moderation way, you have a sticky note image, and you use it over and over again—that’s quite common.

Oh, okay, okay, I see what you're saying, Max and Steve. Like if you’re—got it. I was thinking more of—yeah, so system-level things, like an example, like the sticky note image is a great example. Or, yeah, a star. And obviously, this is better represented as an SVG or whatever, but like, yeah, here’s the sticky note image in TL Draw. And so, yeah, obviously, that’s probably not an external resource. That’s actually a CSS thing, but I see what you're saying—like a stamp would probably be a better example, a stamp that you’d want to reuse in multiple places.

And, yeah, okay, I'm with you.

The thing I don’t like about it is that one of the goals that we talked about early on was making an open canvas as human-readable as possible. Not that humans would be reading it—this is mostly machine-readable—but it should be comprehensible. And it’s—which is why we chose JSON over, say, XML and some other things. So decoupling the resource from the node means that you have two places to look.

Well, we have two worlds. We have the data format on disk, and then we load it and then we have the conceptual world. Conceptually, we have nodes showing resources. But in our syntax, if a resource is only used in one node, we could have an abbreviated form where you can just inline it in semantics. Why not?

Yeah, I would definitely appreciate that option for inlining if you're not going to reuse it.

And then you could potentially have an empty resources array or images array if all the objects are only used once. Like, if you look at this canvas right now, there’s no repetition on the canvas that I’m aware of. If anyone can see it, point it out to me. But all of the items in this canvas right now have their resources embedded.

The arrows are...

Arrows are, well, just this point. Basically, single-use images are common enough where you're thinking that you want to include a special thing for that in Open Canvas just for embedding the image directly there in case you don’t want it to be shared.

That makes sense, yeah.

And text is a resource type. So another thing to note about arrows is, like, we’ll have multiple ways of implementing them, but the current thinking on arrows is that they won’t be implemented with an image element. They won’t have a resource, effectively. They’ll be implemented purely theoretically, which leaves it up to the renderer to decide how to represent the arrow.

Now, the wrinkle there would be, what about this thing? And the answer is, this is not an arrow. This is a shape, right? It happens to be shaped like an arrow, but it does not have the ability to connect two items.

So the other piece, and we should like, we can look at the spec to talk more about this, but the other thing about arrows is that they imply a relation between nodes. It’s not implied; they specify a relationship between nodes that we'll encode separately.

So the other piece that we have going on that, as far as I know, GLTF does not, is that in addition to items and resources, there's also a relations array that is purely conceptual and will not be visualized unless a renderer chooses to visualize those relationships between the items.

So that goes back to, like, popping all the way back to where Max started, which is, what does a canvas represent? A canvas represents items where each item displays a resource.

Go ahead.

Should we once and for all clarify whether we call them items or nodes and just stick to one, because I think I confused it. You started with "node," and now I brought in "items." Let’s just fix it to one term.

I like "nodes," and everything else that we’ve been saying in all past meetings and in the spec says "nodes." So let’s stick to nodes.

If there’s ever a move to replace "nodes" with "items," we’ll just need to do a find-and-replace across the project. But for now, it’s "nodes."

The convention across the game industry is that if it’s a thing in the scene tree that has a transform, it’s called a node.

Oh, good. Okay. Then we’re in good company because there will be a potential transform with the nodes as well. So, yeah, it is a thing in the scene tree, as another way of saying what nodes are. And nodes optionally have a resource, and as we were just discussing, resources can be inline and embedded in the file. Or they can be specified in a separate array we might call resources. I think it’s maybe resource. I do like that.

I like that too.

Max is giving a thumbs-up.

So we have these resources. You can have it referenced in a resources array, and it’s stored separately, or you can inline the resource underneath the node. And then the resources are either embedded in the file, next to the file, or remote in the URL. And I do think this is a sensible way of doing it. Like, we were just talking about the URI, whether we have a `file://` parameter for files or whether we infer it when there is no protocol at the beginning. I’m ambivalent on that.

And then, yeah, Max was noting that MIME types should be implied based on extensions for the URI.

They can be implied, yeah. Just as a convenience. Conceptually, every resource has content and a MIME type, but depending on how we put the syntax, we could infer it.

Yeah, the way it works in GLTF is that if there’s a MIME type, the type is the MIME type. Otherwise, it’s inferred from the file extension. And if there’s neither a file extension nor a MIME type, that’s invalid.

Very cool.

What if it’s an unknown extension type? Is that the same as being invalid?

If it’s unknown, then it can’t be read anyway. Like, maybe if there's a WebP, and your app can't load WebP, then you just can’t load it. So only other extensions are going to be loadable.

Well, you can also discover file types based on the first magic bytes in the file.

If you're relying on the magic bytes, then the GLTF side would say that you have to include the MIME type as the explicit property.

For HTTP, too. With HTTP, you always get the MIME type.

Yeah. HTTP returns a MIME type to the client.

Oh, that’s part of the request—I mean, the response.

Yeah, that’s the content type—it could potentially say.

Yep, that's interesting. I hadn’t thought about that.

Okay, and so the way that we’ve been talking about nodes versus relations is that nodes are the visible elements on the canvas, and relations are the abstract relationships between nodes that are not necessarily visible. That doesn’t mean that they’re never visible. The renderer basically gets to decide whether to visualize them or not and may or may not create them based on things like arrows, which brings us back to that conversation about arrows.

So in TL Draw specifically, these two items—these two nodes, this text node and this image node—in TL Draw’s export format, not in Open Canvas (because they don’t export Open Canvas yet), there is a relation between these two objects that’s specified by this arrow. So the conceptual thing is captured in TL Draw, is my point. It’s not captured in all canvases. In fact, I’m pretty sure Excalidraw doesn’t capture it as a separate thing, but there are certainly canvases out there that just represent this arrow and its location, and kind of where—like its bounds—but do not specify a relationship between the two nodes that it happens to be close to or kind of points to.

In order to bring these two ways together of how to represent arrows, are they like a relation or are they like a node?

Thank you for asking. Yeah, we need to say, "Well, this node is actually showing this relation."

Yeah, and so what we’ve said so far is that two things: One, this is why we want to enable extensibility so that nodes that have a relation associated with them, like TL Draw arrows, would be part of—you could use a TL Draw-specific extension for defining a TL Draw arrow that assumes a relation. And maybe we could generalize it to where it's like a sort of top-level thing that’s like "relation arrow" with relation or something along those lines that has those properties if it turns out to be more general than TL Draw.

But we also would want to enable arrows that don’t have relations. It’s not a required property for arrows. And so this is kind of where we’re getting to the point where we want nodes to be defined by a schema. And the schema is something that individual canvases can choose to extend with additional properties, and that gets to the final thing that you were talking about, Max, where nodes can also have properties about them that we need to store and make sure that we don’t collide and stomp on properties—make sure that you maintain them even if you can’t read them. This is the property bag piece.

So I don’t think I’ve said anything new, or that we said anything new that we haven’t said in past meetings, but it is, I think, a helpful summary. I’m glad you brought it up, Max. Obviously, the devil’s in the details here, so there are probably some detailed questions that pop out of this. But does this summary kind of bring us all back on the same page or get us all on the same page?

More or less.

I have a question about relations. Relations can also be used for groups, sets.

Yes, that’s right.

That wasn’t a question, that was a statement. Or maybe it was a question, and I missed it.

That was a statement.

Okay, I’m happy to answer it as a question, though.

In the current—actually, this might be in the PR—yeah, it looks like it is. In the current PR, there is a mention of, I think, three different kinds of relations. Let’s see. Yeah, core relations are sets, which are groups, edges, and hyper-edges, which are basically the three different types that we’ve identified so far.

I’m thinking of some ways to break it, and one that occurs to me is a door. Doors are kind of like an arrow, but they relate to one thing. Like, I had software, and I had to make a room, and people wanted to drag a door onto the wall. So this door is associated with that wall, but it’s not an arrow between two objects. It’s just associated with one thing at one particular location. Would I use a relation for that?

Yeah, why not?

Yeah, can you use a hyper-edge that has one endpoint?

Or a set, so it just fits within this.

Right, if it just had one room that it went to, then that could be—that’s basically a from-to relationship, as far as I understand. It’s like a relationship between the door and the wall node.

Yeah, you just create another edge for it.

Right, exactly.

This is something that sets, edges, and hyper-edges capture well, but there are always potential edge cases.

One edge case with hyper-edges, though, is that if you have a hyper-edge that has some incoming nodes, some outgoing nodes, and some undirected nodes, you can't specify the undirectedness at the hyper-edge level. You need to state it at the endpoints.

So "from" and "to" are not enough—you need some kind of undirected attached to them as well in order to model that.

Yes, I’ll take your word for it. Hyper-edges were an entirely new concept to me when Orion explained them. So I defer to him. He’s our hyper-edge expert.


Hyper-edges were an entirely new concept to me when Orion explained them. So I defer to him. He’s our hyper-edge expert and lover. So, yeah, you are probably correct.

I do have a question now, actually. Can a resource contain a canvas itself?

Of course. Conceptually, if we can serve canvases over the web, then they are a resource, so they can be included, which is actually... well, cool. Also, they can be embedded in line.

Yeah, they could. That’s a really good point to bring up.

And I will say that that's something many people in the GLTF ecosystem have noted as being missing—that a GLTF can’t refer to another GLTF. It would be nice if Open Canvas came with that ability by default.

Yeah, and there are several examples of existing infinite canvases that effectively support embedding canvases where you can zoom into a canvas deeper, zoom into another canvas deeper, zoom out. Muse, the desktop app, supports this, as do several others.

Yeah, in my own tool that I'm building, I have compositions, and there are multiple compositions on the same canvas, but they are the same composition under the root.

I see what you're saying—that’s another great example of transclusion.

Very cool.

Yeah, so there was a question here in terms of the status of the draft. What I was just showing is the draft in the "initial draft" branch of the spec. It should be on the repository, which is... this is a fork of the one with the JSON schema.

Oh, wonderful. Michael, you and I should work on bringing that into this one then.

Yeah.

Do you have... did you fork off this branch?

Yeah, but I think I have write access to this repository, so I probably can make a branch directly. I will do that.

That’s—yeah, open a PR. I’d love to review it, give feedback, and bring it in.

Great point. This does not represent the only work that’s been done on the spec. Michael has a branch off of this that has some JSON schema additions. The JSON schema stuff is definitely missing from this.

I guess one question would be, when we initially started working on the spec itself, we assumed that the pull request would be a place where discussion could happen, like long-running discussion, until we brought it in. I noticed that Aaron has left some comments on it as well. It feels like we’re at this alpha point for the spec where merging it back to main and appropriately adding a disclaimer at the top of the spec—something like "Spec is not done, this is not a 1.0, but here it is"—and then doing more smaller PRs against the current document feels like a good move. The spec has gotten quite large as we’ve been working on it, so it feels like shifting to that workflow might be timely.

Does anyone agree or disagree? Should we keep this PR open for a few more weeks or months while we work on the spec and use a single PR?

Yeah, I think we should look at the discussion we just had—the longest discussion—about whether the current spec still matches what we’ve discussed. It does a lot of things, but resources aren’t yet in the spec, so that’s still missing.

I've got some resources already in the schema, but they’re very limited.

Yeah, no, the resources stuff is not as well spelled out in the spec. It’s mostly been discussions over the last several meetings, and particularly Max doing some digging and bringing stuff to light, so I need to make it match.

In my opinion, it’s perfectly fine to merge what you’ve got so far and iterate from there with more changes, as long as you’re following the golden rule of Git, which is to go from one working state to another working state. You don’t want to merge the PR if it’s inconsistent with itself. So if the schema describes a property and that property isn’t in the prose of the README, that’s nonsense and can’t be implemented.

Great point. Yeah, and I definitely follow that rule for software. This is my first time working on a spec—I’ve worked with specs, but never worked on one—so this has been fun, thinking about how the process aligns with my software workflow.

That’s great. Yeah, we can definitely do that. At this point, the spec is small enough that I can hold the entire document in my head, which is really nice. I hope it doesn’t get much more complicated, but I can take the work, especially now with Michael stepping up and helping with more of the logistics. That means that after this meeting, I can let him handle turning this meeting into a GitHub discussion with all the associated materials, and I can focus on making sure the spec lines up and merging it back.

One other bit of news: Orion is moving a mere hour-and-a-half plane ride from my house. So there’s a possibility that Orion and I could get together and do an in-person work session for a couple of days because I feel like we could make a lot of progress, especially on building a working implementation that actually implements the spec.

Alright, I think we have two other items. Oh shoot, it’s already 12:56. I haven’t had a clock in front of me because I’m not in my office. Aaron, do you want to discuss transforms real quick? We’ve got about five minutes until the end of the meeting, and I can stay a few minutes after.

Yeah, so just briefly: one of the most fundamental things about any kind of format that describes a scene, whether it’s a 3D scene or a canvas, is the positioning, rotation, and scale—the transforms of objects. This seems to be, aside from the name of the object, the single most important, fundamental property. If it were me designing the base spec, I would have everything related to transforms in the base spec, not in an extension. I see here that rotation is specified in an extension. To me, rotation is a pretty common thing, and it’s going to be defined by many people. If it’s not in the base spec, I would put it in the base spec. Aside from rotation, there are other considerations with a canvas-based format, like size, maybe anchors or offsets. I don’t know exactly what’s in scope for Open Canvas, but anything transform-related that is common and universal should be in the base spec.

That’s a good point. Orion and I debated this back and forth, looking at existing canvases to see what they supported. Some store X and Y as separate vectors, while others store them as arrays. It’s been a question of how much we want to simplify.

Yeah, in GLTF, you would have a position array with X and Y in it.

I could see that either way. One of the considerations we made was around brevity, like making it shorter to specify one of these nodes and not having a ton of required properties at the top level. That’s why X, Y, and even leaving out rotation was done. Some canvases literally don’t support rotation, and that was another reason for making it part of an extension or on a node-by-node basis.

Well, there’s a stage between being an extension and being a required property. What Aaron says makes sense—we should make rotation standard so we don’t end up with different definitions of rotation in different extensions. That’s why you want it in the main namespace. But it doesn’t have to be a required property—we can leave it out for items that don’t have a defined rotation.

Yeah, you would define the default rotation as zero. So if it’s not rotated, you don’t specify rotation. If you’re importing into an app that doesn’t support rotation, you discard it.

Exactly. That’s inevitable, unless you control every client app that uses Open Canvas. There will be different implementations with different feature sets. So there will be some loss converting, and that’s just inevitable. You just have to accept it.

Yeah, I’d say it’s actually desirable. Some canvases are designed to be simpler, and that’s their selling point. For the end user of that canvas, loss of features may be a good thing because it gives them less to think about and lets them focus on what’s important.

Absolutely. From the user's perspective, they really wouldn’t expect to import some canvas with rotation and then get rotated items, even though their own app doesn’t support that. It would be weird if imported files could do more than the app.

Yeah, as long as the format allows both sides to do their best. So, you export something with rotation, and when you import it into an app that doesn’t have rotation, it won’t have it. But if you import it into an app that does, it will. You don’t want the format to be the bottleneck.

Exactly. This makes sense.

The one thing I’ll say is, Max, we should come up with a solution for handling multiple extensions on a single node when they have the same property name.

Well, there are several possible ways to handle that. I think we had the idea of one property bag per extension at first. Then each property bag would have the actual properties nested inside. Now, it’s an extension array, and each extension object in that array has its own set of properties. The way GLTF handles it is simpler and more elegant—they just move everything into the same property bag, but use prefixes on the property names to distinguish between them. So, every property in an extension has a vendor prefix, like "vendorName_rotation" or "vendorName_scale."

In JSON-LD (Linked Data), they take it a step further and say that the prefixes should be mapped to full URIs. It’s similar to XML namespaces. So, instead of just using a short vendor prefix, you have a globally unique identifier. JSON-LD embeds the mapping of the prefix to the namespace URI directly into the file. This ensures that extensions don’t conflict with each other.

The GLTF solution works well because the vendor prefixes are registered globally. That way, only one vendor can use a particular prefix, and there’s no conflict between extensions from different vendors. All the properties are under something like `extensions/vendorName_propertyName`.

Right, so there’s a registry ensuring that the prefixes are unique. That might be a cleaner solution for us because we already have the concept of namespaces with things like `@OCWG` in our schemas. JSON-LD generalizes that and maps the prefix to the full URI right in the document, making it fully decentralized.

If we were to use JSON-LD, we’d basically be adopting an existing, well-understood mechanism for namespacing and extension management instead of reinventing the wheel. The question is whether we need to go that far for our use case.

Got it. Thanks for explaining that, Max. You’re probably the first person who’s made it clear to me why JSON-LD might be useful for us.

The way GLTF avoids name conflicts with extensions is by having a central registry for vendor prefixes. Each vendor registers their prefix globally, and all extension properties are namespaced under `extensions/vendorPrefix`. This ensures there’s no overlap between properties from different vendors.

That makes sense. You have a registry of prefixes, and it’s managed by an organization to ensure uniqueness.

Yeah, and that might be a better approach for us because it’s essentially the same thing as what we’re doing already with our schemas referring to `@OCWG`. In JSON-LD, they generalize that concept and map the prefix to the namespace in the file, so it’s fully decentralized and standardized.

We could look into that, but for now, I think using a vendor prefix approach like GLTF might work well for us.

Yeah, GLTF has a pretty good solution for this with its centralized registry of prefixes. We could follow a similar model, where every vendor uses a prefix for its extension properties to avoid conflicts.

If we stick with the GLTF-like approach, we’d use the prefixes as namespacing for each extension. That way, we don’t need to worry about multiple extensions colliding on property names.

So, in the current version of the spec, I’ll leave out the more complex namespacing like JSON-LD for now. I’ll just note that conflicts between extensions are possible, and we’re considering various approaches to handle them. I might reference GLTF as one approach.

Sounds good. I’ve implemented something like this in my export to OCWG draft, where each extension has a separate property bag, and the properties are namespaced using a prefix.

Got it. I’ll review that and bring it into the current spec.

We’re a little over time now, but this was a great discussion. I’ll take on the task of reviewing the spec and making sure it lines up with what we’ve discussed, including merging in the JSON schema work.

Max, if you dig into JSON-LD further, feel free to create an issue on GitHub to discuss it, but no rush—we’re not blocked on that. We’ll just keep it in mind as we go.

Thanks to everyone for joining, and we’ll aim to have another meeting in two weeks. Michael will handle scheduling, and I’ll make sure I get my homework done by then.

Thanks again, Aaron. We appreciate your input, and feel free to join future meetings as you can.

Thank you! I’ll try to attend regularly and contribute where I can.

That’s awesome. Thanks, Aaron. Thanks, everyone!

Bye, all!

**End of meeting.**
