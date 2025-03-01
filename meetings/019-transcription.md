Here is the transcript with paragraph breaks added for clarity, assuming different speakers and topic shifts:

---

All right, welcome to OCWG meeting number 19, where we're talking about the OCHF spec specification. We were just discussing contributors and authors and kind of clarifying that in this specification. And I think we have a couple of topics to talk about today, and then we can go ahead and get into it.

So the main one for me is I left a bunch of feedback on the 0.3 draft PR. Do we want to go through that? Did you have a chance to look at it? Did you have any questions?

Yeah, I haven't looked through it yet. Well, I think most of it is pretty clear. There were a couple of things worth talking about. Most of it is just kind of nitpicky, like you missed a thing here, you left 0.2 instead of 0.3. It's like really small little tweaks.

Let me go ahead and share my screen real quick. I think this is the draft. So the main one that I wanted to discuss was arrows. Let's see if I can find it.

We said we wanted to add a way that the arrow can point to its visual note, which presents it.

Yeah, that's just missing currently, I would say.

Cool. Yeah, I just wanted to add it now.

Okay, cool. So that was... I didn't know if you had purposefully left it out, or if it was just overlooked.

Oh, I think we forgot it.

Yes.

Well, I'm totally fine with that being the answer.

Yeah, so then we would have start and end x, y locations, and then we would have a start marker and end marker, which I want to talk about, and then a start node and end node, which would be an ID of a node that it's pointing to optionally.

Oh, we need a third thing, like the arrow itself. We also need to be able to point to the arrow, right?

Point to the arrow. The arrow is a visual thing.

Ah, the arrow itself is already the visual node.

So the arrow contains a...

So where actually is... What if we have some cool-looking arrow, like a freehand drawing, which is visually the arrow, then...

Yeah, the font works.

I'm not following what you're saying there.

But if we have a freehand arrow...

Yeah, a freehand arrow just wouldn't work with our arrow.

That's right.

Yeah, we're basically saying our arrow is something...

We're not specifying a middle anchor point either. We're basically saying an arrow is a straight line between two points. That's it. There is no way about it.

And I think that's actually what we should do, honestly, because every infinite canvas that I've seen represents the ways that you can reshape an arrow differently. So like TL Draw and Excalidraw have an incompatible system for drawing an arrow with a midpoint.

Like TL Draw only allows you to grab the middle and you can only drag it off perpendicular, whereas like TL Draw—I'm sorry, Excalidraw—you can drag the point anywhere and it will redraw through that point, but you're on a perpendicular line.

It's kind of interesting the way that TL Draw made that choice, like you're on the midpoint perpendicular to the line is the only way you can drag the anchor. But I think because there are so many different ways to do it, the only simplest way is just to say arrows go from here to there. And if you want to do something more complicated than that, then you need an extension.

Should the relation, the edge relation, should that be able to point to an arrow, link to an arrow, just like we have to install an end node, but you can also add to that?

Yes, that's a nice idea.

Yep.

And you're saying the link should go from the relation to the arrow, Michael, as opposed to from the relation.

Because the relation also links to the start and end node, so then it makes sense to do that.

I see, right.

So yeah, in the relations section, it's not a set. It's just a relation.

But no, it's that group. The edge relation.

Yeah.

Okay.

So we have from two directed and relation type. So we would want to point to a visual node visually representing the relation.

What do we call that visual arrow, or node, just nodes, right?

Because elements, relations are technically not nodes, right?

Yeah.

So I think we're using, we're using this term node to mean visual nodes.

It's like a shorthand for it.

Yeah, I agree.

Yeah.

So it's something, I think if it's not node, if the property's name isn't node itself, it should be something that contains node, like node pointer, node, you know, ref, ref node, or something like that.

Like you could do like that.

Or node ref or something.

Notice.

Notice.

Good.

Notice.

Fine.

I think it's consistent with the rest of the spec where we tend to truncate names. Generally, and not really spell them out very long.

Not truncate, but we try to keep them terse at an optional pointer to a visual node that visualizes that represents the relation visually.

I guess you're taking notes here, but I'll just add a comment here so that we make sure that it gets merged in before we address before we merge it in.

That's a great point, Michael.

So then.

Sure.

We then remove start node and end node from the arrow.

Or do we have a redundant way to specify that?

Yeah, I think on this is that some canvases will ignore relations largely when they do an export and will focus on nodes instead.

That isn't what we would necessarily want, but I think that is realistically what will happen.

And so giving a place for that to happen in the arrow makes sense to me, even though, like you point out, Max, it is redundant.

Yeah.

If you put it only in the relation, then we force applications to use relations more.

Yeah.

Let's just go that way.

Could be good.

I hear you.

How this doesn't ever have a start and point?

Yes, it does.

It does.

Yeah.

So you're not...

You don't have to point to a specific node.

You already...

I'm sorry.

Points are here.

Yes.

We already have an XY location.

Is that OK if type right?

Yeah.

It is.

Yeah.

It's an array of numbers.

OK.

It goes for comfort.

No, it should be a coordinate or something like that.

Coordinate.

Yeah.

I think these are only used when you when an arrow is not has no relation when it's just a free arrow on the canvas, then you start an endpoint.

I think in most other situations, if there is a relation, then you use the start the nodes positions.

Well, I think we discussed that we want to start an endpoint to be required and so that the arrow can actually be drawn.

Yeah.

Exactly.

Always.

I mean, that is another kind of redundancy, but this makes the arrow a standalone geometric object.

It just goes from a point to a point.

Yeah, that's true.

Mm-hmm.

Yeah, for canvases that don't support arrows pointing to nodes, I think it's important to have the start and end like you like you pointed out they're required here.

Yeah.

Yeah.

That's that's for sure.


Yeah, and also in my own situation, I always write the coordinates for the start and endpoint even if the nodes are connected.

Then I choose the coordinates or what kind of like a poor man's version of the point, the port's extension.

Right? You can say, "I'm linking it to this node. This arrow links these two different nodes, and here's the point at which it comes into the node."

Right? Without having to use ports or anything fancy there, you can at least get the arrow going to the right spot on the object.

So, no, I think this is the set. I think the redundancy is okay.

So you would like to have start node and end node additionally?

I think I slightly prefer that as it lets people write a more terse version of the spec and doesn't require them to use relations and have them.

But then we also need to explain then how they should use the relation, the edge. Should you usually have an arrow accompanied by an edge, and then, or should you never use edges?

So what are these edges for if I already have the start node and end node in the arrow? Should I then also have the arrow relation type in the arrow to make it easier?

You mean point to the relation from the arrow node. Copy everything from the edge relation into the arrow node.

Sort of.

Yeah, I got you.

I don't know.

Yeah, I'm not a big fan of that.

We didn't see that with the nodes.

Yeah.

That will start node and end node in the arrow points, start and points. That’s, I agree with that for sure.

Okay.

It's...

I don’t know.

No, I think you're... I guess you're right.

So relations being a more conceptual object, relations being about the conceptual information on the canvas that's not necessarily visual, may be visual, but isn't necessarily visual.

The points give you the spot to draw the arrow from into the start and end in the node.

And then the relation, the optional relation, gives you the ability to say it relates to these two nodes.

And then you can also say whether it's directed or undirected.

Okay, I'm with you there.

What about a field relation where the arrow can point to the ID of the relation it represents so that it's double linked?

Right.

That was one of my practical concerns here: you would have to scan the entire relations node from an implementation standpoint.

You'd have to scan the entire relations node looking for a backlink to the node that you're referring to in order to know which visual nodes it points to.

And the other thing is that there's a difference.

The other thing that's confusing is that in the relation, it's called "from" and "to," and in the arrow, it's called "start" and "end."

And is "from" start and "to" end?

I think it is, but there's like some mapping that you have to do in your brain between those two.

Perhaps we should choose "start" and "end" to align with that?

Yeah.

Yeah, "start" and "end" is probably the clearest.

Yeah.

I don't know if we have...

I think so.

And at least it aligns with the arrow.

So "from" is the start and "to" is the end, and then we have "start" and "end" for directed relations and nodes.

What about the link from the arrow to the edge?

Yeah.

Which way should the link go, or should it be bidirectional?

There’s a little bit of weirdness here in that if we link from the arrow to the...

If we link from the node to the relation, multiple nodes could link to the same relation, which may be good or may be bad.

And similarly, if you link from the relation to the node, no, you only get one option there.

The relation can only point to a single node.

But multiple relations can point to the same node.

Say that again, I’m sorry.

If we have a field and multiple...

Multiple edges would use the same node ID.

Oh, yes, you could have multiple relations all pointing to the same arrow.

Yeah, you're right.

One thing we've thought about in the past is when you delete a specific thing on the canvas, what else should be deleted, like cascading deletes.

We can't control that, but we can recommend what our advised cascading delete strategy would be here.

And so maybe this is a case where the pointer should be on the arrow side.

The danger is that if the pointer is on the node side, then when you delete the arrow, you also delete the associated relation.

But the danger is, if you've got multiple arrows pointing to that same relation and you cascade the delete, then you've removed it.

If you make it a J, then it's a one-to-one, right?

Not necessarily, only if you do it right.

What is it that we want to express?

So we have on the relations side an abstract edge that says these concepts are related.

And visually, we have an arrow going from an x, y position to another x, y position, showing something very visual.

And then these two things can be related.

Is there ever a good reason to not have a one-to-one relation? Can you have multiple arrows representing the same edge, or can you have several edges for the same arrow?

No.

It’s really one-to-one.

So now we should talk about deletion semantics.

Does it make sense to delete the visual thing and keep the structural one, or vice versa?

And maybe the structural thing feels a bit more fundamental than the visual thing.

But usually, deleting one should probably delete the other one as well.

So maybe double-linking them and writing in the spec that these should point to each other is the way to go.

I think so.

And it is somewhat redundant, but it actually is helpful for implementation.

At least for the reading part of the spec, maybe not the writing part of the spec.

In the writing part, you have to remember to update both places in parallel.

So there's some burden on the author, the implementer, to keep those links aligned.

But it really does make it easier if you're reading the spec to say, "Here’s an arrow, where is the associated relation?" and I can follow the link from there without having to scan the entire bag of relations.

I think it really expresses that concept of the arrow and the relation.

If you have that link—a bidirectional link.

And we call that relation, the property on the arrow?

If we're going to call it "node" on the relation, then we should call it "relation" on the node.

Okay, and both are optional, but if one is given, the other one from the other side should be present as well?

Correct, yeah.

And the deletion semantics are: delete both.

Okay, yeah.

Okay, good.

I like that.

Moving, representing the start...

I’m just doing this for my own accounting of comments here.

On the relation...

You’ve got the bulk of the...

Actually, I want to do it as a reply.

Can I do that?

Maybe you can't.

Only if you edit it.

That's right.

My friend Rob implemented that, by the way, and I still give him crap about that.

I'm like, "Why are there two options here?"

Like, "What do I want to do?"

Anyway.

All right.

Well, were you going to bring something up, Max, before we move on?

Because start marker and end marker...

Because it's something that Michael and I discussed last second in another meeting when only we two were left.

So if you have a visual arrow, you want to see where it is actually pointing.

Is it from A to B, or from B to A, or is it connecting both ways?

So we decided, yeah, we have for both ends this decision about the pointiness of the arrow and code it somehow.

So you need like three visual styles.

Is the arrow actually...

Is it going from the thing into the arrow here, or is it coming out of the arrow, or is there no direction?

Right.



And then that allows us to represent all the different components. The two that I feel very confident in—yeah, these are the common ones. Part of that, there is nothing, and there is an arrow. Those two. 

This incoming one, I was kind of like, I get what you're saying, but I don't even know that that is… I'm trying to think of canvases that visualize changing the arrow tip to represent that. 

I don't know. Maybe it's over the top. 

Yeah, it has a certain consistent feel to it. 

I get that, especially since you have "outgoing" as the name for the arrow. I would probably just call them "none" and "arrowhead" or "arrow." Yeah, "arrowhead"—I think it’s the common name for these things. They’re called arrowheads. 

And then leave the idea of "outgoing" and "incoming," because these are semantic, right? As opposed to visual. 

They're not actually calling this the visual. No one calls this thing an "outgoing," right? 

You're saying when you have an outgoing, then it should be an arrowhead. 

And I think that’s too prescriptive. I feel like it should just be: "This is an arrowhead." 

Now, granted, we're probably going to fail to satisfy just about everyone by giving them only, you know, "no end marker" and "arrowhead marker." That’s it. That’s the only two. 

And then how you represent the arrow? Totally up to you. 

But it seems like every infinite canvas probably does this differently. 

And so, this is another case where, like, if you want to really control the arrowhead, you need an extension. 

Yeah. 

Yeah, I’m trying to bet. Let's simplify. So we only have two options, and that’s easier to understand. 

So, that's what I agree to. 

Cool. 

Or is it all one word? 

I don’t know. Google can probably tell us. I'll say "perhaps." 

Cool. 

I think those were the only two comments that I had that were actually questions more than comments. 

Yeah, we just discussed that. 

Yeah, that was just noting that we're out of date, some formatting changes. And then when we look through this… Yeah, everything else is just comments. 

Or like formatting-type stuff. 

Um, what else do you guys want to discuss? We have a few minutes left. 

Yeah, I had also two comments/questions. One of them is already answered—that’s with the edge and the arrow discussion we had. 

And the other one was about the type names for all of the node types and relation types. 

I'm not sure they are consistent yet in the spec. 

I think you had a comment on one of them, which I picked up already—at least the one you mentioned in the comments. 

I’m going to store the direct amount of right. 

Which type? 

Um, right and right nodes, right? 

Okay. Got it. 

References to right node and… 

Oh, she, WGD slash note, slash direct, yeah, the JSON file or the—here, click on that—right node JSON. Got it. 

I think the title I had was "oval note" or something like this, but it's fixed now. 

Okay. The title—is that the name of the type, or just something…? 

Oh. 

Um, description? 

Well, semantically speaking, the name of the type is defined in the schema that uses the type. We can just propose nice default names. 

Oh, now we can define built-in names, so maybe they do matter more. 

I think the spec has a section on the built-in names or something like this. 

Built-in… built-in schema entries. It's called that in the spec, in the appendix at the end. 

Yeah, this one. 

And there we propose a built-in mapping from type names—yeah, these JSON schemas and these URIs actually define which type is really meant. 

And then this built-in schema entry is a common short name. 

So that users can refer to it. 

These names are what we should use in the notes. If you have a different default type, but something different—yeah. 

And then these non-extensions, they are also proposed names, but they carry a version identifier in the name so that they might evolve differently. 

And the built-in schema entries always evolve together with the core spec. 

So if the core spec is 0.3, all these types are also 0.3 and cannot change independently. 

That was sort of what we defined—how core extensions differ. 

So they don’t need a version identifier on their own. 

They have the same version as the spec they are used in. 

Got it. 

Yeah, at least this is my proposal. I mean, we have not discussed this part a lot. 

So then, I could… The nice thing about this is I could write, you know, OCW node arrow without having to include the spec. 

Sorry, the schema in the schema is, you know… I like that a lot. 

And it really does give this kind of, "Here are the core things that you're going to need." 

And if you need those, then the schemas are already defined outside of this file. 

So they can be defined in this file. 

I like that, you know, it's valid to additionally copy in this block. 

You can also copy in these schemas into the schema section. That would be valid as well. 

But yeah, that makes sense to me. 

Michael, where you… You were referring to the file "rect node" and talking about the title in there. 

Were you expecting it to look like this? 

I mean, or sorry, like this: OCW node slash rect instead of rect dash node? I think that’s what it was called. 

Yeah, maybe… I’m not… Yeah, I guess you were, and then Max, you were going based on this, I guess, "rect dash node.json." 

So you called it "rect dash node." 

I just gave it any pragmatic title that sort of identifies it—it’s not much about it. 

Okay. 

Our spec doesn't say much about all the title, but the entries… Let’s see, an object representing a schema entry. 

Schemas have a URI, a schema location, and a name. 

Title is completely freeform. 

Okay, until now—I mean, we can change that. 

Maybe it helps if the title is more formal. 

Why is the title there at all? 

Because JSON schema requires it. 

Because it’s broad a lot. 

I thought it’s got to be in the file, so you can see what you have. 

Gotcha. 

So it's like duplicating the file name, is what you were thinking. 

But if you, you know, cat the file or whatever, you don’t, you know… By looking at the file’s contents, you know what it’s called. 

Yeah. 

Exactly. 

So there really is no name—the name mapping happens to occur outside of the file itself. 

Yeah. 

I mean, the thing is, the URIs identify the type. 

They are the unique key. 

And the local names are just shorthand within the user's file to make it easier, if you want. 

Yeah. 

Hat names, like we talked about, you can rename maps onto that and have a global namespace. 

Maybe it makes sense to also call it at OCWG slash rect slash node—exactly like the user sees it. 

I think so. I think it’s… Maybe that’s confusing. 

Yeah. 

So. 

Oh, that's confusing. 

I was good. 

Yeah. 

Exactly. 


Yeah, exactly. So just—that’s why it’s so great when people are writing the schema files for extensions. We can encourage them to use that title as well, like "Use your organization name," you know, and then the fully qualified schema name.

I guess the one thing we'll need to indicate, Max, is that it is optional. Like, you can… There's nothing… We're not validating that title.

Mm-hmm. 

Yeah, and we also need more examples in this spec.

Oh, boy. That we do. 

Yeah. Maybe we should—

That really helps.

Put them in the cookbook or… I mean, we don’t want to bloat the spec with too many examples either.

Yeah, true.

I definitely—there were definitely—I tried to, well, I tried to note these spots in the spec that while I was reading the spec, even though I know the spec pretty well, I was having trouble visualizing an example in my head. 

And I think I noted in a couple of places, like, "An example would be helpful here," because even when I was very familiar with the spec, I couldn’t think how that would be represented.

And so I felt like, "Then it's too dry."

Exactly.

I hear you.

The first examples that you come across, they don’t have that type indication, because the default is a rect node, probably.

So this is just a rectangle, but maybe we should just—

They’re going to read the spec from the top. They’re going to be scrolling down: "What does it look like? What does it look like?" 

"Oh, here’s what it looks like." 

And they’ll, you know, kind of fixate on this first example.

Just practically the way… Oh, there’s a 0.2 as well. I don’t know if I caught that one in my comments. 

Maybe we should add a type here, even if it’s a default node type.

Mm-hmm.

I'll make it an oval node.

Yeah. 

I thought about—one thought to your point, Michael. I did have the thought that this should possibly be a more robust example rather than a minimal example. 

Maybe still a "Hello, world," but maybe like a rectangle.

Maybe two rectangles with text in them, with an arrow pointing between the two of them, and then have, above this, an actual visual of that.

Like, "Here’s the OCHF representation of this very simple canvas that has two rectangles, one arrow, and text."

And we should move it even higher—before file structure. Like, just an introductory example as part of the introduction.

Yeah. 

Yeah, I would love that.

And then obviously, what we’d eventually like to get to is something like this, where you can, you know, see this, where you can see the spec, and as you change it…

Would be really nice.

Using that is such a nice representation of it, but we’ll get there.

But for now, what we have is the spec file to share with people.

And so, what was your idea? Two notes and an arrow?

Yeah, I was thinking of something like this.

So also an edge relation?

Mm-hmm.

Exactly.

If you get a relation…

The one thing we’re not showing, and I don’t think we should show, is extensions. 

I don’t think we should bother.

So it’d be something like this.

Agreed.

Yeah.

I think this is an excellent example. "Hello, world." It’s super minimal, but it represents a whole lot of things.

Like, there are two different visual nodes, there’s an arrow node, there’s a relation between the two, there’s text.

So you’re getting the resource.

The only thing that would probably be a little bit more maximal would be including an image.

Here’s a great poem by Wendell Berry.

Yeah.

I’m not saying we should do this, but another option would be—this would show assets, right?

In a more hypermedia-assets type of way.

Maybe.

But I do like the simple—you know, two boxes, an arrow, and some text. It’s a really nice minimal canvas.

That’s very nice.

Do all canvases even support images on the canvas?

Does CodeFlow Canvas support images?

Uh, I support images, yes.

You do?

Okay.

I'm curious.

Not as easily as TL Draw, but you can put images on it.

Yeah.

It’s probably just this.

The funny thing is, whatever canvas we choose to use as the image, like the snapshot, I feel like I should make this look less like TL Draw.

Like do, um… what? That and that? You know.

We just draw it in PowerPoint and make it look really… Actually—

Microsoft Visio or something.

Yeah, or Keynote. I'll pull up Keynote and draw this for you.

Get you a visual guide.

We’re coming up on one o’clock.

We talked about having a more robust example at the top.

Michael, did you have any other comments or thoughts as you were going through the spec?

No, this is—I think that was it for now.

Cool.

All right.

Well, I have a couple of TODOs.

But Max, I don’t think I have any other blockers on the PR.

Oh, I did have one other question.

Why did you call it 0.3-draft?

Yeah, I’m not entirely sure by now.

I think I just wanted to make sure that there’s no 0.3 available at some URL confusing people.

Ah.

So I’m on the old version already.

But yeah, I renamed it now to 0.3 so that the pull request actually can be executed, and then the draft will be gone.

I haven’t pushed it yet, I just need to add all these other little defects.

Oh.

Yeah.

And on this point, I do have an idea for 0.4.

We will just copy over the old spec to 0.4 and then make a pull request, putting the changes on top of it.

Love that.

That will be super helpful.

But yeah, it was pretty seamless to review.

I think the other thing that I’ve—the last two times that I’ve reviewed the spec and the work that you’ve done, Max, the thing that I was missing, because of the way the PR review works, I just read from the top to the bottom.

And that’s not necessarily the order we want people to read the files in, right?

We almost want… I think we almost want like a "Start here," "Read this file first," then read these files.

And then we can have that in our minds while we’re writing as authors.

Like, "Oh, if you're in this file, you should have already read this file."

And if you haven’t, I can deep-link into that file with the ID.

But I’m not going to re-explain or reintroduce it, because it’s already been introduced in this other document.

That was just—that’s not your fault.

The PR review process doesn’t present them in a logical order.

But it did remind me that if people dove into it in an unexpected order, it could be really confusing.

Yeah.

But there are basically two documents in order.

The spec should be pretty much self-contained.

And then the cookbook can say, "Maybe you read the spec first, and then I’ll explain to you how to use it."

Yeah, agreed.

Oh, shoot.

I forgot. 

I have another meeting that I have to run to.

And I’m three minutes late for it.

Talk to you guys soon.

Yep.

Thanks, guys.

All right.

