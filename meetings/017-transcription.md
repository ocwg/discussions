

Yeah, this is just for those of you who are watching on the recording potentially. This is OCWG meeting number 17, and we were just talking about how we're going to use the time today. Thinking it will start by doing some planning around like what are some next steps for the spec and for other things around the project. So we're going to get our projects for a bit, and then maybe we can actually dive into writing some examples. All right. Max, was your comment—I missed the very beginning of it, but I think I caught the gist of it. Was it in response to Kapanos positions?

Yeah, exactly. Yeah, first I thought interchange and interoperability is more or less the same, but after a while, I realized that there's a very good point. Actually, yeah, to have a common core that everybody agrees on—what really canvas needs to have and needs to understand—that's really the core of the OCF spec. And then being also able to add more data to piggyback it through and around is nice, but the core needs to work in order to have anybody interested in the spec in the first place.

I just looked at the existing issues in the spec repo, and we have this 0.2 versus 0.21 issue. Yeah, we maybe should soon release a 0.3 to clarify that because the two are so different already.

Right, 0.2, 1, 0, 2. Yeah, that's when we did the relationship extensions simply, but... and yeah.

Okay, I just made a project at the base level of OCWG. I just made it public so you guys should be able to see it now. I also closed out the old project working in progress.

Why? Are you in a project not in the GitHub sense? Not an issue project.

Okay, yeah, yeah. Exactly. There was an old project that was called like "planning" or something like that, that Orion and I used in the first month or something, and then we stopped using it. So I just went and closed it so it wasn't distracting.

Oh, administration.

No, it's still there. I just—we're not using it at the moment, but I think it's private. But now there should be a public one called "work." Very creative title.

I can see work in administration.

Yeah, cool.

Oh, yeah, because you're an admin for the organization, so you can see both.

Oh, got it.

So now we need to put the existing issues we have into the sheet?

I think so. I think it just starts by dropping them here for now, and I think we can actually refer to your issue. Yeah, like you were saying, we can bring in the existing issues. So like there’s zero-two-zero-two-one.

Oh, okay. How does it do that? You think it’s from the repository?

I can’t get any type.

You choose which repo. Pretty nice.

Yeah, so we only need to add the open ones, and I think we only have—do we have issues in other repos already? I don’t think so.

I think we’ve been pretty good about keeping it all in the document and keeping kind of iterating on it within the document, which was, I think, a great choice of like move fast, low overhead type thing.

So we agree for the first one that we should release a 0.3 soonish to have a clear version?

Yeah, I think you can probably take the 0.2 to 0.21 feature over and like change that to be about 0.3, basically. Because it was more of a question now that I look at my own, like there's no finish line inside that. It’s like, what are we doing with 0.2 versus 0.21? I guess I should—we should update it, you know, so that it’s consistent everywhere. But yeah, this is 3. That works.

Okay, so we need a title.

Should we then add a new document spec 0.3 in Markdown so that you can always simultaneously look at the old version as it’s commonly done for specifications?

Yeah, that makes sense.

Oh, thank you. Very kind. My daughter brought me lunch. I’m like, well, I got—let’s see, fish sticks and a cheese stick and pears. Not bad.

Yeah, I was also thinking about serving—setting up the spec URLs at spec.camus protocol. That should be a fairly easy thing. I’m always looking for like brainless tasks I can do when my brain power is low, and DevOps is definitely one of those things.

I’ll convert that to an issue. I’m going to convert that to an issue but put it on the actual website repo.

I wonder if the website repo is public. There’s no reason it shouldn’t be.

Let’s see.

Pretty sure it is. Yeah, it is public.

Yep, I see that.

Good, good, good.

Yeah, everything public.

Great.

Good, good. With the exception of the admin repo or the admin project that we discussed, but that’s fine.

All right, cool.

Jason’s schema for the core parts is definitely one. Even if it doesn’t, you think that Max is including the work to create the validator?

I mean, there is that kind of—it’s kind of the same work.

No, no, the Jason schema for the core part is much simpler. It’s a really small schema. It only has like four parts, and then it says, we can’t specify much more. Enjoy it. But that’s exactly the point.

Did you see my example that I included in the email?

Yeah, I only read it on my mobile, so I’m looking at it. No, it didn’t format super well on mobile. And I actually, I almost jumped into the rabbit hole of changing the way that Buttondown sends email CSS for this particular, like, no, just hit send. Like, don’t reformat the email. But anyway, I actually ended up having to write a schema, a JSON schema, to describe an extension in that. I mean, because like, oh, yeah, this is how this works, right? We’ve got this schemas array, and I’m going to have an extension, even if it’s core, it’s still an extension. And so I need the schema for it anyway. So I did it inline instead of having it refer to some fictitious external URL that doesn’t exist yet. That’s why we have inline schemas.

Exactly.

All right, now we need to look at all the other to-dos sprinkled.

Yeah, look at the bottom of the 0.2 spec in the to-do section. Let’s move those over. Let’s cap this to like maybe two or three more minutes. I don’t want to spend too much time on planning when we could actually spend some time doing work, which I think—I think my awesome goal for me for the end of this meeting, like by one o’clock my time in the next 40 minutes, we would end up at a spot where we have an example documented of like one of the core spec items like arrow or rectangle or whatever it is. And we know where—like what—where we’re going to put it, like the rough file. We’ve done one basically. Because I feel like if we’ve done one, I could pretty quickly do a few others. And then if people are interested and say, well, shouldn’t you have an X? We could be like, well, there’s an example of a Y over there. Just follow that example, and you can make an X and propose it. So that would be my very, I think, small goal of like have one example of one core item documented.

So where is the example circle? In the repository somewhere?

It’s not in the repo yet. It’s only in your email. Literally, it’s in my Obsidian, and it got copied from my Obsidian into Buttondown and got sent via email. And it also became a screenshot that went into the BlueSky post.

All right. So I’ll copy it into the repo.

And I very quickly, you know, made the decision of like, circles only have radiuses. Like, should we add stroke? You know, like, I just left it all alone. I was like, radius. It’s got radius. That’s all it’s got. Probably has a background color, actually, and probably has a stroke and a stroke weight and a stroke color. But like, this is all up for discussion.

Okay, how do we call the examples from the mail? That’s the circle extension.

Let me pull up your back. It was kind of interesting trying to write that example for that email. Like, I actually did have to refer to the documentation. There were things I had not memorized. I was like, Oh, how does that work? And I found myself definitely wanting examples. Like, this would be so much easier if there were already an example that had a schema with an object referring to the schema. And I’m like, instead, I have to parse the documentation to understand exactly how it works because I didn’t want to include like improper syntax in an email that went out to everyone. Zero dot two. Here you go. And then syntax error.

In fact, I almost blocked myself from sending it on hearing back from you, Max or Michael, to like validate my JSON by hand. And again, I erred on the side of just send, just send it.

All right, the formatting you used—very nice and compact. But yeah, as soon as I did to format, it’s—

No, go ahead and go with your auto-formatting. It’s fine.

Yeah, but then it’s—

I compacted it for readability in an email, right? I like to be above the fold, so to speak.

Yeah, but it’s like it much better in the compact form.

Well, we can write our own Prettier. We can use something like Prettier ESLint or whatever to reformat our examples, and we can check those rules into the repo so that when people are creating examples, they get auto-formatted. Or we can at least run an ESLint. If they check in something improperly formatted, we can clean them up so that they’re more compact.

Something that I want to—actually, when talking about your example, I want to make a small video about my project where I implement this spec. But I do think that, of course, that implementation should be correct. I think I’ve got a video finished after this weekend, but yeah, I’m not yet sure if it’s already the right moment to send it out. Again, of course, I will say in the video, that’s not a perfect implementation yet, but yeah.

Dude, what’s the manifesto with the standard?

Shall we just call it circle data instead of circle extension?

Call what? What are we going to call it?

Like the example file or like the normal language? Is this is circle extension to the OK spec? Or is that maybe just the specification of circle data? So that would be more lightweight in language.

Extension is correct. 

It feels like there’s two things to me. Like there are things that are core, and then there are things that are extensions. The reality is that core is actually a blessed set of extensions.




Yeah, kind of there, but they’re all extensions, I think.

We’ve already talked about assets representing external media. So it’s not an asset.

Data feels too broad to me. I would probably just call it extension, but I don’t have a better word yet. 

Or we go with a circle node type or circle relation type, sort of like—

I would say circle node. That’s the circle node. Yeah, and the arrow node and that kind of stuff.

Yeah, I like that. And circle node is actually a node extension if you—

Right, but the shorthand being able to refer to them as like this is a circle node, an arrow node, a rectangle node, a text node, that kind of stuff.

I’ll just drop this link into chat about rules for standard makers. I’ve found this article to be very helpful. This is by Dave Winer. He’s the guy who wrote the podcast and RSS, I believe. Did he do RSS as well? 

Or no, he did podcast and I think he worked on an outliner as well, but has written several successful standards. And his rule number one of standards, like what we’re working on, open formats and protocol, is that interop is all that matters. Getting working interop as evenly as possible is all that matters. And I respect that as wisdom. The only reason we have open formats and protocols is so our software can interoperate.

And there’s somewhere in here where to your point about—yeah, freeze the spec, keep it simple, don’t break anything.

Yeah, we’re close to a point where we would actually want to freeze the spec seriously. And like, for example, think about Michael’s implementation in Code Flow. Like, how much work do we want to put on Michael to continue to keep up with the changes in the spec, right?

Yeah.

Yeah, I will not put more time in than I have, of course. This is until so far. Now it changes are coming, made pretty quickly.

Right. And you’re the only one right now. But hopefully, very quickly, we get to a point where we don’t want to change it because there are people building on top of it.

Yeah, that must be the goal. Yeah.

All right. So let’s see. I was looking at the spec. I’m going to copy.

Max, do you want to share your screen while we work on the first set of examples since you’re already working with Circle?

Yeah. I just rearranged everything so that I can just see my IDE.

Yeah, no, I understand. So how do I share a screen here? What, the share button?

Oh, and I have to give you access to it, which I just did. There you go.

So now I’m allowed to share. Okay. This bigger work screen. This looks good.

Okay, how do I get rid of this Zoom—

Yeah, unfortunately, you can’t get rid of that bar completely. 

I can move it elsewhere.

You can move it, yeah. But I think I’m—I hope I’m still sharing the same screen.

Yep. What we’re seeing is—it looks like VS Code or something like that.

That’s IntelliJ.

IntelliJ. Oh, I see.

Yeah, that’s what we’re seeing. So we have a Circle node. That’s what I copied from your mail. But this is already an example.

Okay, it’s correctly an example. So we now also need to like put the schema itself in its own file. As an example of how these schemas can be put in their own file?

Exactly.

And do we want to attach a version number to it? Or is it like assumed that without a version number, it’s the most recent? Or do we version by folder?

Like directory. The way you have the looking at the URL schemes right now, because I’m thinking about implementing these, and you have it organized by like there’s a directory almost like zero dot two slash here’s all the things. But that implies that we would want to version everything together actually, which is not necessarily true.

Yeah, except for the core types, they should always be a consistent set of elements.

You’re saying the core should all be versioned together.

In reality, people don’t want to deal with the fact to use spec zero dot three with a circle data extending zero dot four, which blah blah blah. That’s too much.

And that’s a good point. I just go for a schema zero dot three, and that’s it.

Got it. I like it.

So we have—yeah, maybe one folder per version.

Yeah, so if we’ve got an OCW spec folder, we’ve got the schema folder, then—and we’ve got the spec—then yeah, one folder per version. Should that folder be in the—okay, so the spec folder is really documentation, like it’s a markdown file.

Yeah, with docs. The schema are actual JSON schemas.

Okay, got it.

Maybe, yeah.

Actually, I’m not actually sure where these come from.

I think some of these need to go away now. I think they are—

Yeah, legacy.

Do you put them into zero dot one?

Yeah, that makes sense.

Can I use a dot in the directory name as that a good idea?

IntelliJ says.

Yeah.

IntelliJ says that’s okay.

It’s just the—okay, so these are the legacy. Okay, then we want to have a schema for the circle to start with. Circle, and it’s a node extension.

Okay, and looking at the example, the schema looks something like this, but now—

No, I custom things.

This is a valid JSON schema.

Yeah.

So a JSON schema has to have a top level. You probably know this better than I do. I had—I learned this in the last week, which is it has this top-level thing that says, what is—you know, what is this thing? And I basically said it’s a JSON object. I mean, a JavaScript object, and I cut that part under the assumption that all of our JSON schemas, the top-level thing is going to be a JavaScript object. And so that’s kind of redundant for us to say schema is a JavaScript object.

Okay, so, this was—Gemini says we should do.

Exactly.




So that line three is what I cut.

And is this the correct version of JSON schema to use? No, I didn’t go look.

Shouldn’t that be the route to this file?

Again, shouldn’t that be like, you know, let’s just be the same for all of our JSON schemas.

Yeah, but it should be the correct one.

Yeah, sure. And I think most people are using this just one by now, I think.

Yeah, I think Aaron mentioned this in a comment on the pull request of mine.

Oh, no. So this is the right one, JSON schemas draft editor.

Okay.

Back to my IDE. So this is wrong.

So now they have a pound sign at the end and we don’t.

So if nobody knows the answer to this one, I’ll ask Gemini again.

Oh, sorry, I didn’t hear the question.

The pound sign at the end of schema—is it required or not?

If I look at JSON schema validator.net, that is a schema on the left side, and it hasn’t got the pound sign on the end of—

Yeah.

Okay, so leave it out. Okay, so now we have one basic schema.

Okay, now it shouldn’t be too hard to have the JSON schema for all a specification, right?

Let’s ask Gemini again.

Max, would you create a branch and call it like examples or docs or something like that and push up what you have? And I’m going to start adding some other things.

That’s the extension. One second.

Oh, yeah. No problem.

Any more screen time?

Yeah. My kids would agree with that. They need more screen time.

All right. Yeah, I’ll put these things in the branch. I think I’m in some branch already.

I was just looking. I don’t think there’s any branches out there that are pushed up to the remote anyway. Specs 0.2.1 is still out there, but that should get deleted now.

Yeah, I’ll put them in this branch.

Wonderful. I can drop a little bit early. I’d love to do some async work now that I have time again. So I’ll look to follow up in the channels and see what I can contribute.

Well, I’ve got bad Wi-Fi up in the mountains here.

Awesome. Yeah. Well, don’t break your neck landing any backflips, and we’ll look for you back to the US.

Yeah. Yeah. Yeah. Let’s meet up and do some stuff when I do. That’d be good.

Awesome. All right, man. See you.

All right.

So what are the examples that we had? Or should we maybe define the core stuff from the spec so that we can...

Yeah. Let’s do it. So we just go to the existing extension and decide what—for example, we have the ports extension.

It’s not synchronizing right on left.

Yeah. And I’m going to go to the 0.1 doc that Orion and I wrote up because it has some good core stuff in it.

So the ports extension we could leave out of the core or we could add to the core.

Right. You’re saying it doesn’t need to be part of the core.

Well, most canvases support ports.

I doubt it, actually, but—

You doubt whether all canvases support ports?

Yeah.

Most canvases—if you look at whiteboard canvases, they usually can make connections or arrows, like the L-row, but is that with ports? I don’t think so.

So what does it mean to be in the core or not? 

So we will have one specification document, and that should be as short as possible. And then we put extensions that are not part of the core in another document. And for this core part, we will say that we maintain a consistent versioning across all these extensions so that if arrows are part of it, then the property peg of the arrows is versioned together with the spec. So this is one coherent bundle.

But if stuff is not in the core, it can evolve separately and needs to be mentioned separately in the schema section and so on, and it can have different versions if needed. So this is like the split we’re talking about, maybe.

We can still unofficially provide or strive to make the ports extensions match the core part. But yeah, the promise we do is that the core is coherent.

And if we have a shorter spec, the adoption rate might be better. If it’s too short and it has not enough features, then again, we have a problem. But yeah, the ports—maybe I agree with Michael’s assessment to have it not in core.

Yeah, agree. Agreed.

Okay. I’ll not leave it like this, but it’s just my marker. I’ll see it in—

Whatever other extension have we defined already? The relative constraints extension?

I think that’s something that Aaron mentioned—that this is super common in GLTF to have nodes acting as groups for other nodes and then positioning them relatively.

Yeah, but totally not the most common thing in other canvases.



So I posted my shortlist. My shortlist is rectangle, circle—

Yeah, these are not there. So we need to add them. But first, let’s look at what we can keep out.

Sure.

Because we also have relation types. The set relation—that seems really basic, right?

I agree. No, I think set—I didn’t think about relations yet, but I think set is one. And what was the other? Edge set?

The simple edge.

Our core.

And the hyper edge can go out.

Yeah, I don’t see why it would be core.

I know. I know there’s a few people who love them, but...

Copilot suggested this should be part of core.

Yeah, I don’t know that hyper edges are supported in Obsidian Canvas.

So group?

Group is set, right? It’s the same thing.

No, group has—

What does it have that doesn’t?

That’s a good question. A group has members. And if you delete a group, the members are still—I don’t know—the members get deleted as well.

So group has a much stronger semantics than set.

I see what you’re saying.

But it doesn’t have any—like, functionally, the schema is exactly the same, right?

Yeah, but that doesn’t matter for interoperability. If it’s still a different thing, if you put it in a set, it will behave differently from putting it in a group.

Okay. So set and group—both are the same with the one exception of group being a stronger relationship where the things that get deleted, when you delete the group, it deletes everything inside along.

So we should add it to core.

Yeah, group definitely needs to be in core.

Okay. Then we have parent-child, and that was used to inherit properties.

Yeah, that doesn’t feel like core to me, but inheriting properties doesn’t—I’m like trying to think of canvases where that’s actually implemented.

All right, so we can leave it out.

And that was the existing list of extensions. Now we can talk about the ads.

All right. Here’s my ad list.

Where is here?

Sorry, I dropped it in a chat in Zoom, but pretty short.

Yeah, I think it seems to be more... really to be the first node that you should describe instead of circle, because of position and the size.

So I almost did a rectangle, but then I realized it was going to be longer. Like, the example would be longer, the JSON schema would be longer, and the properties would be longer, and I aimed it. I went for terseness. And so I was like, circles only have radiuses. Done.

That’s a... yeah.

Okay, for circle, the one weird thing is that the XY coordinate is not the center but top left.

I definitely left that ambiguous in my example that I included and thought about it. I was like, Oh, wait a second. Where is XY? We needed to find that.

Okay, so what circle we have already then?

There’s actually some pretty—we did some of this work in the 0.1 spec on the core. It’s like saying, what are the properties that they need?

Rectangle is rather trivial. I mean, okay, where—

So we get it from the first spec.

Well, I’m looking at it right now. There’s a—yeah, so position and size, the other elements, which we already have position size and root. Wait, is rotation part of the core?

Yeah, cool. Great.

Yeah, then it really is, like you said, fairly trivial because position and size should cover the bounding box of the rectangle.

Yeah, but that’s also core.

Yep.

So then really, it just comes down to stroke. And this is an open question of like, what do we want to do with stroke generally in core? 

So the minimum that we came up with before is there’s stroke color, stroke weight, and fill color. And those are kind of—that’s it. And if you want a more complex rectangle, you’ll need to extend it or come up with your own extension.

Okay. So again, so we had stroke weight—

Or width. That’s a better way of saying it.

Like in SVG, it’s stroke. I would—we followed SVG here. So instead of width, we would say stroke. And that’s the language.

Yeah. Okay.

Like the last stroke color, at least.

Yeah. Stroke color. Okay.

Thanks for that.

With—yes, stroke width.

And is it a stroke? The color is just a stroke property in SVG.

Oh, interesting. Well, we don’t have to do that. We could just say stroke color.

Yeah. Yeah. Maybe we call it stroke color.

And they do the same thing for fill. Fill is assumed to be the fill color.

Okay. Okay.

Then in SVG, there’s a concept called the stroke pattern, where you have the dash pattern that defines them, that you have two colors and—

Yeah. Do we want any of this? I mean, we cut away...

Yeah. This stuff.

Yeah. So my thinking is that like every canvas visualizes strokes in subtly different ways. When—well, let me say it this way: Most canvases offer the ability to have a like a constant—they have like sort of their default stroke.




Yeah, and that might be more or less sketchy, right? Like, think about Excalidraw’s default stroke, which has like this sketchy kind of look, or Miro’s default stroke. But if you don’t customize anything, you just jump into those apps and draw a rectangle, you’re going to get a certain stroke. Then they offer customization options on the stroke. And from my experience playing with those different tools—Excalidraw, Miro, TLDraw, some of these others—the customization options are always different.

And so my thinking is we just offer the basic stroke width and stroke color. And any customization of stroke beyond that, you need to extend because I don’t know that there’s any customization that we could offer that would be consistent across canvases.

I agree. This is cool. Yeah. These three things. This is really a quick minimum.

One of the things that I noticed as we were doing this before is that stroke width, stroke color, and fill color will end up applying to rectangle, circle, probably text as well. Now it’ll be interesting—there’s an interesting question I’ll bring up—but it certainly applies to freehand and arrow, right? And do you want to put a border on your image or not? Like, we can decide about that. But it’s at least in rectangle, circle, freehand, and arrow—they have the same stroke qualities.

Yeah, great.

Sorry, freehand?

Freehand and circle. There’s just a stroke color depending on how it’s pressed.

Let’s get to freehand in a second. There’s one more thing about writing a way to talk about, which is how would you represent a rectangle with text in it?

Oh, thank you. It’s two visual nodes.

Yeah, its simplest form. Or is it a node with an asset of type text and a node with a data of rectangle?

Ooh.

Right. That’s why we did the asset thing.

Nice.

Yeah, I feel it’s nice. So it’s the visual part, which is the border of the rectangle or the circle. And then the content orthogonal to that is the hello world. And then you can change it. It’s no longer a rectangle. Now it’s a circle showing the hello world or the JPEG image.

Sweet. Yeah, I like it. I’m so glad we went this way with assets, Max, because Orion and I were working on text related to these different shapes, and we never really cracked it. Like it didn’t feel good. It was like, yeah, we could just add a text property for rectangles and you just throw it in there. And like, ah, that doesn’t feel quite right.

Yeah.

But the fact that you can have that—

The text formatting will come—

But text formatting is going to be a nightmare, and we’re going to have to think about that. But like, yeah.

What do we want to support there is a big question in core.

Yeah.

So you were just at this duplication that circle and rectangle do have quite similar properties. And I think, yeah, that’s correct. We just duplicate these properties, and that’s fine.

Because in freehand, maybe we don’t have—for to start with, we just don’t have a fill color.

That looks good to me.

Yeah. And we talked about how we would store freehand, and let’s not go— That was one of the more complex ones. We can stick with rectangle and circle.

So I just had this thought though. If you define size for a circle, the radius is applied.

Yeah.

And along the circle is an ellipse.

That’s what I was going to say. Should this actually be oval or ellipse?

Oval is nicer. And I like TLDraw because the shortcut for circle or whatever is “O.” The keyboard shortcut in TLDraw is “O” because you’re drawing an oval, not...

I don’t want to say it. It’s fun hearing it in another language.

By the way, from anyway. So we call it oval. But I think oval—I like oval.

Okay. So then, yeah. And the nice thing is a rectangle can naturally be a square, right? Like, you can—

Yeah. So the broader case of oval is the broader case. The minimal case is circle.

But I don’t think it needs a radius, right? That doesn’t make sense. We just don’t need it.

Yeah.

We just leave it out.

Okay. How dumb can you be? It doesn’t need a radius.

Exactly.

But what’s an interesting thing— Isn’t size optional?

We need to make an optional property a required property when you’re drawing—

Rectangle and oval require that size be specified.

But why?

Can we not have a default size? If it was optional for other elements, why is it suddenly required for a circle?

So we just like make it like 100 by 100. Like, default to—I mean, not crazy.

Sure. I mean, we’ve already talked about defaulting to XY and that kind of stuff. Defaulting an XY position when—well, actually, I think we decided XY is required.

Yeah. Go look at my circle without a size. It’s a point, isn’t it?

Not without our defaults.

We just made it 100 by 100, Michael.

Position.

Yeah, position. I was going to say position is also recommended, but we default to zero. So that means we need to update the node section, Max, to add a— Right now for default on size, we have N/A, and we need to now specify it.

Yeah, there it is. Line 194.

Required contents, but there is—default is the last one. I just don’t see it because it’s so crowded.

Okay. So default is the array containing this as the default, but it needs to be in these text fields.

Yeah. Yes. You got it.

Looks good.

Okay, back to where we were.

For freehand, we need this path data stuff. And the only reasonable compact version is SVG or an SVG subset.




Yep. No, I think you probably want an SVG subset, but yeah.

Is that enough? If you look at the old draft, if I’m not mistaken, you can draw one path, which has thickness in it.

Yeah.

Yeah. When you draw it with that one, pretty—I think that’s a special TLDraw thing.

Yeah, for sure. That’s a—I mean, actually, yeah, it’s kind of broader than that because freehand is its own library that Steve wrote and released independently of TLDraw, and other canvases implemented.

I think that’s where it began, actually.

Yeah, that’s where TLDraw began, exactly. So there’s probably a freehand extension that is broader than TLDraw, but it is not what we’re supporting. We’re just supporting the basic points, you know, the path data that you get with SVG.

So freehand would be another extension.

To truly—

Well, I like that better. Yeah, yeah, yeah. When I just call it path, that’s a great name.

Yeah, because path could be any arbitrary shape.

Right. So yeah, if you do it this way, as usually done in SVG, then you do have a fill color for sure, because they can be closed, and you’ll see that on the path.

Yeah, agreed.

And do we support everything from an SVG path there? So also curves and stuff like that?

Good question. Do you mean curves?

Yeah, in an SVG path, you can contain different kinds of curves. LineTo, which is a straight line, then you have the cubic Béziers, which are the first kind of curves. Then you have the quadratic Béziers, and then you have even arcs, which are elliptical arcs, I think.

Right. I think these are all SVG commands.

Okay.

And we could leave this out.

Or maybe have two different types. So we have a complex path and this simple line path because every one of these complex shapes, if you subsample and add more points, you can put it into a simple path. And these very, very simple paths that only have MoveTo and LineTo are very easy to implement for any tool. Just have straight lines. That’s it.

I mean, wouldn’t we want them to just use the SVG library? Like, wouldn’t we want to make it easy for an implementer to just use SVG?

Well, I mean, they’re going to have their own internal representation of paths. How they represent it is up to them, I guess. But we would probably—I’m thinking about how we would parse.

Like, we ran a JSON parser.

Good. I wrote my own SVG parser. It was medium. So it’s doable, but it’s not a 10-liner.

Right. Yeah. Maybe erring on the side of simplicity for implementation of both a parser and someone who’s writing a converter. And I don’t know SVG well enough to know which one—what’s simpler there.

You would probably be—since you wrote your own parser, you’d probably have a better opinion on that than I would.

What about this? We say we use the full SVG language in the path data, and we say explicitly in the spec that if a canvas doesn’t support the complex path, it should just treat every command as a LineTo. Because that’s how they are cleverly crafted anyway. They always have—you can just get out all the points, and if you don’t know how to draw a curve, draw it straight.

Beautiful.

Fine. That works.

Are we sure that we want the path in the spec itself in the core?

Yeah. That allows us to represent so much stuff. That really—that is, that’s true.

You can use that for arbitrary shapes. That way we don’t have to represent octagons and hexagons and triangles and all that kind of stuff. Just use paths. If you want to have a triangle extension, go for it. But we’re only supporting ellipses, ovals, and paths. 

And that gives you, as an implementer, a lot of flexibility. And also, you could use an SVG path to represent a freehand object. It’s just a series of points with LineTo commands. It’s not a very complex freehand that has things like TLDraw’s freehand, but that’s not for core.

That’s called perfect freehand.

Perfect. I wanted to know what it was called.

Oh, perfect freehand. Yeah.

Oh, yeah. That was the name of the library. Yep.

Well, guys, unfortunately, I do have to run. It’s been another meeting. Max, if you just want to check these in, this is a great start. You know, when you get these pushed up, I’ll see it in GitHub, I suppose, and I can edit tonight.

Sweet.

Should we also have a simple image? Images should be pretty simple, too. Although do we even need images? Can you just use a rectangle with an asset?

Ah, yeah. Maybe we need to think a little bit about how that really works together.




Touch. Copilot got it. So we have a simple line—I mean, the path is a bit like a hyper edge. And if you just need a simple line from here to here—

Yeah.

No, I think a line is a really critical one.

And then, yeah, there are arrows, which have meaning beyond lines.

All right, guys, I’ll see y’all in a couple of weeks. And I won’t close this meeting—or I won’t—I’ll actually, I’ll make you the host.

No, I don’t have a lot of time either.

We could merge the right line—I still have like 10 minutes left.

Do you want Michael? I’ll become—

That’s okay.

Because arrows are like the last thing to think about, and then we have more or less an idea for the core parts. Because arrows have these start markers and end markers, and that’s still missing and adds a host of new problems. Because obviously, these markers need to be defined somehow and—

So what could be a minimum?

What I did in my library is to say the start is representing something that’s outgoing, incoming, or not directed. And that’s it. So it’s like undirected, outgoing, incoming. So one of these keywords. And the same for the end marker, and that’s it. So if you—and the default is, of course, undirected. So then you can have all kinds of arrows. And that’s it.

I mean, every UML tool already has more complex markers like the filled triangle and the other triangle or whatnot. But this would be the bare minimum.

Yeah.

Yeah, I agree. Something like, I do want to end the relation where you have a triangle with free...

Yeah, that’s already maybe too complex for the core.

Yeah.

What does TLDraw have as default as options?

Let’s see.

TLDraw already has a lot more options but maybe already too much for the core.

What does an incoming arrow have?

Yeah, that’s a bit tricky. It has to look something like a bit like this—triangle in the line. Maybe I need to make the line thicker so that this is imaginable at all. Or maybe we’ll make it really thicker. And then it needs to look something like this. That’s actually one of the tricky things to render.

Okay. So then for the real arrow, we do it the other way around, and it should extend, of course, this shape. Maybe the idea gets a bit clearer.

Yeah.

Yeah. And that’s then the undirected sort of...

Undirected end. This is the outgoing end.

At the moment, I went into the final end.

I got direction from the first page of the arrow. Yeah, it’s setting.

Yeah. So if I write this up a little better and commit it—

Yeah.

—and we have it.

Yeah. Very nice.

It’s already way more than I’m supporting in CodeFlow currently.

Yeah. It would be interesting—how can you import other stuff that’s defined in core, and you say you claim you implemented it? So how do you import it?

Well, I have to think a bit about it. Also, yeah, with regards to the issue with interchange and interoperability, probably one—I should store a flow in the OKF format itself to keep everything within there. Because if you want to export again to the OKF format and you keep everything, you want to keep everything that you don’t support, then you should store that as well in your system.

Probably using the OKF format itself is the best way to do that, I think.

I agree. I am thinking—are we forcing every implementer to do this exactly? Because it’s almost the only way to do it.

I was also thinking I can store it next to my own format, but still, I need the important data to be able to export it back again to that same—and don’t lose any information. So why not just use OKF itself?

You need at least the same nodes. And you need to store JSON bags for them. Then you can use your own database for it or do whatever you want, but yeah.

Yeah, but what about the relations or assets or things that are in there that you don’t—

Same applies. But at least we have an overall ID scheme. They all share the same ID space. So you only need to have the ability to have some map ID to JSON blob. And then you can transparently recreate an OKF file.

Of course, you also need to remember the type of the blob you stored so that you put it back in the right arrays.

Yeah.

Yeah, I think using the OKF format as the storage format is also very nice because you’re just saving in your tool, and I can already open it in another tool even if I forgot to ever do an export.

Yeah.

So it’s nice.

Yeah, something to talk about a little bit further maybe next time.

All right. Yeah. I’ll commit this tonight.

I don’t know if I can stop the recording, but it probably will stop automatically.

And a recording is in progress. I can—can it stop.

So now I’ll implement this nice forwards. See you next time.

Yeah, see you next time. I will plan a new meeting.

