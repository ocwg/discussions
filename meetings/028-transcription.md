That was just preparation, I copied the spec over to a new folder, renamed to version identify so that we can start doing something actually. Beautiful, beautiful. Yeah, start changing 0.051 draft.

Okay.

So, so, so, so, I did see Max that you pushed a couple of minutes like right before this.

Yeah, but that was just preparation. I copy the spec over to the new folder. Renee to version identify so that we can start doing something actually.

Okay. Let's see.

Yeah, so last time we met, we released 0.05. It seems like if I'm stretching back my brain to the meeting before local first comp, there was some discussion about nesting canvases which did not make it into 0.5. Am I remembering that correctly or did it actually make, did it actually land?

In primitive ways, you can always nest canvases by giving an item a resource, which is a Nokia file. But it's not explained in the spec at all, how that works. And if you nest an okif file, you have to wonder how does that nested okif file get represented. Presumably that resource would be like attached to some node to place it somewhere in the scene, but then what does that node correspond to in the other okif file.

And this was briefly discussed at last week's meeting, or three weeks ago's meeting, the last one, which I wasn't able to attend, but I did watch recording. And in response to that, I did open up a GitHub issue discussing this if we want to spend some time on that.

Yeah, I think that I think the real question should be like one of priority, like that does feel like an obvious way to improve the spec. But is it the most valuable thing we could be working on right now? I'm not sure. It feels like it feels like right now the most valuable thing is more implementation, more complete implementations supporting okif.

And if I if I could throw all my chips on one number, it would definitely be a obsidian canvas to okif round trip. For a couple of reasons. One, I feel like the obsidian canvas, the obsidian community is like very well aligned around like files as being important and all of that kind of thing. And so they, I think from a values perspective, they kind of get it already.

And so that that's helpful. Also, there's a lot of obsidian users somewhere north of a million people using obsidian. So, I'm sure that obsidian canvas as a feature within obsidian is a much smaller use case, but it's still, I think the Excalidra plugin is the second largest second most installed plugin in among all obsidian plugins. So like clearly canvases are a really big use case inside of obsidian.

So that's one, one reason why I would say obsidian canvas to okif and round trip makes sense. The other reason is that obsidian canvas is just a really simple canvas. There's really not many features. And so having full support there is actually much more attainable than going after something like TL draw, which actually is pretty robust or something far more robust like a Vizio or that kind of thing.

But I think having that one, like starting to build around a single implementation that is already useful feels like a way that we could learn. We could learn that things that are closer to core than like embedding canvases is are actually not working well and we should fix those.

The other sort of open issue is having a root item. We also haven't finalized that.

That's right.

Yeah, I think there's a discussion out there for this one.

Right.

It's kind of touched on in the issue I opened. My suggestion was to reserve the node index zero for the root, but there's some questions of like, is that the best approach or is that like the okif style approach because you. Okif doesn't really use indices for anything else. So should there be some some special uid for our roots, but then two different canvases.

Yeah, like I don't know exactly how this is going to work with okif. Yeah, we sort of a new property that says root item or whatever is this ID. And then then it's not adding any magic strings.

I think we had one meeting where we discussed magic strings, magic indices or explicit link, and then we settled on the explicit link. Maybe that was the one where you were not there. I don't know. Having some kind of just property that says the node with this ID is the root mix a lot of sense to me.

And I think the most explicit. Easiest for LLMs you know.

True and human readers as well. And yeah, it is. I think we explicitly at some point we had the conversation around magic strings as like a. Anti pattern or a design decision of like we're going to try to avoid magic strings wherever possible.

So, so yeah, that'd be a good instance of that. Seems like a reasonable thing to respond to.

Yeah, and then there's there's also sort of like the root transform piece.

Yeah, I think Michael my thinking so Michael dropped in chat. And for those who are watching the recording, the Jason validator website that he had. Vibe coded slash worked on. And there's a there's already one that does Jason canvas to okay. Does that direction.

What I'm thinking that we need to get in place in order to enable people to more effectively contribute and adopt is having. Like a well set up library. And I actually have a plan for this that I worked with an LLM to generate.

Of like how would we have a library that. Pushes to NPM that is like well named that has a CLI tool around it. That that the that is in a mono repo that has you know all of the properties that we would want from like a well set up repository.

If people want to contribute we could be like oh you're working on an obsidian or an oak if to TL draw. Like put it here like in this directory. And then here's how you would like add an option to the CLI tool to be able to use that and get like get people into an iterative flow.

Here's where the test suite would live right like having all opinions about all of that. I think we'll make it a lot easier for people to contribute as well as it'll make it a lot easier for LMS to do this work right.

So we have a well structured repository asking an LLM to generate the code to do you know around trip or what or to or generate some tests suite. We kind of know where things live.

I think that's a great goal and I only suggest to approach it more agile so we just build two tools. And we align their structures where we place the test students on and from that we extract how the other tools should also behave in the same way.

Because top down is harder to guess how to do things well. That's at least an error I often made so going bottom up is just quicker.

I think it's a practical approach where you're looking at the actual implementations and tools and learning lessons for those is a good idea.

Yeah, if you have a CLI tool for like, okay, to Jason canvas and then another CLI tool in a different repo for Jason canvas to. Okay, no, it can be the same repo. Why not.

I wouldn't even start with a CLI tool, maybe start with a library. I mean, what is the core, how maybe we start with what Michael has already so he has a working app, which sort of contains a library, maybe not explicitly factored out.

But there should be something that is a library. So how could a guy like Michael download that library from another repository what what needs to happen so that.

Okay, we make this library this way so that you can just put it into an app. That's set up you will learn how these libraries need to be shaped, maybe.

If we make that money report, but with the plan that just has, then we can add separate packages, separate apps for the implementations and the library as well.

There are a lot of tools that can do that easily. We just have to choose the tool.

I have some experience with an X, for example.

Oh, it looks like here it is monorevo plan docs. Yeah.

This is Jim and I going crazy on like how to generate the library. It's fine to be inspired by that, when when setting up the initial attempt, but just not.

I not get lost in the 17 stop file it when.

Yeah, that's a great point.

Yeah, I think a good, a good near term goal.

It brings it even nearer and is aligned towards the oak if to Jason canvas use case would be like you mentioned Max extracting the library from Michael's as a starting, Michael's app as a starting point with the intention of basically now that we've extracted it to this library over here

we can just import it back in and now we have literally we haven't broken anything. We just, we've just proven that we can give someone a library that does something now we can go improve the library, which like doesn't change anything for the validator

every time we release a new version of the library, we can just, you know, refresh the library and the validator. And I think that enables us to learn more about the real issues. And also as soon as we have two libraries doing something with the oak if some urge will emerge.

What is the shared stuff. What's what is common to all these oak if I was what are the common oak if core tools. And I have no idea yet what these are.

Yeah.

Yeah, it turns out that the software engineering principles for using agentic coding techniques or the exact same software engineering principles that you should use when working with humans.

They turn out to just go faster because the L M can go faster than humans.

Crazy.

L M is like a junior software engineer with a lot of caffeine.

And an autistic one too.

It's not so good with humans, but it's very good with it takes that.

That's a good and also very forgetful like wakes up every day and has forgotten everything from the day before you have to like point out everything back out to it again.

Well, I'm going to make Max you have been christened the host of this meeting.

As I mentioned in discord, I actually have to run to another meeting, but you guys can continue using this one and the recording will continue as well.

And I'll try to catch up on the last half hour.

Had another meeting come up that I have to attend that I can't reschedule.

So I'll see you guys.

And good luck with your Friday demo. Thank you.

All right, so we have this library thing.

What is what is the real step we can make so that we have a working library in the mono report that can be imported from the validator.

I'm not a TS developers are really don't know what needs to be done.

Finding the time.

I can do I can do it without problem.

Is it totally clear for you how what the expectations for the library are.

Yeah, yeah, quite quite well.

I can set it up as well, but we can work from there.

It's more it's more time issue to find the time and start because I've only tried, tried finding your time with Queens yet.

Yeah, you're already spent a lot of time. So that's.

Okay, so then the next productive thing we can do in this meeting is maybe to define more about this route item thing.

Yeah, we'll do that, I think.

I will try to start with with the mono ripple, the library.

Before next meeting so.

As for the item stuff, I'm happy to discuss it, but I should note that I have most of my thoughts pretty much written down in the issue.

So.

Do you think maybe Max Michael, and you know, y'all can just take it from there if you want.

Whatever, whatever we want to do. That's okay if like, you know.

Yeah, so how do we call the property.

Well, the roots item is it.

Should be root node, maybe.

Or canvas node.

I guess the root node would make sense.

Michael.

Yeah, I think it sounds that root node is really obvious, I think.

Okay, so I can obviously edit the spec.

And also one thing we should decide about.

Is if we have like we have this kind of expectation that oak if nodes are just by default, like just like at the top level.

And you do like parent child relationships to make them like the children.

So we should probably explicitly.

We will need to explicitly define that if there's no relation, if the node isn't explicitly a child of something, then it should be a child with the root node.

Yeah, that's a very.

Same idea.

Do we allow to redundantly also state that it explicitly that it is the child of the root node, although that's implicitly already there we have some of these hacks already.

Well, if if I was, you know, building an importer and I came across that data, I don't see any reason I wouldn't be able to parse that.

So I guess it could be a lab, but it would be redundant.

So yeah, just so in examples to make it explicit and then saying the comment is actually inferred anyway.

Yeah.

So, so the spec would say every node that has no parent does have a parent, namely the root node.

Right.

Yeah.

Okay, and is a root node required in a canvas?

Or can we also get around that?

That's a good question.

So you could it some apps need to have a root node.

So you could all you could say like, oh, if there isn't one defined one would be implicitly generated.

And then some apps don't have that right so I'm not exactly sure how it'll work there if there is one.

But regardless, I think that we have something will typically represents the oak if documents and whether that there's a node associated with that.

Some apps there needs to be and we think one we can be generated implicitly.

But then if this property is defined where there is a root node and that root node represents the document.

So if I'm parsing an OK file and then either root node and there's none defined, I just create one because obviously there's no information yet about formatting or anything so I just make one up.

Yes.

This is this for precedent. This is like, what kiddo does when parsing, gltf files.

If there's no explicitly defined root node, we just make one.

And do we have like built in settings like the default font size, which propagates down from the root node to all other nodes by default is 12.

Is that built into respect?

That's a good question. I don't know.

A little bit like what the HTML default style sheet does. It defines some defaults for margins and font sizes.

And that was a design principle of off-kiff, correct to that. Once a node has some kind of theme attached to it, that theme like propagates down to its descendants.

So therefore, if you want to have a document wide theme, the straightforward way to do that is just to put the theme on the root node.

Well, yeah, yeah, that was the idea. We haven't defined themes yet, but yeah, that's how it should work, I guess.

And then if there is no theme defined because the file is so small, experimental or whatever, then there needs to be some defaults.

If you have no root node, then God gives you font size 12.

Yeah, that does need to be defined, yes.

So we need to, I mean, the other settings are easier, like the default scale factor is one. The default rotation is zero.

The default colors may be black on white or maybe not.

Dark mode versus light mode.

What's the default of the default? Okay.

Yes, this is enough to draft the first thing about root nodes.

There was a question from G, I think, no, somebody else on the chat said the node transform was weird.

We have moved scale into the node transform extension, but rotation wasn't moved.

And.

Yeah, honestly, I don't know why haven't we moved rotation over into the root into the node transforms.

Should we.

No transform was for relative nodes, relative positioning.

And rotation is, in that regard, an orthogonal concept.

And right now, a rotation remained a core property of visual nodes.

And that distinction maybe feels a bit weird.

But okay, it's not a huge problem. We can just document it better.

But is there like a clear justification? Why one is standard and one is extension?

I think the reasoning, if I recall correctly from the previous meetings, was something along the lines of that you can use size instead of scale if you just want the global size of that object.

But scale is kind of inherently a thing that affects that node and all the sentence, you know.

So it affects, you know, the sentence position, no, it's relative positions.

But rotation does make sense that's its own like global rotation property, right?

So the match as well with the nose having a position.

Yeah, I mean, position and it's a good explanation, but position and rotation also affect all the sentence.

I mean, okay, position needs to be core property. So.

I think this is just how things are.

It needs to be documented better, but there's no very hard criteria.

Why it's exactly this way, because it can.

Yeah, scale clearly belongs to this parent child problem.

Scared is useless without parent child. That's maybe the thing in rotation, like size, as you said.

And position can be used without parent child.

Okay, that's.

That's what I can write. Okay, so we more or less thought that.

Isn't it now super easy to define nested canvases.

I would think so as long as we have the transforms figured out and we are going to do a root node property.

And at that point, it seems pretty straightforward to have nested canvases just do it. We're done, right?

That's just one thing. We have a note that says my resources and ocafile.

And that ocafile says I content a root node, maybe.

Then what's the relation of this importing node to the nested node?

They are the same node.

So essentially what happens is like, that's clever.

Yeah, so the node from the document gets generated and then placed in that node's place.

So an effect and if there's any properties on the instance of the node, like a position,

that's will like override the what was in the file.

So that way you could have, you know, the same ocafile have it instanced three times in three different places.

And each one has their own position.

So the master parent, the parent node overrides the imported nodes properties.

Yes.

Yeah.

Yeah, I think I think that's the magic thing. It's the same node.

And the overrides.

We have another instance where overriding happens already if we have parent child with inherit properties or something like this inherit.

That's where we can steal this inheritance mechanism from, because we also have extensions and then it's not so easy to define extensions override each other.

But I think we should have defined that already somewhere where, and I can see from that.

Excellent. Yeah. Okay, I can, I can use that for draft.

So if I understand correctly, the nest converse that will be the nested converse itself will be your resource, not defined inside the main nodes.

As long as it's in the, in the same nodes, then it's just the same canvas. I mean, there's no benefit.

I mean, what's the difference between a nested canvas and a nested node in this view.

Yeah, I was thinking that if we have this root node has probably also has a special type.

Or give converse slash convos, something like that.

And that you could have a note of that of the same type, which is the starting point of.

Of another.

Yeah, of the nested combo itself.

I'm not sure whether we need a canvas type special note or not.

I have no intuition on that yet.

Maybe.

And then you say, what if we have multiple of these special canvas nodes.

Well, I can only answer that when I understood what a canvas node is.

It is different from a normal node. Maybe it is the same.

That would be beautiful. If we don't need a canvas node.

And if every node can define things with propagate down, then any node can clever role of a.

Of a root node.

Yeah, so what this can, they, I would say they are the same and that also means that, you know, if you're.

If you have some, some scene in runtime, you can just take any node and save that to an oke file and save that subtree as its own oke file.

So you can any, any subtree of nodes can become an oke file needed.

Yeah, and.

What happens to an oke file where we have a tree of, of parent child and the root node is not the ultimate parent, but some other node.

So what is the root node of the canvas has parents.

What, what does that mean?

Uh, it doesn't.

Um.

Here, let me, let me, uh, let me get a little diagram out.

We could do like a screen share or something.

I mean, we can say this is, uh, I have to allow now.

Okay.

Now you should have the right to share.

Yeah.

Yeah.

All right.

Um.

Uh, hey, have the zoom interface changes.

All right.

So let's say we have, um,

we'll have a node and then there's another node as a child of it and another node as a child of it.

And another node as a child of it and some, some like long nested thing.

If you, for example, wanted to save this node as, uh, let me change colors.

You want to save this node as its own oke file.

Um, that this whole tree gets saved as the oke file.

Um, that, that's perfect.

That makes a lot of sense.

And there's, there's more, you said it's not the ultimate root.

So like there's still like these that don't get saved.

And what ends up, uh, if you want to use this oke file,

then the, it get, what, what uses it is effectively a tree of nodes.

It looks like this where this node is kind of present in like in both.

Uh, where it says like, Hey, I'm the roots.

Um, and, uh, it has any like inherent properties, but then like transform properties will be specified inside of this.

Uh, this scene, which is instancing it.

So the, the, the transformer of the root node in, in the, in the oke file, uh, is, uh, is zero or it's the identity transform because the root of a canvas isn't transformed relative to the canvas because that doesn't really make sense, you know.

What about stuff like theme, let's say the parent here defined theme is all fonts are yellow. So when I exported my notice yellow to, and after export, suddenly lost that yellow.

So we could.

If we do the report.

We could.

If the materialized properties.

Okay, good questions. Like what if this node here, uh, says that it's yellow, uh, yellow something.

And that's going to apply recursively to all these other ones.

So I guess that what that means is that the, those theme properties have to be copied to this node, whether it's safe.

Yeah, that makes sense.

Um, actually my question was a different one, but this is also very good.

My question was, if we have just one file without part of exports or anything, just one file, let's say this one with five nodes.

But the file says, actually, my, my root node is the one in the middle.

Okay, fine. You can do that.

But what does it mean? Why?

I don't think that's valid. I think, uh, if we have a series of parent child relations, then, um.

If the root node cannot be a node that is a child of any other node.

You know, so if it is the same way.

Yeah. So if you, if you wanted to say that this one is the roots, uh.

If that is the roots, then this here makes that impossible. You can't, you can't, uh, if the existence of this relation, combine with the existence of this is the root makes the file invalid.

Those two things cannot coexist.

Can you have multiple or what notes in one file?

No, because that defeats the purpose of, um, of a root node. If you wanted multiple kind of like nodes that exist at the top level.

Um, so let's say like you wanted some node next to this one, then you would, what you would do is you would actually just make like another node, which is the roots.

And then that node has that and then may also have, you know, some other nodes.

And these collectively, um, would be, I.

Quote the root nodes of the file, but there's only one file. The file itself is represented by, by this node.

I like that, and I think that makes it easier to define the next thing. Um, we wanted to be able to define the view. So he is an orchestra. You just opened it, but please, when you open it zoom to this rectangle.

That's what some formats support and this information where to zoom.

Yeah, it would be something for an O gift card canvas extension. Yeah, because it can only exist once per canvas. Yeah, right. And the other orders is a separate.

Part of doing of their file format, or special note of format mistaken.

Yeah, they also have these pages where you sort of have multiple canvas in one file, like you have multiple slides and PowerPoint. Um, we could say there's still only one root node and these pages from tier draw are just notes in our canvas, but you can give them a special type.

This is actually a tier drawer page. So if you are tier draw, go ahead and import them back as pages. But if you are not here, just one of them is not. So you have six boxes and can zoom them. I mean, pages don't have to be tabs on the side.

So for pages, we could have tier draw extension and not make it an okay feature and for defining the view. We couldn't have an extension that's only applicable for the root node.

So that would be, I think the other other settings, no type ready and store that the camera information.

Yeah, how should we call this root node type? I think I don't like settings. I like canvas better.

Because it's information about the whole canvas or document attributes or metadata or.

So one thought I have about the idea of defining like an area to zoom to one option is that we could just make the like that's like area of focus be just the size of the root node.

And but that would mean that the area you're zooming to is always going to have its top left corner be the root node.

Or be the origin of the canvas and then the zoom is just a matter of like, where does the other corner go like how far like that are you zooming.

I think it's quite clever, but maybe not.

Maybe it doesn't go far enough to define any rectangle to zoom to.

Or should we call this root node extension just okay if type root node, because that's the extension you can only use on the root node, whatever you put in there.

Makes sense, I'm good with any of these options really. Okay.

From from my existing experience with like you know 3D formats, there is no such thing as like a part of a 3D model we zoom into when we load it so it's not this is outside of my area of expertise so whatever you think is best for canvas apps really.

Do you have this requirement such as ideas on that.

In my own canvas tool I don't have that project when I load the file it just so it tries to show it so it's completely.

And you have to zoom in yourself.

So another example would be meta data like author last modification date.

Yeah.

The tool that created the export.

Where would we store all this stuff.

I think in something I called me it's something with meta, with information.

I'm now looking at the other format but I can't find what I'm looking for.

Inside of a GLTF it looks like this there's a top level asset object in the JSON that stores information about what generated it what's the version of the specification and so I would assume that like information about like what tool generated a file is going to be some

special top level section that has like metadata about the file.

Is asset a concept that's recurring in GLTF so is that like the root asset.

This only occurs once per file and exactly once.

It's not allowed to not have it and it only exists at the root.

So maybe we should build ours not as a note extension but really into the top level of the canvas file itself makes it maybe.

Because if you have a note extension like are you saying that maybe the no extension says metadata about the file like what app generated it.

Well but the app didn't generate just that one node it generated everything right.

Yeah I just feel that somehow this extension mechanism we have needs to reoccur all the metadata part of the canvas too so that it keeps being extensible for more document level stuff that apps need to store.

But yeah maybe we just have no extension relation extensions and.

Can this extensions.

All right well I'm going to stop sharing because I think of shown what I need to do to show here.

Yeah.

All right.

Yeah I think so at least in my brain it's nicely organized now what the next steps for the spec need to be.

Thanks a lot for these clarifications.

Yeah I will attempt to also define the nesting I mean we with the ideas we have now that's.

Easy seems.

Yeah.

And I haven't updated my good implementation of gift in a few months but I'll probably get back into it especially if we are defining the nesting because then I've actually already done the nesting for another format.

So it should be very easy for me to do this for oak if as well.

And provide like an example thing that can generate nested oak gifts.

Cool.

Yeah I think I also already implemented nesting in oak if.

That will be obsolete probably because I've been sitting canvas.

There was a tool dropped in our discord.

And charcoal. Yeah exactly or something. And that's some kind of nesting right.

Yeah they have to be implemented.

And that as well.

Do you remember if our concept now is is different or does it fit together or.

Different there they are there it's a child and it's a property and in a note which contains the complete converse.

Ah that was the mix of grouping and.

Yeah.

Parent child somehow into one.

Yeah.

Okay then I like our concept better.

Yeah.

Okay.

Yeah.

Nice.

I think that was a good meeting.

Yeah for sure.

No time to get some.

Yeah.

Thanks a lot for our their planings.

A nice.

Small task.

Although sometimes I forgot to forget this.

Well it's a very important task to keep us together.

Yeah.

No problem.

Okay so I'll hit stop record.