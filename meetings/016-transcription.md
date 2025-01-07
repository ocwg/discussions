Here’s the transcript broken into paragraphs for better readability:

---

Oh, well.  
All right.  
Let's see.  
Go.  

Adoption.  
Yeah. And then since Michael, you're the first adopter, maybe we should just talk through if you have anything that we can help with immediately, like what's your impressions immediately, and then we can talk about getting other folks on onto it.  
See, you want to start with what you were saying about relations?  

Yeah.  
I'm already very impressed with what you have, I think. But I think for sure, we need more examples. Also, in this book itself, there's also in the repo repo that will help.  
I agree.  
That's my main thing.  

What do you need examples of? What have you found yourself?  
Like, er, I don't know how to do this. How should I do this? What?  
Yeah. Which ones?  
Yeah, exactly, that you can see what the spec-- the output of the spec is if you were in Pima, if you want to export to the OKF format, how should it look? Exactly.  
Not just the spec, but also examples.  

There are some examples about simple nodes, for example. That's a fun example. But I think we need much more. For every element that's in the spec, we probably need an example, I think. And maybe even a document that has everything in it so we can see how everything links together.  
That's a great idea.  
Yeah, and everything in the kitchen sink document would be really--  
Yeah. That's a great idea.  
[INAUDIBLE] Maybe later on, if there's somewhere a possibility to validate an export and document, that's also great. That's maybe a bit more of a longer term.  
Yeah. Maybe not that important to build.  

What would you-- Michael, what would you want to export to? Like, what would be the first place you'd want to take something out of your program and put it into something else and see it like a full interop scenario?  
What I've already done myself, I can also export to the L drawer. I've used it in the past to see how an export from my tool to the L drawer looks like. And then you can see it in the L drawer. So I think that's very nice. Although, other tools can be nice as well, but--  

No, it would be good to build around your use case to begin with, since you're already using it. And so, yeah, not that TL draw is like the be-all-end-all, but if that's what you're hoping to take that out of your tool and drop it into, then we could start with a TL draw converter of O-Kiff to TL draw.  
Yeah, what I like about TL draw is that it's so easy, simple application, but still very powerful. That's really good UX, way better than my tool. I'm jealous.  

Wouldn't you need an export from O-Kiff to TL draw and from your tool to O-Kiff so that you have the chain?  
Yeah, I think that's for O-Kiff, very good. If we have something like that, not just for my tool.  

Yeah, Max, what I was thinking about was writing the O-Kiff to TL draw leg of that. So it'd be on him to get it out of his tool into an O-Kiff form, and then I'll write the O-Kiff to TL draw.  
Now, that doesn't solve the round trip of whatever I can't convert to TL draw format. TL draw is not going to keep those nodes around if it doesn't understand them, so we still have that. It's not a full implementation, but it's at least a one way. You can go from one tool to another tool.  

Yeah, but we could try to also have an import from TL draw, which also makes it easier to test the export. The round trip is definitely the golden possibility there.  

One thing I thought about trying is some kind of merge of, like, I mean, tell me if I'm crazy here, but I'm thinking of-- remind me the name of your tool. Michael, it's slipping my mind right now.  
Codeflow Canvas.  
Code flow Canvas, yeah, that's right.  



Do you separate Canvas from Codeflow, or are there--  
Yeah, Code and Flow are also separate words.  
OK, Code flow Canvas. See, I was thinking something like Codeflow Canvas to an OK file, and then going to actually TL draw, and then saving the TL draw back out again, and then merging with, like, make some changes, and then merge this OK file, merge these two, and see what happens. But also, back to Codeflow Canvas again.  

And then go back to Codeflow Canvas. But even just seeing-- so, like, going from OKF to TL draw, if there are things in Codeflow Canvas that TL draw doesn't understand, which I'm assuming there are, do you know what some of those things are?  
Yeah, I've got some way to represent. Yeah, I think I can render that totally to TL draw, but something that I have are compositions, and I can use compositions.  

You can enable code, you can compare it with functions, of course, but those compositions are also a set of nodes with connections between them, edges between them. But you can have the same composition multiple times on the canvas. And then you change that one composition, all those other compositions also have that same flow.  
And I think TL draw does not have something like that. It has groups, but when you clone a group, you make a copy, I think. When you change the group, it doesn't change the copy, if I'm not mistaken.  

If you change the group, it doesn't change the copy of the group.  
OK, so you almost have an idea of inheritance like this. There's object A and object B.  
Yeah, it's more like a subflow that you can use. And if you change that, they can be nested as well.  

Gotcha. Would you want to show your screen real quick and show what you're talking about?  
Yeah, let's see. All right. I just allowed-- you might have to hit screen share again.  
Yeah, but I can. Yeah, let's see, I'm sure.  

And I'm also still thinking how I should implement-- how I should export the compositions.  
Yeah, let's talk about that. OK, let's see. Where did you have one?  
This blue box has a composition. When I edit it, I can--  
Oh.  
Interesting.  
I can go in further. This is a nested composition.  

OK. But when I make a copy of this composition, this is this-- if I change this composition-- composition, this is also changed.  
Ah, interesting.  
Let's see.  
[INTERPOSING VOICES]  

Visual node is visible in two places, sort of.  
Yeah, the definition of this composition is the same. So is it showing the same resource?  
Yeah. And if I look below a memory, this is stored in the index, in the bars of a storage.  
No, I was using the terms of OKV. So is the same visual node-- two different visual nodes rendering the same OKV resource.  

But this is used to model your use case.  
Yeah, I don't-- there are now two compositions, because this is another composition. That's the same. But what do you need?  
OK, so what's in composition? I probably will export the compositions to resources and OK format.  

But in a composition-- so this eight E3 thing is a composition. So a composition has an ID, has input nodes, has a name, has nodes, has output nodes.  
So it would sort of benefit from being a visual nodes or relation concept to be linked to the other things and not just stored away in a resource.  

So maybe it should be modeled as a special node or as a special relation.  
I think as a resource, because if in the OK format, you would render this as a node, then you would also have to put these nodes in that node.  
But the other composition that would be exported as a separate node with the same--  

With the same set of nodes, you've duplicated the nodes now. You do it on the duplicate, duplicated.  
Mm-hmm. That's why I was thinking of still having nodes on exporting the composition node to the OK format, but put the reference to a resource in it. And the resource contains the flow of that composition.  

A simple work?  
Yeah. Go ahead. That would work, but it's like the base case. So it's like a hack to use transclusion, because we only have that defined for node showing resources.  

But what you have in your resource is not an opaque image, but it's a highly connected entity, which really suffers a bit from being modeled as a poor resource. You should worry more live on the nodes and relation layer.  

So we could add a new concept. Let's say we could say we have a visual node, which isn't showing anything except the stuff that another visual node contains. So that way we have transclusion on the visual node layer.  

We just say we have a node extension that says I'm just a delegating node. All my properties are taken from here, or maybe some of my properties are here.  

So the next question is, do these two blue boxes with a label test? If I change one of the test labels, is the other label changed?  
Yes. Should be? Probably if I refresh, or no?  

OK, so that's an entity of the composition itself. If I resize the blue box, is the other blue box resized accordingly?  
Go ahead and resize those boxes.  

OK, so at least I have an independent position. So they are not completely identical.  
So would it make sense for your use case to have them resized independently? Or is that?  

I think that’s just a question. I don’t know.  
Yeah, in this case, I think in this case it should have the same size. But yeah.  
OK, because it’s not user-resized at all, because it has just automatic size and the same quantity to the same size.  
Yeah, in this case, it has done by the system.  

OK. I have notes that I can resize. And I can imagine in the future that these compositions also can show content from something that is output by the notes under the root in this composition.  
Currently, I don’t have that, but I can imagine in the future that I built something like that. So then they want to resize them independently.  

And then they would also look differently but contain the same computation notes inside.  
Yeah, and depending on the input, the output is different. That’s also already what you see happening here. This is the same computation, but the input is five. And the output is an object of AMD. But the output is different.  

If you understand what I mean, see if I can replicate. So in your JSON, we see already the four properties of the composition. And then you have probably somewhere the instances of the compositions as well.  
No, I don’t have the composition themselves yet here. In this--  
No, in your own JSON. I mean, in your code.  
Yeah, in my code there is.  

But we just saw that they-- Mm-hmm. This is the-- All the stuff inside these two compositions is properties of the composition itself. So what we see on the screen is like a visual note saying I contain a composition. And that is another complex note or relation.  

I’m not sure yet with all these things.  
Yeah, but these two compositions-- It’s really different than this. Let’s start from scratch.  

This composition has a flow in it. And that flow also has a composition in it. So this test two, let’s see. This test five is the composition that’s used on the parent flow. This test two is a different composition.  

Nested composition. That has a difference from--  
OK, is that-- Sorry, that’s-- Crows even more to model it as notes, because notes can contain notes, can link to notes, and resources cannot.  
Yeah, and don’t have to be notes.  

These notes, this composition notes should be in this list somewhere. Let’s see that that’s why, for example. And then you have this concept in your program that-- another concept that TL Draw doesn’t have, which is related to compositions, which are-- it’s like an entirely different canvas.  

Like when you go into that composition, everything else goes away, and you’re resizing things on a new XY plane, that kind of thing.  
And so how have you handled that? How have you thought about handling that with TL Draw that you would just put them on as-- like, TL Draw has pages.  

Would you use a separate page? Would you use-- and I’m not thinking about, OK, for right now, I’m just thinking about, how would you even export that? Just put it in a separate spot on TL Draw’s canvas, on the same page.  

Good question. I haven’t told you about it yet.  
Go ahead, Max.  
It’s just zooming in.  
Oh, OK, yeah. That’s true.  

That’s true. Yeah, that could be-- I haven’t told you about the most natural thing for it, zoom-up look kind of.  
Yeah, yeah, especially for TL Draw. That would be the most natural thing.  
I mean, interesting.  

Yeah. Huh. So you were, Max, I think you mentioned an idea about how to handle sort of-- how to generally implement Transclusion, and I’m not sure I 100% followed you. Can you say it again?  
Yeah, the idea would be to say we have a node extension that says some of my properties come from another node, especially, for example, the resource, which I’m showing, or other stuff.  

We need to be careful how to specify this extension to distinguish what remains separate from the template node. I mean, it’s not template. There’s one node that acts as a holder. It has its own--  

OK, it’s the holder. You added fairly late in the process. I remember we talked about it last meeting.  
Yeah, we don’t have such a holder yet. I’m just imagining it right now.  

So imagine we have some kind of a holder node, which is a visual node. It always has its own position, and maybe also its own size. And then it can, for its other properties, delegate to another visual node.  

So it’s like the data node. We have a holder node and the data node. And the data node is another visual node. But it has a property to mark it as--  
Non-visible.  
Or usually, un-visible. It can also be visible. I don’t care.  

And then you can say, OK, here my box is showing the stuff from that box over there. And whether that box over there is hidden or not, so it’s another decision.  
That’s a great point.  

If you simplify thinking about this down to what you have right there inside Test 5, is you have two-- if you open it up, like that value type box on the left, that thing exists in two places kind of thing on the canvas. Inside Test 5 here, and then inside Test 5 in that other flow.  

And so really, the question, an even simpler question, is how can you show the same node twice on the canvas, such that if you edit it in either place, you’re editing the other one, which is Transclusion, like you mentioned, Max.  

And it’s like that generalizable capability would give us the ability to do everything else, I think.  
Yeah. The question is, for example, should we translate the size from the other node or have its own size that may be use case dependent?  

Yep.  
What other things? A position must be unique. Otherwise, it doesn’t make sense to everything of the same spot.  
Shouldn’t the extension kind of allow you to specify which properties you want to translate?  

Yeah, maybe. Then we also have to list the properties that you want to translate kind of thing?  
Yeah, yeah. But we have to look how that plays together with other extensions. So if an extension says, I am defining ports, but we didn’t say we want to inherit ports, then--  

Right. I mean, we should probably default the address. Maybe. Let’s look at what a node really has, and then decide how to handle it. So if I look at our basic node in the spec, how do we have it?  
Yeah, I have the spec up on my screen right now.  

Yeah, a node. OK. So we have an ID. Should be unique. Position should be unique size, debatable resource, debatable data.  
Yeah, these are the extensions. Should we exclude extensions or not? Rotation could be own or transcluded scale again.  

So we could-- now, the easiest would be to have a list of non-transcluded properties, or even simpler, if a visual node defines properties on its own, then these override the transcluded ones. So if I have a node that has no position, but it has a scale and a transclude from somewhere, position doesn’t make sense, but everything else.  

Yeah. Transclusion.  
Yeah, position seems like the only one that we would want to, by default, not transclude, because then, like you said, it wouldn’t make any sense. They would be on top of each other.  

Yeah, you want to have different-- yeah, so by default, position differs. Everything else, I think, copies over is transcluded between the two elements, or the n number of elements that are transcluded with one another, including everything in the resource bag-- I’m sorry, everything in the data bag.  

So all-- by default, every extension will be transcluded across all of those nodes. I think that’s the thing that makes the most sense. But you can omit. I don’t know.  

OK. We’re doing it. And so the special rule of position is weird. Maybe we should also allow overwriting position. I don’t know for which use case.  

Then maybe if you transclude again and that other node then has-- can that translate from multiple nodes? Is transcluding like transitive kind of thing?  
It must be transitive for sure.  

So there’s a really interesting case of this in practice. You guys use Notion, and it’s synced blocks feature.  
No.  

So you’re probably familiar with Notion. Like, it’s a pretty standard document editor out there. You guys heard about it?  
I do sit already, but--  

OK. I don’t know what’s left right now. OK, so they had this really interesting problem of like, they wanted to enable transclusion for the purpose of you could edit something in one document. And you could include it in several different other documents as sort of a window to that item, you know, to that.  

And then you could edit it in that one, go back to the original place and edit it, and it would update standard transclusion stuff. And so that’s a pretty powerful feature.  


And the design decision they had to make was, does a transcluded block exist in the original location? And that’s sort of the root or the origin or whatever. And then it’s transcluded to these other locations. And the other locations are special, because they’re not the origin. They’re like mirrors of the origin.  

Or is a transcluded block an abstract entity? And every location that it’s visible at is the same. It’s just a place that is visualizing that one, transcluded entity.  

And it has very practical ramifications for the UX of like, am I-- if I delete the block in the original, in the origin, does it get deleted everywhere else? Or because I’ve removed it from its original place?  

Or does it stay in all the other places? Because it was just this abstract block that is now visible in these other places. So in that sense, it’s not gone. And which for a user, that would kind of be surprising of like, I created it, I created this whole document, I transcluded this little section of the document, and then I intended to delete that section of the document.  

But because I had transcluded it to these other documents and they could see it, now I’m going to leave it there in those other documents, even though I deleted it in my origin document. It’s like, yeah, anyway, there’s some kind of two different ways to think about this.  

It sounds like it’s comparable with the composition concept that I have. But I’m--  
Because if I’ve just-- I don’t know if you just saw that. But I added this expression node to the composition. And it’s now used by both of these nodes.  

And if I would remove it, then it would be removed for both. And you can see it in the results here. It was 10 and 100 and 10 before I added that expression. And now it’s 16 and 100 and 16.  

So if I remove it, then--  
What happens if you create a composition? What happens if you remove the-- you create a test-- you create a composition. You copy that composition. You delete the original composition. Does the copy get deleted? Does the copy stay around?  

If I remove this, then this will stay around.  
You’re not sharing your screen, by the way.  
I’m sharing mine now. So sorry. I just thought.  

Oh, wait. No, you are. Sorry. I think I am sharing.  
I don’t apparently support multiple screen shares now. I didn’t realize that. My bad.  

But yeah, sorry. So you deleted one and the other one stayed.  
Yeah. And currently, even if I were to remove this one, then in memory still exists. I don’t support that yet, that I can remove it. Remove it totally. There’s just references with the global compositions stored.  

Oh, if I would make some copies.  
So the reason I brought that up, Max, is because you were asking about translating a transcluded node like--  
Yeah.  

And in the case of translating a transcluded node doesn’t mean any-- you’re transcluding the original node. In the case of it, it’s an abstract entity that can be represented in multiple places. There’s no difference between the original node and the transcluded node. They’re all the same node. It just happens to be visible in all these different places.  

Yeah, but if they have a different position, and maybe a different size, maybe it could limit it to these two things, and say transclusion can only transclude position and size.  
You mean only position and size can be not transcribed?  

Yeah, yeah, yeah.  
OK, so this idea of overriding extensions is also tricky because what if I want to overwrite just one extension, but not the other two, which I’m not aware of?  

No, that’s a good point. It starts to get complicated. If we just say, but OK, what about the ID? Every visual node has its own ID different from the transcluded one, obviously. Then position, we could say it’s always different for simplicity’s sake.  

And size, well, there, maybe it’s optional to give them their own size, but probably would make most sense to just give them their own size each time. And if the application automatically determines the size, then it should also know about its own transclusion, and set it in all transcluded nodes.  

I mean, how did you handle it in your current code, Michael? Do you just have one item into a lookup? What’s the size?  
Yeah, these nodes have their own position and their own size, but the size is determined in this case by the system.  

But if I would make this user-resizable, then they have their own size. The only thing they share is the flow that’s stored in the composition store.  
And the name?  

And the name, yeah. The name is also from the composition store. I think if you look at how the composition node itself is exported, let’s see where it is. This is the composition, one of the composition nodes, I think.  

Do you see it has a position, it has a size, although this is system determined. But also, it’s also stored on the composition level, over the node level, and here’s the one here. This is a different node type. These are some properties, the ID that the composition and the composition ID.  

So this is the ID that’s used in the composition store. So this is like what’s transcluded?  
Yeah, you can think of it as the ID of the node that’s actually being transcluded.  


Gosh, that’s interesting. So then we would represent the node or nodes. Let’s just use node for now that’s being transcluded as sort of-- like you said, Max, it could be invisible or visible. And then everything else is a transclusion of that single node.  

But the weird thing is what happens if you delete that node, then all those transclusions are like an empty pointer or a hanging pointer, dangling pointer, whatever you call it.  
Yeah.  

Like you would want a cascading delete, basically.  
Yeah, so if these are semantics of a transclusion, then the original-- yeah, deleting the original node causes deletion of all our transclusions of the node.  
Yeah.  

So then is an-- Max, are you thinking of it as an extension of-- it’s a node extension.  
Yeah, why not?  

And it’s an extension that can be applied to the node and all of the transclusions of the node. Like, I’m trying to think of what the properties would be. The node ID that is the transcluded node.  
And what if you are the origin node? Then you don’t have a node ID. It’s null or nil or whatever.  

No, no, no, no, the extension is only used on the transclusion nodes, not on the original nodes.  
Got it. OK. Now I’m tracking you. OK. That makes sense.  

So the original node is just any plain node, which may be visible or not, we don’t care. And then we have the transcluded node, which is a node using a transclusion extension. And in there it lists one node ID of the transcluded original node.  
Love it.  

And it usually should have ID position and size.  
Yeah.  

Yep. And that’s good, because that’s what our required and recommended fields are-- or properties are for nodes. If you look at the spec, that’s-- and everything else is optional already. So that feels great.  

Some nice-- in the case of compositions, you could represent those-- here, how I would think about representing those now, if we assume this new transclusion extension is the test 5. When you had two test 5s, those are relations. I would call them group set relations or whatever that has a set of nodes in it.  

And then the nodes that are inside test 5 are transcluded between all of the instances of test 5.  
Yeah.  

And all these nodes, that’s-- for example, if I open again, open again, this parallel node, that’s when I would export this to the OK format, would also be on the root level. But the special flag that’s invisible.  
Oh, I see what you’re saying.  

I think Max was saying that you might have only two-- what was that node called again? Position, not position. I don’t know.  
Yeah, you would have two nodes that say that are parallel. One is the original and one is the transcluded one. If you have two copies of test--  

No, no, no, no. Michael wants to transclude the whole group. So we have one parallel. Now we are inside the test 5. Test 5 contains. He’s using nesting at the same time.  
Yep. Yep.  

So this parallel and this value type enters test 2, all the three elements, they exist once. Then group them using a relation.  
Ah, OK. I see.  

And then we need-- do we have something like a container node where we say one node contains the other nodes?  
Yeah, that’s what we do with the relation, right? So we do the relation. So we create one holder node to put the other nodes inside using a relation. And this holder node is the original for our transcluded and the two test 5 things.  
Yeah.  

Could be any symptoms. Oh, yeah. Nice. Because they’re contained in the same thing, you just transclude the holder node.  
Yeah.  

No, that won’t work. Well, yeah, yeah, because we talked about you can do x, y offsets within the holder node. I was thinking about where you would put the parallel needs to be in two different places on the canvas.  
For that, we just used a relative offset extension.  

Yeah. This is quite a test already.  
Yeah. Michael was like, hey, this one. This one thing is not in TL draw. Boy, pull the thread.  

Yeah, I did this composition thing. It’s something, especially nested composition. It’s been something I’ve been working on during the holidays to get some stuff working. It already gave me some headaches. But I really wanted to make this work. I don’t know why exactly, but I just like the concept.  

So back to the general transclusion. Right now, we do not prevent to transclude transcluded nodes again and again in the log chain. We could say that a transcluded node should not be a transcluded node itself. But also, we could also know it. I don’t mind.  

Yeah, I don’t mind. I think it would be one of those things that we recommend that you-- the normal user intention is probably to transclude the original node rather than the transcluded node. And so you probably-- there’s probably not a good reason to transclude a transcluded node. But it’s not disallowed by the spec.  

I guess this will be an extension. This is a helpful case. I can imagine that in my case, I think I go into half that, something like that. But I’ve seen some movies demo from Toadpond, from Lu Wilson, from TLdraw.  

What has this mirroring effect? She made this mirroring effect. I think it sounds a bit like that. But that’s not essential.  
Yeah, that one does feel like transcluding transcluded nodes.  

Yeah, that was a nice demo. But it’s also adding an effect via transcluding. That’s-- if it’s really mirrored or just the same.  
There’s several of them that she showed off. One was adding rotation each time.  

And so as you rotate the base node, it multiplies or sums the rotation across all the other nodes. So you can make a flower effect all the other transcluded for one another. You rotate that one, and it rotates this one, which rotates this one more, which rotates that one more. And you get these really cool cascades of effects.  

OK. Yeah, really cool. I’m noticing we have like five minutes-ish left. This was a super interesting use case that we definitely, I think, transclusion is going to be a general thing we’re going to need to support. So I’m glad that came up.  

Cool. What other things should we be focusing on around adoption? Certainly getting an email newsletter out that lets people know that we’re following along, that 0.2 is out there and is ready to be played with.  

Michael, do you want to record a very brief little demo video or something like that that we could drop into Discord or something like that that shows where your app was 0.2?  
Yeah, that’s a good idea. I wanted to make some recordings now and then anyway, for my project. And I’ve planned to make a recording again soon about some stuff that I’m working on. But yeah, this is something I can do, for sure.  

I was also thinking I’m also on the future of code Slack. I don’t know if you are familiar with that.  
Yes, I’m on it as well, yeah.  

And because we can also post a link there, because it’s quite a big community, 3,000 people, I think.  
And totally right up, right up their alley. That seems like a great one to post in there. I’ll let you own that one. Feel free to do that whenever you’re ready.  

I’ll own the email, getting that out the door. And, yeah, I think, what else should we be focused on? Examples?  
Yes, examples, yes.  

Max, would you mind putting together just a single example of how you would like it structured? Or if you already have one in there that you say, just follow this pattern, wherever. I’m happy to write some of the examples. I just need to know.  
The tricky thing is to have an example that uses all core features. And then for each section, strip it away. Only show that part. And then he’s back together.  

You’re right, using all core features. Also, what is especially core and what not. We have this shifting boundary of what is built in.  
Right, OK.  

That’s a great point. I’ll see. Yeah, I might be able to take a crack at that. Add an everything document.  
Yeah, the minimal document that uses all core features. And then the next step is the minimal example that uses all extensions we mentioned in the spec.  

And if we have that as a JSON file, it should be really easy to craft parts of that for the example sections.  
That’s a really pragmatic way to start. I like that. Just get the JSON file, and then we can figure out how we want to turn that into documentation later.  

Yeah. To turn it into documentation would be easy for me. But to come up with the first example, using everything and also sort of deciding, do we need to include this in the core? Or can we leave it out? This is a bit--  
I can be the design question.  

I can be the initial decider, and then we can argue about it.  
Yeah. Hell, that’s always good. Happy to do it.  

Yeah, whenever there’s a, like, where should we go out to eat? I’ll just say something just to get it started. We’re going to that restaurant. Any problems? All right. No? OK, great. We’re going. Or yes, great. Let’s talk about it.  
Yeah, that’s good.  

Cool. And then we talked about the whole page to have it maybe add a validator. That’s certainly a good next step to have a validator. And then the next step after that could be converters.  

So somebody exports TL draw to its native format. Then we have a converter that can convert TL draw to OKF and PEG.  
Yeah.  

And then we have, like, three formats and can do I/O. And already we can connect tools in arbitrary weird ways. And then the tool authors might come over and say, hey, maybe we should integrate this into our tool.  

So this could be a way to get adoption started, especially with tools we would like to adopt first.  
Yeah. No, I think a validator-- I’m sorry. I can’t write the code right now for a validator. But when I say right now, I’m in the next week or two.  

I just have a particularly busy beginning of the year. But-- and I’m going to make sure that we get the newsletter out of what we have already done. Make sure people know about that.  

And then look at work on the example docs or the example uses of the-- because I do think that’s one of the things like Michael mentioned that people will immediately ask.  
Yeah, that’s suddenly the near-term goal. But you asked for year-long goals. And that’s maybe one to convert our code.  

I agree. Yeah, no, I think OKF to TL draw, two in from TL draw, would be huge. And then having a validator and updating the homepage. Probably want to be have some examples that we might even be able to use something like cursor to create a validator for us.  

That’s what I’m hoping is-- yeah, once we can-- if I can feed it the spec and some examples, how good of a job. Can it give me 80% of the way there? And then I can work out the fiddly bits.  

I was just trying it with the ChatGPT with the current spec. And it does even do a nice job already from creating some JSON.  
Max, you’ve written such an LLM-readable spec. Well, well done.  

Now, because that happened, maybe LLM still help in the creation of the spec already. Perfect. Awesome.  
All right. Cool.  

Well, I think we’ve got marching orders for now. Max, do you want to own-- I saw you seem like you were taking some notes around the transcription.  
Yeah, at the transcription extension.  

Great. All right. Fun times-- let’s get some people using this thing. We’ve already got one implementation with Codeflow Canvas. How great is that?  
It’s a good way to get back to me here. That’s also something we should celebrate on the homepage.  

Oh, heck yeah. Absolutely. All right. Well, talk to you guys soon.  
Yeah, have a nice day.  

Yiddie. Bye.  
Yep. Bye-bye.  

