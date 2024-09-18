
All right, welcome to OCWG meeting number 10. If you're watching the recording, this is meeting 10. I'm trying to come up with an extensible interoperable specification for helping infinite canvases interop. I'm going to share my screen real quick. We have a TL draw canvas that we're using as a note-taking canvas for this meeting.

There's a couple things if you're watching the recording. You can find out most everything you need to know at canvasprotocol.org. Probably already know that, but if you don't have that URL, that's the main one. That canvasprotocol.org also links to our GitHub organization, github.com/ocwg, and the slash spec repo where we're iterating on the spec. So yeah, hopefully those links are helpful.

There's also a—if you want to find out more about what happened in the previous meeting, you can go to the OCWG or GitHub org discussions, or the canvasprotocol.org website also has a link to this discussion. But it has notes and a recording, and as well as an image of the TL draw notes from last time as well.

All right, so let me see, drop. So I figure in terms of today's meeting, we don't have any instructions because it's just the three of us; we already know each other, Michael, Max, and I. I think we'll just jump into working on the spec this time, which will be actually nice, since we don't have a whole lot of questions to answer.

All right, here's a—I'm dropping a link to the TL draw. Michael and Max, if you guys want to jump in there, you're welcome to or not. Totally fine. I'm not sure how much I'm actually going to end up using the TL draw today, since we're going to be looking at the spec itself.

All right, yeah, I saw your PR jump out. So let's go to GitHub real quick and merge those back to one file. You know, this is this file that I just put that on the—I just made a commit already. This is the combined files together. Great. I use that myself to do testing, so I still had it—

And—oh, gotcha. You have a schema-combined one. Perfect. Any reason to maintain the different files as well? No, if we are going to use this, then no. Yeah, probably. I did make one change to one of the files. So if you checked in this combined file without pulling in my changes, then you are missing one thing, which is—

I added the—actually, let's just talk about stuff we've added so far. So some changes from this morning. I'm going to go to the version that's easy to read real quick, the preview version. Yeah, I just did some generic cleanup of notes that were in here. Michael, you were saying you weren't sure what this file was for. The way that I think of this file is sort of the human-readable version of the specification that would hopefully provide you a plain language.

I can just read through this top to bottom and understand the spec without having to just go read Jason's schema, especially if people are not familiar with Jason's schema. But even if people are, this gives us an opportunity to describe and prose some elements of the way that the spec works. And then Jason's schema feels more or less to me like an implementation detail, as opposed to the thing that you should have to read and learn to understand how it works.

Yeah, I agree. Yeah, in the initial draft branch, I think the reading was empty. Oh, there was not much in there. Oh, that's true. You're right. Yeah, you're right. In the—[INAUDIBLE].

Yeah, in the main branch currently, in fact, that's probably a good argument for at some point we should bring this PR back to the main and then just start branching off, doing short branches off main, as opposed to this long-running PR. I don't know that the long-running PR is granting us that much benefit right now. But we could probably do that today.

And once we get it to a state where we feel like it's at least internally consistent and flags things that we know are open questions, I'm OK with merging it in with open questions, especially if we've said we're not sure how to handle this section. And then call that out in the markdown file.

So I'll kind of go from the bottom. I cleaned up the motivation and design goals section, which we had some of this information in there already. I modeled some of it after the GLTF documentation. There has been around a lot longer and is a lot more mature and more formal. And they actually acknowledged that in a couple of places here, like we're using formal words and language, that kind of stuff.

More in line with the way that like NFC—not NFCs—what are the—RFCs. RFCs. Thank you. More in line with the way that RFCs are written. And so I'm going to try and keep OCWG in informal language for now, given that most of this is to support a conversation that we're having about the design trade-offs that we need to make.

And then when we can kind of upgrade—hey, Aaron, thanks for coming. We can have upgrade. But my house randomly lost electric power, so I'm actually on the hotspot right now. Are you—do you happen to be anywhere near the East Coast? Where are you? No, I'm in California. OK, gotcha.

We're having a lot of storms on the East Coast. I've also lost power like twice in the last two days here in North Carolina. That's what I was asking. So hopefully you get power back soon.

So Aaron, I was just mentioning that I did a bunch of work on the spec, and over the last 24 hours bringing in some of Michael's work, and then also trying to rewrite some of this to at least make it internally consistent. And I guess our goal today would be—I dropped in a couple to-dos, so if we could just work on those directly during this call, that'd be great.

And then maybe even close this long-running PR and bring it back to main, as long as it's internally consistent and highlights the areas where we don't know things. So top-level structure now after our conversation last week, I understand it to be this schema version may or may not be important, but my understanding is that we'll basically have four arrays of objects—nodes, relations, resources, and schemas.

Now, my lack of understanding about the way that Jason's schema works means that I'm not exactly sure how this schema's thing is going to work, like how we'll refer to them, how we'll embed Jason's schemas inside of a JSON file, and how we'll represent them. I mean, I can sort of squint and see how it works, but I'd love to have an example in this file, which we don't have yet.

But the nodes, relations, and resources is a little bit more fleshed out in terms of—yeah, go for it. OK, the combined schema.combined.schema.json file that has references to sub-schemas. You can have a depth section and point to them. Gotcha. The depth and reps thing that you were talking about.

Yeah, exactly. Cool. But in terms of conceptually, does everyone agree this is where we are? Am I—we're at a place where we got four arrays, nodes, relations, resources, and schemas? Yeah, the schemas, if that needs to be an object. But yeah, I don't know yet. Agreed. That's the one that I'm least certain of.

But it seems like the way that we're talking about using handling assets as a set of resources that nodes point to, it seems like at least these first three make sense. So let's go through the nodes real quick. Yeah, so anything that's visible on the canvas is a node, period. And then actually shoot.

I should rearrange this, such that resources is next to nodes. I mentioned it here. In order to enable net asset reuse, we distinguish between a node with a location on the canvas and a resource that that node displays. And so I really need to kind of collapse those into one thing, even though they are in two different arrays.

Well, sorry, one section in this document to aid with people's understanding of it all. In terms of the—I went to start to convert these types, which we had due to familiarity. Orion and I had written these as TypeScript types. That wasn't meant to be prescriptive of any sort of implementation or anything.

This was a language of describing a specification that both Orion and I had some familiarity with. And neither one of us were very familiar with JSON schema. So the one thing I didn't have time to do or the skill to do this morning, because I still have some learning to do, was converting this to a JSON schema.

However, when I looked at how to convert this type to a JSON schema and looked at your JSON schema things, I find TypeScript types to be much more human-readable. Even if you don't know that this is TypeScript, this sort of just makes sense, at least to me. It'd be just my familiarity with TypeScript; I'm not sure.

But in terms of having a document that is easy for people to read and to comprehend, to understand how the spec is orchestrated and how it works, I was planning on using JSON schema since that's going to be the underlying tech for the spec anyway. But after I saw it, it's just kind of ugly and kind of verbose and doesn't read very well in terms of an educational tool.

So I don't know if you guys have thoughts on using JSON schema, using TypeScript types, or if there's another way to better represent the structure of the spec. Thought probably did this. It's very interesting for me to look at this TypeScript thing that you've written, because from my

 perspective, this is kind of in between the kind of two human-readability levels of definition that you would find in the GLTF world.

So you've seen this game as a course; those are very verbose, and they are not very human-readable; they're designed to be machine-readable, although a human can read them without too much difficulty. And then what's actually designed to be the tool that educates the person on how the spec works is the readme documents with the pros and stuff.

And those usually have markdown tables that describe the properties. So in the markdown table syntax, the typical way to write a number—if you want to say like an array of three numbers, instead of writing bracket number, comma number, bracket—in a markdown table, you would typically write number, open bracket, three, close bracket, for example.

In a number of three, you'd be like the number of elements. But in this case, it would be like you'd have to say like number three or number two. Got it. And especially in the GLTF world, this is very sensible because like we have like that you're looking at right now, like Vek3 and Vek2 and Vek4 and stuff like that built in, like inherited from OpenGL.

So like a tube element array of numbers is like a very special thing of Vek3 too. Got it. That makes sense. Yeah, that makes a ton of sense. In fact, I'm inclined to try rewriting these as markdown tables as well. I think that makes a lot of sense.

And it heads more in the human-readable direction. And that's exactly why I didn't want to bite off the JSON schema, at least in the readme. Like you said, you can learn to read it. And like even reading it in a couple of hours this morning, I was already starting to get a feel for it. I'm like, oh, this is getting easier to read.

But ideally, no matter what you do, don't copy-paste the JSON schemas into the readme. It's just like an unsightly mess if you do that. For real. So what I was thinking about doing actually was having a link from this markdown file straight to the JSON schema for people that are inclined that way.

So there would be like a markdown table version. And then if you would like to read the JSON schema, here's the—you can just go click on that and jump straight over and have at it. If that's helpful for you. Absolutely. That's the same thing I do.

Cool. OK, cool, cool, cool. I'm actually going to take some notes here. For me, from a coding perspective, the TypeScript version is much more readable than the JSON schema, also probably much more for me than the markdown tables, I think. I agree with you, Michael, here.

As a coder, I think reading the TypeScript type is actually maybe the nicest and most precise. It gives me all the things I need to know, like what's optional, what's not, how is the next thing done, what are the properties named? Yeah, it's interesting. So we're serving two different audiences with GLTF and infinite Canvas; like the infinite Canvas people tend to be web developers.

That's not entirely—that's not 100% true. Obviously, there's some native infinite canvases like Muse and Cosmic and all these others that aren't necessarily written in TypeScript themselves. But yeah, there is definitely familiarity in the audience that we tend to work with with TypeScript types. I'm going to look at it in markdown table form and just kind of see what it feels like.

And maybe I'll post a discussion post about it to GitHub and we can kind of compare the two. It's also possible to have both—well, you can also look at it at different levels. Like, first, I need some introduction. OK, what is the node? What can it have? What's conceptually behind the node?

And I don't care if it's such whether the coordinate is an array or is x, y, z. But it has always x and y coordinate and the z is optional. That's what I need to understand conceptually. And that is best written in markdown.

And then this TypeScript type is a very nice, concise summary of what I just learned, maybe, or maybe it also belongs to another file already; I'm not sure. And it's very nice at the design stage because it's so compact and easy to change. And then the JSON schema is really the best way to nail down every last formal bit of what in JSON actually is going to happen.

Like, can this array ever be empty or is it always present or whatnot? Let's give it—I think the TypeScript types are really useful as a kind of not quite an implementation, but a gateway to that. And even though it may feel redundant to have the TypeScript types and the schemas and a markdown table description, it's actually not a bad thing because this is similar to like, like, Cronos providing example implementations of GLTF.

Like, just because this way we're providing, like, an example of how to implement this in TypeScript. That's a great point. And there actually are some pretty good tools out there for taking a TypeScript type and generating a JSON schema. I'm thinking of—because—but I'm thinking of a fact schema and some other things that are easier, easy to build a tooling chain around, a tool chain around, of like, you know.

So we could maybe decide around, like, what is the source of truth. But at this point, right now, the specification is so small that keeping them manually up to date is fine. And we're still in the, like, swishy design phase as well.

Another idea is that long-term, what you could do is you can set up just a CI check to automatically check that the structure of one is identical to converting it to the other. Yes, I can already see how we could do that. Like I was mentioning, that's great for that kind of thing.

Does the TypeScript type contain a description of the property, or is it just like what the properties are named and what types they are? So unfortunately, TypeScript types do not. But they don't contain what's called annotations in the, like, types world or whatever. They don't support annotations, sorry. But the effects schema does support annotations, and effects schema can generate both TypeScript types and JSON schema.

So that would be an interesting way to have a single source of truth effectively. And an effects schema looks like a TypeScript type from a—yeah, from the way it's written. Cool. OK, that's something to play around with. I'll take a look at that. And that's really great feedback from all of you guys on what you're looking for there.

Orion, do you want to say hi, or are you just going to lurk? I will mostly be lurking. I'm in the middle of a very loud apartment. It's sad that I had to miss the Lost Equals, but also very, very cool to see or step it up and doing all the organizing stuff. I feel like this project has been in very safe hands with me gone absent for a little bit. So that's been nice. And I'll be settled in New York in the next few days, finally. So I'm looking forward to that.

Fighting. That's great, man. We look forward to it. Well, lurk and enjoy and safe travels to you. [LAUGHS] Oh, OK, so yeah, I was just mentioning that nodes refer to resources. And I realized that relations in terms of the order of the document comes before resources. I really should pull the resources up into the relations. So let's jump past relations real quick and jump down to resources.

One open question—yeah, it looks like I didn't put the to-do in here. In terms of how—there's a general question I have about IDs. And I'm curious, Erin, maybe you can enlighten us on how they do it in the GLTF world. But obviously, allowing people to pick their own IDs. For things, there's the possibility of collisions.

These aren't like auto-incrementing IDs, so to speak. And if they're not UUIDs or some other thing that guarantees or strongly suggests that there won't be collisions, we might end up with some weird problems there. So I was thinking about that.

So the way GLTF does it is that there are no IDs and everything is referred to by index. And on one hand, that is a really compact representation of the data. And so it works fine for most use cases. There are, however, some people in the GLTF world that are annoyed by this, because if you're trying to uniquely refer to a resource, there's no way to ensure that you're getting the same one if you have a different version of the same file, maybe you removed the item at index 0 and then the index of everything else shifted.

Or if you were trying to merge files, you would not be able to keep track of things externally. It would just be you have—each file is internally consistent, but any other tools trying to reference the file may have issues. And so that's an ongoing discussion in the GLTF world, is like, if we should have IDs and what are the consequences of how to do that.

Go ahead, Max. Yeah, semantic web is taking the exact opposite approach, like you use globally unique IDs everywhere. And the big benefit is you can then squish two files together, and things that are denoting the same thing are actually merged together correctly, and the other things not. And the way that is actually often done in practices, you have some kind of web document, like you serve maybe your file on the web or you have it on your hard drive.

And that establishes a kind of base your ID. And then the local IDs are then appended to some base your ID to just simply go at them and give them a stable global URI. This is not without problems, because if I take a file from the web

 and now it's on my hard drive, then now it has a different ID. The local ID still works.

So for us, if we would say IDs in a file should be unique, period, use whatever string you want, then people can use full URIs as the ID if they want, or they can use local strings and some base your ID. This would all still be open. But it's also in JSON-linked data, or this ID is a very important concept to have IDs of some kind.

So anything. And we have this relations part. And this relations part where we want to state relations, that sort of screams to look at JSON-linked data and linked data in general, because relations—that's what Semantic Web stuff is about to encode relations.

So the way that the GLTF does things is fairly limited in its ability to compose files together and refer to other things in other files, especially if we want JSON Canvas to be able to do things, like reference other canvases. For example, maybe you have a sub-canvas in your canvas. In that case, a unique ID would be much more robust than an index.

So I would vote for having IDs, and not auto-incremental integers, but string IDs that are unique. And it's up to the implementation how to do that. So question, if we only have IDs, maybe the data structure holding those should be like a dictionary instead of an array. Yeah, we discussed that, I think.

And I forgot why exactly we voted to have an array instead. I think in the end, it's a pragmatic reason to be able to stream data, to copy-paste data, and to just have self-contained objects within the array that have an ID, which makes it easier to debug. Otherwise, you would have a redundant thing to have the ID as the key in the dictionary and, again, in the object.

So just have it in the object, and just have an array of objects. That's a good point. Yeah, I think that's—the last thing you said was the reason we ended up going; it felt redundant, the key to the array. In fact, if you go back to our commit history, I think when Orion originally wrote some subsections of the markdown file, it was a dictionary with the key being the ID, and then also having an ID property for each of the nodes.

But I suppose the ID part is redundant. Part of this, I guess, would depend on how—yeah, I'm not—sorry, part of it would depend on how JSON schema supports that. I think we'll just have to document in the specification that the order of the elements in the array doesn't matter.

Yeah, I agree. The weird thing is JSON-based in Canvas. Actually, the order of the elements in the array is the Z index, which is even weirder. It's interesting from a human-readable standpoint of this item comes in front of this item on this 2D canvas based on the order of the items in the array. But yeah, we definitely don't want to do that.

All right, now we discussed that already a little—some time ago, because some tools have a special index for that, the other, for example. Yeah, that was actually important. It does not depend on all of it. The nodes is—I guess we actually need a Z index.

We had talked about maybe using Z as the thing. And then I think we decided that that's probably a faulty way to manage it. Yeah, because fundamentally, this isn't even about giving it a position. It's about just determining the render order of these elements. And especially the hitbox of when you're clicking at an element and the two elements are on top of each other, which one should resolve first.

It's really what Z is often used for, beyond rendering. Also, I will mention that in Guido Engine, the 2D objects do have a Z index. But then if two things have the same Z index, then the position in the hierarchy does matter for determining which is in front. So in that case, if I imported a JSON canvas into Guido Engine, I would kind of be forced to make the ordering of the nodes matter.

Interesting. Theldro has a specific algorithm for the Z index. Great. Let's see if I can find a link to it. It's in one of our past notes, our past whiteboards. Let's not go down the Z index just yet, because I really—two things I want to make sure we have time for is Max to share your learnings on JSON LD, JSON linked data, and then also make sure that I'm capturing things correctly around resources. And there's a couple of things I want to discuss here.

So last time we talked about how resources are the assets that nodes display. They're stored separately so we can reuse them. So you could have multiple nodes pointing to the same asset. And one of the common use cases we thought about on infinite canvases are when you're using shapes on an infinite canvas, you often have a shape that's kind of reused in multiple places, like think a star or some other SVG object. You might want to have 57 of those stars, or another common one would be what's it called? Sticky notes. Sorry.

Sticky notes are like a common thing you might want to reuse. And some canvases might have a PNG of the sticky note. Others might actually have a sort of different representation. But the resource there would be reused all over the canvas. And so having that be stored in a separate array at the base level that could then be referred to by nodes seems like a good approach.

We had talked yesterday, our last time, about having a URI and an optional MIME type, where MIME type can, in some cases, be inferred from the URI. And that was kind of the MIME type inference rules were one of the things that was hanging me up as I was writing out this section, so we can kind of walk through those. But were there other properties that we discussed resources having either all the time or optionally that I missed?

So I looked into this part. And actually, if we say that our nodes are referring to resources and resources can live on the web in the file or next to the file, then if we forget for a moment that we're doing open canvas, what we're doing is we're taking a bunch of web resources as a snapshot in one local storage file. So it should be possible to write a web server serving that local file as resources.

So you do HTTP GET and are talking to that single JSON file. That should work. And that is a good way to think about it, like, OK, so if that should work, what do you need to know about resource typically besides the content bytes, MIME type, which you get as a ref sponsor. And most results about caching, actually.

So does it make sense to have an age of the resource and some cache headers so that the smart client can say, yeah, actually, I'm getting this resource from the local JSON file. But I know I could get the fresher version from there. And my resource is just a week old. So I'm not getting the fresh one or I'm getting the fresh one. So it's caching at all a topic for us.

Because for the web, usually it's a big topic. And maybe we can just ignore it and say no. That's a really good idea. JLTF doesn't have this, but that's a neat idea. It is neat. I wonder if—so I think, let me make sure that we're thinking about it within the context of the motivation and design goals.

We're trying to come up with a format that's used for interchange or transmission, as what JLTF calls it. So I can get these things out of my canvas and then get them into your canvas. And the assumption is that each of our canvases is going to have a different runtime and a runtime data model that they're using internally.

And probably not using open canvas internally as their sort of internal data structures. And then they'll write to open canvas as they export that item or be able to import and kind of convert between their runtime and this interchange format. And I'm trying to think about that use case within the context of caching.

It seems like what you're saying, Max, is that we could provide an additional piece of functionality of hosting an open canvas file, like hosting a set of resources from the file itself, as opposed to taking the file and converting it into an internal data structure within the runtime of a single canvas. Slightly different use case, maybe. Or like—

Yeah, that was not even my idea. But what you just clarified about the goals we have, I think it follows safely that we can completely ignore any caching aspects. So if I model something in my tool, it's a local resource that doesn't exist on the web at all. So I stored in the open canvas file, you open it. There's no other place you could get it from.

So caching is just not involved at all. And we don't have to care about it, which I like in order to keep the spec simple. One thing that we could do, though, that would open the door for this is we had originally thought of resources as not having schemas associated with them. And then we said, you know what? I think we thought of all the relations—sorry, not resources, relations.

We'd initially conceived of relations as we'll just specify the three different types of relations. Full stop, we're done. And then, you know, someone on a call was like, well, why don't we just make relations support schemas too? And that way, if people think of another type of relation, they can extend the relation.

We could potentially do the same thing for resources. Like, resources also support schemas. The base type is OCW resource. And it only has these few fields on it. But if you wanted to do more, you could make a resource that you could make a resource schema that supports caching and these other elements to it.

Potentially, even beyond hypermedia formats. OK

, maybe that's a version two feature, then? Though I'm also thinking about the extensibility that you could extend the resources, or maybe the whole schema itself to implement something like that. So let's talk about extensibility.

I looked into JSON schema LD and JSON schema and then semantic web stuff. And we have schema and schema version as two properties. And I think we shouldn't. Why do we have it as two properties? We want to, like, signal, look, dear human. Actually, this is the same schema, but another version. So it's quite similar.

So for the machine, it's OK, what is quite similar? I cannot rely on anything. Anything could have changed between version one and two, so for me, it's an entirely different schema, technically. And for the human to encode this version information, this is actually similar to the old one. Yeah, you could just use a similar string to the old one.

You just have a V2 in the string, or a date, or whatever. But I think two properties just complicates everything unnecessarily. And in sake of simplicity, I would vote to merge it, actually. I think we even talked about potentially having the version be part of the name itself.

I think we just did a lot of points. Maybe by convention, it has some format that's easily human-parsable. So it'd be like OCWG/arrow:1.0. Actually, a common way to encode the version is to use a date, like year and month. And if a new version comes out, usually you have a different year and a different month.

And that, for humans, establishes a lot of context about the schema already. And for the machine, it's two different strings, which makes it clear it's a different schema. Actually, a little dash between the 24 and the 09 would be not—yeah, that's nice. Cool.

Yeah, so that's like the high-level thing. If we just have schemas, then it's also much easier to make a schema URL, because it encodes everything about the schema in one URL. If we just have one identifier for a schema. Yeah, that makes sense. And then we could, in the best case, have resolvable schema URLs.

So something like JSON protocol.org/namespace/so-and-so, dot JSON. And if you get that URL, you get the JSON file. Can you say that URL? Again, I'm trying to figure out what are the chunks that you're referring to? You need to domain. Like I can't have a product of work.

Yeah. And then usually you have a website there, and you don't want to mess up your website and your technical documents. So you do something like NS for namespace, which is similar to hosting your images. That's where you host your namespace stuff. And then beyond that, you have what you need to have, like maybe schema name.

Something like that would resolve to everything within the OCWG namespace, so to speak. Let me talk about that. Yeah, I'm not too sure about arrows and colons in the URL. Right. Add signs and colons I meant. Maybe just you will save encoding chars. Yeah, it's a good call.

And then at that page, you can serve like an HTML document explaining this stuff. And if somebody comes with a content header, except JSON, then you serve the case. That's a cool idea. Yes. That's like the perfect way to do it in semantic web stuff.

I think a JSON schema that works the same if I'm not mistaken. Most likely. So the lone hacker just enters the URL, gets some human-readable document. And the mighty machine sensor different header and gets back the JSON schema. That's a nice way to have only one URL.

And usually, if you do the exception, the JSON thing, the server just sends a redirect to the JSON file, which is somewhere so that it's normally linkable for humans as well. True. Yeah, so that's about schema names, schema URL, URLs. And then should I briefly explain the ideas behind JSON linked data?

So what we have here is we have like our conceptual model. We have nodes. We have resources, and we encode them in JSON. Some parts in JSON have an order. And we don't mean the order, like in the array of the nodes. We say that array order is not important to our conceptual model; nodes are just there.

But JSON has an order. So that's a slight difference sometimes between what we have in our head and what we put in the file. And for JSON linked data, the main idea is to say we annotate the JSON so that we can transform it to RDF. And RDF is a completely different thinking world.

And RDF, you only have triples. So to give you a primer on RDF is you have something that has a URI, so that you can identify it. And then you link it to something else that also has a URI. And this link, in order to characterize the link, you use a URI to describe the link type. So you have URI, URI, URI. That's like the basic kind of webbing linking stuff together.

And then to have these things be something and not just be linked—I mean, that doesn't make any sense to just link your eyes together. You also want to say, OK, actually it has a name. And then you also have a property map. So the thing, URI has a property and a value. And the value is a normal, I think it's XML types. So you can have strings, longs, what you need.

And the property names are, of course, again, your eyes, so that they are unique and don't mix. So you have two kinds of triples, URI, URI, URI, or URI. And I call it literal, or value. And that's like the basic data model you have in the semantic web. That's all.

And it does map to what we want to describe. We can express our current data model in semantic web structures. We can say we have a node, and that node links to a resource, and that resource has your URI property. The resource has a so-and-so property, so that works. And then the idea is to—these, your eyes are very cumbersome.

They are long and ugly. So usually what you do is you establish some kind of namespace. And there you have a long piece of URI and a short suffix. And this long prefix, you abbreviate it with a few characters. Exactly like we did in our examples with OCWG.

So it's a replacement map where you say like this OCWG or this arrow thing actually means this URI, and then we put something behind, and then we have the full URI of the property or of the resource. And JSON link data gives us ways to annotate JSON so that a compliant processor can extract valid RDF from it.

But in order to make that really work, one should not completely ignore the RDF model. And especially the properties and the resource, they all have your eyes. If we flirt with using that conceptual model, then we get for free to have properties that have unique names. And I have some notes here which show syntax examples how that would look in our case.

And I think if I show that it might become a little bit clearer. Great. Check where I have to go. You're also welcome to drop it into a GitHub discussion post. If that would be helpful, either one. Yeah, there are still unpolished notes. But how can I actually share my screen? Oh, let me give you one of these.

Ah, OK, I have to give you that. Actually, let's see more spot my share and share. I have some share button now. There you go. So what about this screen? So remind me a couple of silly questions, Max. Like, when you say, use JSON LD, JSON LD, do you mean that—how does that interact with JSON schema?

Like, I mean, OK, yeah, like, what's the relationship between JSON LD and JSON schema? None. [LAUGHTER] JSON LD is like a—is that—in my understanding you correctly, that it's a way to write JSON that's sort of like a subset of—it constrains the way that you structure your JSON. And then you would use JSON schema to describe the schema.

And so they're completely disjoint, but they— Yeah. Now— They are disjoint and can play together, but not very, very nicely, I assure you. So let's assume we have our sample JSON file. We have some nodes. We have some resources. I left out the other parts.

Then how would we model this as JSON link data? We would have to have a context object. It's always named at context. And it actually defines these key mappings, like how our vocabulary lives at Canvas protocol, blah, blah, blah. And it annotates sort of how our structure maps to link data.

And then as you see, the JSON we have looks as before. Because these annotations map everything to the correct URL. Like in the nodes, the ID maps to the property contains node in the namespace of our vocabulary, blah, blah, blah. So how does it look in—so this would be like how RDF sees what we've wrote in JSON.

So we have some document, and it contains the node. It's the node number one. And the node number one has a resource, and it's actually the resource number one. Resource number one has a content type. And we find that we set this here, and we mapped the properties, two namespaces, and so on.

So every valid JSON file which we write would need to have this header so that the other parts are mapped correctly to JSON link data. And there are many ways you can craft this header to make it shorter or different. So this is like the shortest way I've found.

Because this leaves the other JSON exactly unchanged. I'm not sure if JSON schema has sort of the ability to say, actually all valid documents that exist having our schema implicitly

 have this header. Just assume it's there. In XML, I think this was possible to imply elements or at least attribute values. For JSON schema, I'm still a noob; I don't know.

Do we really need to include this in the documents? Or can we sort of imply it? So then I asked Chet GPT to say, OK, now I need a schema describing my JSON link data. And I'm not so familiar with JSON schema, but I think this turned out to be astonishingly ugly and convoluted. So it's not nice.

And comparable, the schema for just JSON is much more sane. So they do play together, but just describing what you put here in context, this doesn't make so much sense. This is then more or less the normal schema, as we would expect for this part. But we could also think about to say we don't use JSON link data, but we get inspired from it and say actually having a context object.

I mean having a context object and map some prefixes to longer forms is OK. And then we use them in the file with, as property names, we would say, base column content type. We're talking about the base and the mapping. Is that kind of like the registry that a GLTF maintains?

No, no, this is the base URL of the document itself so that when I use SNID hash mark this, it knows how to resolve it. OK, so the concept of base URL is really helpful in semantic web context, but not required for us completely. And vocab maps like just every term that has been used to the same spec.

And you could define other namespaces here. Like you say, actually, max reserves to max funny little schema, and then you use resource max colon content types as something for max colon rotation and max define the special rotation system for notes. So just having add context and then define key value pairs and resolve to namespace prefixes would completely disambiguate our URIs, our properties already.

And yeah, I have not fully understood how that plays together with JSON schema then. Aaron, have you come across JSON LD in the GLTF community and are there? Yeah. So yes, so there is an extension for a GLTF called KHR XMP JSON LD, which is encoding XMP data inside of JSON LD.

And what they're currently using it for at the moment is copyright metadata. So it's like listing licensing information, like what licenses it under, who owns it, who is the author of it, what's subject is it in. And this is all defined by the DCMI licensing metadata.

And before Max explains the benefits of JSON LD, I had no idea why this was done, because the KHR standard doesn't say when you should use JSON LD or what it's good for. So I was always confused why they didn't just put a regular extension for copyright with just data directly in JSON instead of layering together these five standards together: JSON, JSON LD, XMP, DCMI, RDP—there's—

Yeah, so— Yeah, the thing behind that is Adobe uses RDF to have metadata about copyright information PDF files. And this RDF data now for copyright data is sort of standardized, but in RDF. And in order to express this in JSON, you need something like JSON LD in order to have a container that is JSON-like and holds the RDF data, which is already standardized.

But standardized not as a JSON schema, but standardized as RDF structures. So it's a bit complicated. I mean, like the text file we use is just holding the JSON data for us, but we're not looking at it as like a text file. Then you can encode in JSON RDF, but not looking at it as JSON, but as RDF structures as this URI structures I've mentioned.

And what we could—now we have like two options. I think for the relations part of our standard, we need something like JSON LD probably, not 100% sure, but it would be really helpful to have the bridge there. And now we also need an extensible way for JSON, like some kind of extensible JSON.

And learning from the Cronos group, they actually use two extension mechanisms. One, this homegrown with the prefix and the underscore and the central registry. And one, they embed JSON-linked data because they have to in order to represent this RDF stuff from copyright information. And we could maybe go for just one of these mechanisms and use only JSON-linked data as the extension mechanism.

But I'm not sure if that's a good idea because JSON like LD provides several mechanisms that in a lot of cases are just not necessary. For example, the distinction between arrays being ordered and being unordered, that's all at a time not necessary at all. Maybe we can also just make it more similar.

I mean, if we say we use your I keys and use a syntax to abbreviate them to shorter namespace prefixes, and that's it. So we don't need a registry because we use your I's. But also we don't really use link data. We just steal that property mapping idea. So the case of what we would have, yeah, I have to write it.

So it would look very much like in the Cronos groups examples. But instead of underscore, we would have colon. And in addition, we would at the top of the file have a mapping which prefix maps to which URL. And that's basically it. Right, yeah, so we'd have some like mappings at the top that has—I see your link there.

Aaron, I'll pull that up in just a second. Actually, I guess it would be a dictionary. And then you'd have things like this that map to the full URL. And then the goal of this, if I'm understanding it, is that you can construct fully qualified URIs for any of the properties that fall underneath that schema.

Yeah, you would even leave out the add sign and the mappings. Just, yeah, yeah, got you. And then in a property key, you use ocwg colon arrow. And that implies your name, URI, HTTPS, canvasprotocol.org/arrow. Got you, so in a single node. And the beauty of this is while we are still small and there are a few properties, you can practically safely ignore the mappings.

Just use the property keys as they are. Don't care that they contain a colon, and it still works. Right, the colons will differentiate them enough that you won't matter what the mappings are. We won't have collisions early on, is what you're saying. Yeah.

Gotcha. And then we had the idea that there would be multiple property bags. Which then we wouldn't really need. We could just use the same as the cronos group and pull the properties up to a top level. All the way up to the top level; you don't even have a property bag? Yeah. Interesting. I guess it's an unnecessary distinction.

I mean, extension authors still can establish their own property bag if they have to, but we don't have to. Yeah, no add here either. Just post it up, you error. And then that would be a dictionary that is—and the shape of that is defined as— The shape of the property value is up to—what are the specs? [INAUDIBLE].

Yeah, to the schema, exactly. OK. What about inlining the JSON schema? Yeah. This would be almost like a case of a cached web resource, wouldn't it? Having it be—I think that the advantage there is that it's potentially—it's self-contained of the file has everything in it. You don't need internet access in order to load it.

But you don't need a schema in order to load the JSON. True. That is true. Well, is that true? Because what I've been thinking—I haven't written an implementation yet, but I'm planning on writing one soon. The—in the case of you are a renderer, or you are an implementing canvas, you're going to need to create some memory, effectively, to store all the properties in.

And my thinking is that I would create those objects in memory based on the JSON schema, that I would instantiate those objects using JSON schema, and then populate them. Because this is the whole, like, you must now must preserve the property bags, even if you don't support those features thing. But I need no schema in order to do that.

I just read a property with an unknown key, and then I store it. I don't need the schema to tell me how much I don't understood. I just don't understand it. I mean, there's a certain case to have a way to inline the stuff. A canvas might contain remote web resources, so while I'm on a train, I cannot access the remote web resources.

But if my render does understand the schema, then the implementer of the renderer had access to the schema implemented it, and then knows the schema by the schema URL. And if I now read the correct prefix and the mapping, I know exactly which schema is meant, and I can use it, even offline. So really, putting the schema into the file is not really necessary.

It might still be nice, for example, use cases, which are important. So it does make sense to support it. But at runtime, it's not really— There's no advantages there, yeah. Not required, I think. On the giddo side when we import a GLTF, we have C++ classes to represent each component of that GLTF, and we just copy the data over.

And any data that we don't recognize is discarded. So anything has to be explicitly supported. And in the context of just preserving the data in general, it tends to keep that data around. But in most cases, you're going to want to do stuff with the data anyway. So if you have a position number, you want to actually use it as the position and not just read it into a dictionary in memory.

Got you. So I guess the use case we were thinking of Aaron that we talked a lot about early in the first couple of meetings was basically being able to round-trip between two different infinite

canvases that have very different capabilities. So an example might be that you're doing something like a flow diagram in React Flow or something along those lines, and you want to annotate that in TL Draw. And you open that React Flow infinite canvas in TL Draw, you add a bunch of stuff on top of it, almost like another layer.

It's not actually another layer, and then you might make some changes to the underlying stuff as well. And then you export that and bring it back into React Flow. Then React Flow would need to preserve the TL Draw stuff so that you could get that export back into TL Draw, and it doesn't just drop it on the ground.

That was kind of the—and then the intention there, the design intention, was to eventually be able to support multiple canvases live-interoperating with each other, which might be a bridge too far, but seemed really compelling. If you could kind of be working in React Flow and working in TL Draw on the same canvas, if you have this ability to preserve properties that you don't understand, then you can support that use case.

I like that use case. I think doing that is definitely a bigger scope than what GLTF does. But I think that's a good goal, a good use case, and that you should totally go for that, yeah. Cool. That's good to hear the encouragement from somebody who's working on the ground with a real format.

But yeah, I think I mentioned this in the section here where I'm talking about extensibility. It's like extensibility through preserving the property bag. It definitely has this big call-out of note. This is the most onerous part of supporting open canvas. They have to store the data that they don't need or recognize and have to be committed to storing it and then exporting it.

And so a lot of our thinking around how to do this sort of extensibility framework is around—we need to make sure that people know the shape of the data so that they could store it accurately. That was my question when I was asking Max if it was important to have access to the JSON schema.

And I think I've convinced myself in my mind that it is not important to have access to it in order to preserve it, even if I don't understand it. I think the data will quickly be so complex that you just need to store JSON in memory and round-trip JSON. And if you can do that, you don't need any schema information.

But your story, you've just highlighted about the two tools talking together. Maybe is a use case for putting the schema in the file. Let's say I'm a tool vendor, tool author, and I'm not able to host my schema files just yet. I don't own a domain, but I've written a little nice script and it extends it in a nice way and adds some little data.

So if I now would be able to write the schema into the file, you would be able to get it and we wouldn't even need a server to have the schema at—because that's some ceremony to set up the server hosting a schema, keep it up to date. And in hacky scenarios, just being able to transmit it in the file is actually quite nice.

So that's the second motivation why—maybe this mapping here is a URI, which can again be a couple of different things. Well, basically, you would need a schema array at the bottom, which states this URI actually is not only online, but it's also here. Yeah, that's what I had this.

So I guess some of the things we've just been discussing has been—I didn't connect the two until now, formally, but this mappings thing we were discussing, or the JSON LD sort of set of headers. And the schemas are sort of all one thing. There you have IDs, which are URLs. Usually, you use URLs that quite resolve, but don't have to.

The most important thing about URLs is that they are unique. And if I use my domain name as the base for URL, it won't accidentally mix up with your IDs, because you put them in your URL, and that's fine. And if we're cool, we serve a schema at the URL. But if that comes later, then for now, we just put the schema in the file.

Yeah, I think schemas in the files makes sense for now, as a pragmatic get it out the door 1.0 kind of thing, with the flexibility to extend to using URLs there. OK, cool. We are 12 minutes over, but this has been super helpful for me. I'm going to go ahead and wrap the meeting up now, unless anybody had any last-minute comments they would like to be in the recording.

All right. Cool. And I'll also add that schemas are—in practice. What I used them for is validation. So just checking if a file is correct by comparing it against a schema. And that's kind of what I was hoping—that's kind of what I was thinking as well, is as you bring the file in, you need the schemas in order to validate the file.

But to Max's point of, if I don't even understand the schema itself or the data itself, then validating it really isn't that important. And what am I going to do? Show the user an error that the file is misformatted when my particular piece of software doesn't even support the features that are represented in the poorly formatted JSON schema. So, yeah, it's an interesting use case.

Cool. OK. Let me stop the share. There's a few things that we didn't get through in terms of this PR, but it's getting close to the point where I'll merge it back in and we'll just be working off of main. Max, if you get around to writing a discussion about JSON LD and capturing your raw comments, that's great.

Otherwise, my thinking right now is I'm probably not going to pursue it further unless you kind of push on it again. Does that seem like a reasonable conclusion? Yes. OK, good. Yeah, thanks for digging into that. I definitely appreciate it. 

Yeah. And we'll have another meeting in two weeks. Michael will take care of getting this stuff up online. And we'll see you guys soon. Yeah. See you soon. Thanks, everybody. Bye. Thanks.