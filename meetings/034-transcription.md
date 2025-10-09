All right. Welcome to OCWG meeting number 33, I believe. It's amazing that we've spent 33 hours meeting together at this point. 34, 34. Dang. We've spent 34 hours meeting together. Fantastic. Cool. So last time we met, Max had a proposal that was working on, that was intended to allow for like multiple canvases and that would, and we were talking through the idea of, or the issues around transclusion around multiple canvases.

Yeah. No idea. Up there, Max. Okay, cool. I have topic number one would be that. Let's do that. And then topic number two is what I've dropped into the admin channel earlier of like, why not 1.0? Which is more of a signaling and forcing, signaling mechanism and a forcing function of a conversation than it would be a, than it's like a, I think it's time. I'm actually saying like, we really should ask our questions, like ourselves, why not? And what would it take to get there? And then see if there's things that come up that we're like, well, clearly it's not time because of these things. So anyway, but that's, we can do that conversation at the end.

Oh, okay. Yeah. So fitting in that idea of wrapping things up, a transclusion or including, how do I have a working transclusion? And I, I just pushed and get a new proposal, which, which I can quickly explain. So the idea is still to say, you can have a node as a resource in another node. But the technical details are now on the visual side. We say, if node A imports node B, then the app knows how to render nodes anyway. So the app should render node B as if there was no a just render node B.

And then whatever the app does, there is some kind of internal bitmap or SVG or vector image in the app, because the app needs to draw it at some point on the screen. So the app knows how to render nodes into internal bitmaps or vector graphics. So we take this bitmap or vector graphic and say, that's actually the resource we're including. And then then it's pretty straightforward. If the application can render PNGs or can render SVGs or other vector graphics, then transclusion is defined.

And what happens under the hood in this app, we don't care. Just render it and show it here. And if it's also shown there, also show it there. And if it's edited, obviously it changed. And, and that's it. The things we discussed last time are not wrong. That's probably how an app that is smart, what implemented, but the stack doesn't need to care.

Yeah. So, transclusion is like a window onto, onto a resource, which happens to be rendered by the app, and to go to the real estate, what you were saying, we're making a couple of assumptions here. The assumptions are that the app already knows how to render a node. And all of this children and all of its properties and that kind of stuff. Otherwise, how would it render it to begin with?

And so, yeah. And then the, what's the, why, why a bitmap or a vector image? I'm not sure that I follow the logic that gets you to there. Those are the only two kinds of visual systems that I know either. I mean, that that's all computers have given us. Either you render two bitmaps or you render two vectors, which you then also render two bitmaps. But you always use some kind of toolkit where you say, I want to draw a rectangle. You either say pixel from here to here or you say vector from here to here. But that's it. I mean, well, maybe there's even a 3D render mode, which, but, but the basic idea still applies. I mean, we don't really care whether it's a bitmap.

Yeah, I wonder if this is maybe, yeah, maybe I don't know how to, maybe need some rewarding. Yeah, I think I understand your intent here. Yeah, maybe, you're basically saying render it at this, show the, render is not maybe even too strong of a word, like present the node at this location using all of the, you know, the logic that you, presentation logic or whatever that you would.

There's one subtle thing because if a node shows a resource and we say the node has a border, which might be even an oval or whatever, then that is a cropping and then we have resource fit, whether it's less aligned or right aligned. So it's not showing the important node at this location. It's showing the node at some location we don't care about, maybe off screen. And whatever you get from there, treat this as a rectangular resource you're importing here, like you would import a vector graphic or bitmap graphic.

So that's really the thing. So it's different for importing a text resource because text resource, you would also render into some ultimately rectangular shape. And we were, we were initially saying when we were talking last time, we were using the language of node imports. If A transcludes C, then A imports the node C as opposed to rendering or a visualization of the node C, like in actual C.

Okay, do you have an example of how this would look in terms of the implementation difference, not implementation, the, how it's represented in the, the JSON.

Exactly the same as before. I think it is before, right?

Yeah. Okay. You just reference another node by its ID. And now I restricted IDs to be valid HTML IDs, which say, try to avoid space in your ID. And the HTML spec goes on to say, it's actually quite a good idea to use valid CSS IDs. Otherwise, you need a ton of escaping hacks. So CSS IDs are actually what we should strive for. But it's also not so important to have them. If you don't import nodes, and for some reason, you need your IDs to be very weird. It's not such a big deal.

Okay, so then node A, in this case, node A is transcluding node B. Is that right?

Yeah, from the, yeah. So in this case, you're saying that the position size and resource fit would overwrite in the same way as when we're importing a P and like a visual resource.

Yeah, this, this is not an override, like we discussed last time. This is just applying resource layout.

Yeah. So, okay, now I get the difference. I get the difference now. So you like, you're, you're basically saying, this is similar to presenting an image on the canvas.

Exactly, exactly. And so you're using that. And instead of thinking of it as sort of inheritance, where you're like, yeah, this node is inheriting all the things from this node, and it's also not a writing specific property.

No, no, no, no, no, no, no, it's just render, render the node. However you render, like, however, like you said, it could be 2D, it could be 3D, it could be bitmap, it could be vector, whatever, like render the node, and then take that rendering and paste that around almost like a stamp, boom, boom, boom, in the different places that we're importing it.

Yeah, but apply these resource fit things. Maybe the node wants to have it less the line, the other one, right aligned. That's okay. We know how to align bitmaps.

Or vectors if your canvas is vector-based, right? Or, yeah, no position size in that, that allows, basically, it leans on the pre-existing functionality of resource rendering.

Exactly, yeah. So it's like a virtual resource that gets it content from the app itself rendering it eternally somehow. I do like it that it's like really, really pretty simple. Like, there's no, there's no complexity to it. It's like, however, it's rendered over there is how it's going to be rendered over here, you can use, and you can kind of clip it, and however you would like if you wish to. Michael or Aaron, do you guys have any questions?

Yeah, if I understand correctly. So if you have a node that points to a resource, and that resource is also a node which has a lot of other nodes attached to it with edges and connections and stuff, so it's actually quite a big graph, for example, then that is makes the shrink down or fitted into that node that has the resource points to that resource.

So I want to mention something that Max said earlier, which is that if in those not being transclusion, then maybe it's not a big deal to have weird characters in the ID. I want to say actually, I think it is a big deal because transclusion is not the only case in which you want to reference a node by ID. So there's an uncountable, uncountably infinite number of ways that this could be done in the future by some future use case where they want to be able to reference something about ID.

So I think making sure that the allowed characters in an ID are sane goes beyond just this one use case and we should indeed use a sane set of characters. This allow things like hashtag colon slashes dots and stuff like that. I get the idea, but I just looked at how does HTML define IDs? I mean, obviously, HTML has IDs and they can be referenced in CSS selectors. And in order to make that work, these IDs need to fulfill some restrictions.

But then I was quite surprised that the HTML spec is not saying IDs can be this and this and this. Instead, after 20 years of learning, the HTML stack says, you know, use whatever you need to use as your ID, but you will pay for it. For example, in IDs, you need to use spec slashes to escape stuff and it will look ugly, but you can do it. We don't care anymore after 20 years of abusing. We recommend, however, to use sane IDs, which would look like this, but we don't restrict it. And if HTML does this, maybe they have a long history of learning behind it.

I would necessarily like assume that whatever HTML is doing is like a good example to follow, because consider that they have to deal with backwards compatibility of like every website ever for the past, you know, many decades. And yeah, but it came from a stricter area. I mean, in the beginning, HTML was XML or HTML and XML has a quite strict ID space, which is more or less the same as the CSS IDs of today. But then in HTML five and onwards, they seem to have relaxed it.

It was stricter before. I think HTML's roots are actually in signal, not XML.

Yeah, it's a common ancestor of the two, yes. But then for a brief time, there was HTML which tried to reunite it and then, but yeah, you're right, of course.

Yeah, anyway, but the main thing I just want to mention here is that like with HTML, we pretty much settled on the only, you know, use case of HTML is rendering it in some kind of browser environment. So the answer is just whatever. No, it's also referencing the IDs by CSS and also using the IDs in JavaScript.

Yeah, that's still in the browser. But yeah, okay. Yes. But then in OCIF file, I could imagine it could be loaded into all these different apps that do things very differently and maybe even like displayed at runtime for displaying like an interface in some kind of game engine. That's like my use cases I'm thinking of. And having the IDs be, you know, simpler and not having these wacky characters does help with some of these use cases or else I would have to like, you know, strip out columns and dots from an ID to display it in the node name.

Yeah, obviously, like control characters are completely useless in IDs. I agree.

But so how to, so if people need, I don't know, German Umlaut characters in their ID for some reason. Do we force them to escape them? Do we auto escape them? Do we recommend apps to auto escape them? Do we build a tool that auto escapes malformed IDs? And what do we really gain from that? I mean, different apps have different requirements and we cannot take the lowest common denominator in ID space of all IDs because we don't know all the apps. We cannot create IDs that just work everywhere. I mean, CSS IDs are pretty nice because they are still the age old XML or SML IDs. They always start with a letter, a Latin letter from A to Z, lowercase or uppercase or underscore. And that's about it. And then they can be followed by digits and orthopedic letters.

And the other advantage to follow HTML's lead here is it's easy to explain to people who are already familiar with it. Right, so you can reference whether it's logical or the best, the best way to do it. You can say it has the same restrictions as HTML IDs.

And that for people who know what that is and there's like existing documentation from the W3C on that, there's some advantage to that. All right, I don't really have a dog in this fight either way. I would let Max and Aaron Arm wrestle if you guys are in person. I mean, I like clean IDs, but what do you do if there's a file with bad IDs? Do we say the app should reject it?

And if it shouldn't reject it, then it does have to accept it anyway. And if it should reject it, then why? What's gained from that? And in the end, an ID is a string.

Right. And I think the difference is you guys are saying the same thing, but you're saying Max is saying should and Aaron is saying must in the language of specifications.

Yeah, I think ultimately we should acknowledge that having these weird characters and IDs is an edge case and 99% of files aren't going to do this. So it's like, who are we going to, you know, wag our finger at in school for using these weird characters in their IDs? Should we do this to importers and runtimes, have them deal with it or exporters have contact creators deal with it? Is this, you know, either way, it's perfectly valid. I'm biased towards making things easier for importers and harder for exporters, but you know, in any, any ways, ultimately, like, it doesn't matter too much. You said easier for importers, harder for exporters.

That is a good line. Yeah. That's the, that's the stance of GLTF, where, yeah, it's the same reason that like, we, you know, we only have one coordinate system, like meters and GLTF and pixels and in OCIF is that you don't want to have like some kind of unit definition at the top of the file that might make it easier for exporters in case, you know, some app has that as their native coordinate system and they can specify that in the file and keep out their numbers the same, but then importers have to convert that and that sucks. And there's, no, not really any good reason for that. Like, it could just be the job of the exporter and the exporter can handle unit conversions.

Anyway, that principle can apply to other areas. So I thought I'd mention it.

Yeah. Um, Aaron, any other thoughts on Transclusion?

Because it sounds like we're at this point talking about two different issues, which is how do we reference IDs for nodes?

Yeah, sorry, I went on a tangent there, I guess.

No, it's perfectly valid. And I'm glad we talked about it. And we need, we do need to come to a decision and just decide and document the decision. So I'm glad we discussed it. I'm, but I am curious to make sure we're all in the same page on Transclusion. Because if we, if we're, if we're good with Max's proposal, which I think I am, I am, and I don't have any further questions, then we can go ahead and document it and, you know, put it in 051.

Okay. So really quick, I do like what you wrote there about Postl's law. That's, that's good. And it has for Transclusion and having to be rendered to an image. That's like, from my perspective, that's kind of odd, but it is doable. This is like, totally something that you can like do in Giddo Engine. I assume most apps like have this capability.

So yeah, I assume that if it's being like rendered to an image that this is intended to be like a live image, like if you were to change those nodes, then the image should change. So it's more akin to what a game engine would call a viewport. Not, not a static image where like it's just, it only looks like what the, what it looks like when the app loads, because that would just be that are represented by like, baking it into an SVG. So I assume that's not the use case. So we actually want it to be a live, you know, updating image.

Yeah, that's a good term viewport. I like that.

Yeah, I just added a comment on there, Max, for your say. Thanks.

Yeah, because that, yeah, that that definitely reading it the first time confused to me, but I understood the point of what you were saying, which is viewport is a good way of thinking of it, or like view into.

Yeah, and to your point, Aaron, it would be like a live view, you know, editing, editing a would then edit B, if we're like, yeah, would, would immediately, the appearance of the B would immediately reflect whatever changes to a happened.

Yep.

Also reminds me of iframes and browsers.

Yeah, that's also good analogy.

Yeah, that's a very good analogy.

Yeah, because especially because HTML handles the rendering of the iframe, the iframe's contents in exactly the same way as, as if it's a standalone file that's not being iframed into.

That's good stuff.

Cool. Okay, I think we're, I think we're on the same page here for max. Do you need any other help for 051?

I was noticing.

Yes. One last thing about transcription and in detail, there may not be loops in the transcription graph, because otherwise, it's not defined how to start rendering. Should we mention this in the spec, or is it obvious? Is it not defined how to stop start rendering? Well, if A is transcoding B, B is transcoding C, C is transcoding A, where do you start creating actually an internal render?

You start at the outer layer and you work way down. I mean, it is, it's cyclic. What if it's cyclic?

So I think the way that the browser, I mean, Orion might actually be able to speak to this. I would not be surprised if Orion had made built a transclusion, or a cycle using i-frames in a browser before. That would seem like something he would do. But I think the browser.

I called it. Is it rendered up? Like it limits render depth, right? It does. But things quickly break just because of the overhead of i-frames.

Yeah. So great to have you on the call, Orion.

If you're curious, I put in the zoom chat the exact language that GLTF uses in its spec. The node hierarchy must be a set of disjoint strict trees that is node hierarchy must not contain cycles, and each node must have zero or one parent node.

That's probably what we need to define for parent child and for transclusion.

Both trees need to follow the structure. Yep. Both are trees at the end of the day.

Yeah. At least they should, uh, must, must.

That sounds good. Cool. I copied that.

Great.

All right. Thanks for that. Okay. That's transclusion.

Then, um, we should review the whole spec at some point and make sure that it's somehow coherent because we now just shuffled all core extensions and extension extensions together as extensions. And it is a single document by now what we've never reviewed it as much.

Yeah. I think you're right. I think there's a review step coming. I think the other thing is, I think the way you have this set up.

Yeah. You have, you're creating like a brand new 051 draft. We should make a 051 branch that's a copy of main that like a 051 draft branch and then your 051 should merge into that branch. That way we can see just the diff. We should read this top to bottom without reading just the diff, but that would give you a nice clean diff.

Yeah. But yeah.

And then we can review both the diff as well as, uh, read the whole, um, uh, spec top to bottom. It's a large diff this time due to the merge.

Oh, yeah. That's a good point.

Because the extensions empty file is now part of the spec empty.

Right. Right. Yeah. So be it. So be it.

Um, hmm. Yeah. Then one other suggestion, um, don't have to do it, but it could be helpful. It could be helpful to do a 051 draft branch off of main, do the moves of all the files as a PR and go ahead and push it into that 051 draft and then do the another branch. Don't only do this if like cloud code or Jim and I can do it for you, like don't spend time finagling with get. But if you could do the edits onto the moved files in that branch as a separate PR, then it would make reading the actual diffs possible.

But again, um, does that make sense?

I think I get the idea, but it's still quite some manual work because I also think editing this structure, but only do it if, if like, cloud code could do it for you of like, um, anyway, um, no worries. Not a big deal.

Um, yeah. Thanks for putting this together. Um, when you're ready for a top to bottom read through, let me know.

Um, Max, and I'll, I'll volunteer to be like a reader that reads from beginning to end for cohesion sake. Um, happy to do that and give feedback. Just let me know how you would like that feedback if you wanted his comments on the PR or whatever.

So.

Yeah, comments worked, but good.

The tooling is great.

Yeah.

Okay. Uh, the next topic that I wanted to talk about was, uh, my shower thought of like 1.0.

Why not?

Um, and, um, why, what would it take for us to feel confident saying, okay, we're at 1.0.

Um, and we're going to kind of, here's the version that people can start implementing now.

Um, I mean, we're already saying, you know, try it out.

Um, but instead of have, you know, I think the value there is basically saying we don't expect to make significant changes to the spec at 1.0. You should just use it as it is.

Um, and if we do make any changes, they'll be largely backwards compatible.

Um, well, the common yardstick is to have two independent implementations using this spec.

And if that did work and the spec didn't have to change it a lot, then the stack seems to be reasonably stable.

But before that, it's quite likely that there will be changes.

Sure.

So I don't like that kind of yardstick we can do.

All right.

I'm good. I am.

Are there other things other than that?

Or is that kind of it?

I think it'd be, it'd be nice to do a review, maybe even a slightly longer zoom call and get some other people to kind of go over it with as a, as a bit of a group process, just as a kind of collective sanity check.

Um, like maybe we can, um, ask Brooke to come on, for example, um, and other people that have had experience doing spec writing and, and might find some glaring issues right at the bat.

Yeah. And Brooke actually volunteered for that.

Um, I requested that she, and she said she would absolutely be fine doing that.

So we can get in touch with her and set up a call.

Um, and it might be that, you know, maybe two or four week, maybe it could be probably one of our regular calls, like we mentioned, all right.

It might be, it might need to be longer than an hour, potentially, but, um, but we could maybe do it at a regular time and then just extend it by 30 minutes or an hour or whatever for those who can stay.

Right.

Yeah.

Yeah. I think that makes sense.

I think, uh, LLMs can do a first round of review as well.

I use Gemini on smaller specs to, to give feedback, identify contradictions.

It's a good, that's a good, probably a good idea to do that before, um, Brooke reviews that way we, yeah, obvious things we can address or at least have a list of those things and that we share with Brooke ahead of time.

If we haven't resolved them, then yep.

For the implementations, what, what can we do to, I mean, could we try to generate some kind of tooling that does something with ocif files?

Yeah. I mean, I think, should we just connect two existing apps to ocif, like Obsidian and Teirdro or?

Yeah, I think in my mind, it's just build and, you know, do it for Obsidian, do it for Teirdro, and then you're, you're pretty much there at that point.

And we can, I think the way that, I know you, you said that keyword max independent implementations, um, and, and I think the way that we can have it be, uh, independent, so to speak, is having a deployed website similar to what Michael has put together for tooling in the past, where you can kind of utilize the tool to do transformations, two-way transformations.

Drop a TL draw, get an ocif, drop an ocif, get a TL draw.

Drop a TL draw, get an obsidian, drop an ocif, or obsidian, get an ocif, like having that as a utility that people can then use.

Obviously, if we have it on a website, then we should probably have it in a CLI tool as well.

But I think those, having tooling that people can download and use and/or hit on the web and use seems like a good way to have a implementation that isn't necessarily internal to TL draw or obsidian, but still has some testable, verifiable utility for people outside of the team.

Yeah, that should be enough.

I mean, it's the tooling manages to capture all the difference between TL draw and obsidian nicely, and it does work, then obviously, ocif seems to work.

Exactly. And at that point, it doesn't really matter whether Obsidian integrates it into their software as a first-class like file save as or file, or it would be ideal if they did, and it would be easier if they did, if we have the tooling available in TypeScript, it should make that process easier for them, and the same goes for TL draw.

But even having it external, because we've talked so much about interchange rather than a very high polluting form of interop, it's still going to enable people who are motivated to do the interchange between the two programs.

I kind of feel like there's another kind of independent that's actually maybe more important, which is having like at like an organizational level, having different people that are largely like, that don't have the same information in their head, independently implement it as a test of not the specification as like an abstract design, but as a concrete like kind of proof-by-demonstration of what's actually written down, and that people end up with something independently or mostly independently, that is the works, and it's compatible.

It's clocked for that other, let me say this.

I think for example, Chi might be down to do that. I was actually, Chi came to mind.

Yeah, if they would be down to do it, that would be fantastic.

Orion, I haven't chatted with Chi in a month or two, do you want to reach out and see if they're interested?

I think we are at the point where we should have someone should do that work.

To see where we are, which is kind of why I was pushing on this topic, it's like, okay, we're kind of at 1.0 minus some things that we can't entirely control.

What can we push so that we are making those external things happen?

And then what things are within our control that we're just not paying attention to was kind of the impetus for asking this question.

Yep.

And then it also came from recalling that manifesto for standard makers, where he's basically like just, I think he said like, yeah, perfection is a waste of time. What was it? Just like, freeze the spec.

He's like, get to a point where you're just, just say like, we're done. This is it.

Provide an extension mechanism, which we already do, so new ideas have an outlet, but just get, just freeze it and say we're not going to move it. So there's some value in that.

Yeah. Other thoughts on 1.0?

I think that's nicely covered.

One, one other person that might be down is Mime Mime. I don't know why I'm liking on how to pronounce his name, because I worked with him for months.

But he, because he already did a prototype implementation at tail draw.

And I think he would probably be open to doing a bit more on that. I can also, I can ask Steve, I'll be in London probably in a few weeks and was planning to meet up with Steve as in tail draw Steve.

So I can also ask if he can kind of, I guess, give permission for that work to happen on company time, which I think would make a big difference, as opposed to asking someone to, you know, spend a couple days of their own time.

Yeah.

Well, hopefully less than a couple days.

Yeah, hopefully some of that. That's a, well, that'd be great. I think that makes ton of sense.

I've got a question. What do we expect from an independent implementation? How, how big or small should it be at least?

I mean, it's a great question.

I think in the ideal case, it covers, the implementation covers all the features in that particular canvas. That's, I mean, that's should be obvious, but maybe it, maybe it's not as in as much as like Ociv seems to cover those features, then it should, it should cover them.

And I think a really, one of the reasons I say that that's the ideal is if there are things that it seems like Ociv is not able to represent, that's one of the most important pieces of feedback we can get is I went to implement this with my canvas tool, and I had no idea how to do feature X. And, and so I didn't include it in the Ociv file when I exported it. And so now we have some like lossy inner interchange. It'd be really good to know that I know why and see if that that feels like one of the obvious gaps in the spec.

So any other thoughts on that?

There will always be some level of loss, but it is important to make it our goal to minimize that whenever possible.

Only.

Yeah, I exactly, Aaron, I was thinking more along the lines of at least we could then say, we are aware that you can't represent this thing, this kind of thing in a canvas in the Ociv spec and we're okay with that. So I think something to be aware of that came up, actually when Chi was doing an implementation, is that they ran into issues that I think would not have happened if they weren't doing real time interrupt, that if it was import export, Chi would not have noticed some of the nuances, I guess.

And so I think we should at least be cognizant of which thing we are validating. Because I think it's good to kind of target interchange is in a more manual, non-reactive import export type interaction. But we should, I hope, also optimistically plan for the ability for people to do real time interoperability on top.

And so we should at least be aware of if someone is actually helping validate those things or the kind of non-reactive static interchange. So like, whether the spec is successfully preventing or, or like maybe in the worst case, like by design necessitating some infinite cycle, right?

Well, like if you try and build a reactive system around it, you actually can't without violating the spec in some way. I don't quite see how that would happen, but I think it's complicated enough. We would only already know that by having it implemented.

That's a good point. It definitely feels like interchange though, the import export functionality is the first step on that path of like, you need that anyway, in order to do real time interop. And so starting there, if we can get to there, then we can figure out that next step as well.

Which is interesting because I do remember cheese implementation was more, it was focused on real time interop. So he only implemented one feature or two features or three features, and then kind of had that as the demo of interop, as opposed to implementing the full set of features for import export, like deep instead of broad.

When I'm working on other conversion issues, I'm often creating a set of test files for a certain format. So it's not easy to handcraft test files for all these features we have. Also, it's hard to describe what should happen with them. I mean, at least in a formal way, you can try to load them and not crash, but what actually should be visible on the screen is a bit harder to fully describe.

But as soon as we have some implementations, we should somehow have a set of test setups that will then draw into your drawer and export them all, document them, and then have this suite of test files being used to validate the obsidian import, for example. Something like this, it's more than examples, I would say. It's really a set of test files, and if you can read these all, then the chance of having bugs is low. So it's a, yeah, like a test suite or a set of test files.

Yeah, if you want to be a certified Java machine, you have to pass this oracle test and pay thousands of dollars.

Yeah, I was thinking about fragment testing as well. That's not necessarily something we need, but would be pretty powerful. Basically, you could go from one system to another, like do the round trip piece, and let's say this is field draw.

Not full files, but just a node. Well, it would be full files. What's in those files is the big question here, but like going from obsidian to tail draw, and then back to obsidian, and then the rendering should be exactly the same in obsidian at step one and step three, like, you know, like once it comes back.

And why do you call it fragment testing?

Yeah, because fragment testing is a way people use, what am I trying to think of, storybook tests on the web, and storybook renders the actual components, and then saves that rendering as an image, and then reruns it, and it does image comparison to make sure all the pixels match, and if pixels don't match, it highlights, hey, this little rectangle should hit the right a little bit. So you we could have some that would be an incredibly robust set of things of like, you know, run a run around trip, and then test to make sure that the rendering is exactly the same pixel or pixel. That may not be necessary, maybe it's just literally comparing the file itself.

Yeah, the similar different ways to encode the same visual

I mean, if the IDs are no different for the nodes, but it's still looking the same, most likely file comparison should be.

If the files are identical, then we have one, but if the files are different, then maybe they're still okay if you if they look the same.

Yeah, that's a good point.

I guess there is more than one way to represent the same thing.

Yeah, in respect, so.

Yeah, like the order of extensions in the extensions array or whatnot.

Yes, exactly. So the comparison is going to be a little different. It can't be just like a character per character comparison, it has to be like an intelligent equals. All right, so it sounds like we have some to do's here.

I'm going to put together like a project plan in GitHub. So I think like first we're, let's get 051 out the door.

And then I think it's Orion is going to talk to Chi and Mime, or Mime, or however you say it from tldraw/steve about independent implementations.

And then I could probably look at an LMP back review, what either you or Mimex, one of the two on that piece.

And then once we've done that, reach out to Brooke and see if we can get her on the calendar.

And then, yeah, one small change, I think would be nice is in the spec text, the text node and one on the node has like a question mark after it.

And I think that'd be better written as like text in quotes, because the intention is to say that text doesn't really exist as a node, but putting a question mark after it makes it look more like it, we're unclear on what text is.

Yeah, I got to sit back. That makes sense.

Yeah.

Wait, what are you merging, wouldn't you?

Cool.

All righty.

Anything else? We've got a few more minutes left.

No, actually, add quotes instead of dropping.

Okay. I didn't fully understand what was being said then. Add quotes?

Yeah, to say text nodes. Because we don't have text nodes, but text nodes.

Got it. I understand.

Or maybe make a sentence of it instead of adjusting text nodes.

Yeah, definitely have the examples are helpful.

All right. Well, we don't have anything else. We can end a few minutes early.

Thanks, y'all. And, yeah, look forward to next steps. Talk soon.

Yeah. Bye-bye.
