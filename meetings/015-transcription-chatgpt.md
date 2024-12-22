All right, here’s the transcript with paragraph breaks added for clarity:

---

All right, here we go recording OCWG meeting number 15 and yeah just the recap of what we've been talking about so far. Max has been working on getting the spec 0.2 merged into the main branch, which will basically be this point. I think spec 0.2 would be a spec that could be implemented. Like, we should try to implement it at this point. 

Not that I mean, Michael, you've done some implementation with the older spec, but as more of a proof of concept, I think we're ready to actually give this thing a try. So yeah, for sure. Michael has some comments on Max's PR, which we're gonna go through real quick. So go to Max.

---

All right, excellent. So we have first—you know, let's start with the same point. Rotation—sort of the rotational center of the note—should logically be the same as the point that is used for positioning. Which in the spec we said is, I think, top left because that's apparently the standard in this tool space. 

So if top left is the point you position, then probably that should also be the point you rotate around. Rotation—and I'll just add—change that in the spec. I took a note then about the styling. I added some weird CSS, and I'll just remove it. No problem.

---

Then about the resources, and last time we already had some discussion about things with an ID. So if we address stuff by ID, why don't we put it in a map? And this is, yeah, this is an aesthetic problem, not so much a technical one. 

So I found an argument why putting it in a list might be better. If we have two files and merge them or we have one file that we manually mess up and accidentally introduced the same ID twice and we parse that file, the usual parsing technically will be a JSON parser parsing it into run and then some other code looking on the JSON and trying to create useful in-memory data structures and actually throw validation errors. Like here, you have a note with the same ID twice, and that's not allowed in the sort of fix that blah blah.

---

But if we use a map, then the first JSON parser will say this is illegal JSON—you have the same object key twice. End of story. And then there is no useful validation message because it's already technically structurally broken. 

And so, due to the reality of how this parsing works, using arrays with an ID field will result in better validation error messages. It's not a strong argument, but it's one I—yeah, sounds good. 

---

In the simplest case, you can just—a very simple logic here when combining two files is just concatenate all the arrays. Yeah, and you know, don't do validation or, you know, like that. You could, you could cross your fingers, you know. 

---

Yeah, exactly. It's probably gonna be invalid, and you want to run to a validator, but you could at least—there's a simple algorithm for that. It will guarantee no conflicts of just concatenating the arrays. But the spec has covered your back because we say the IDs should be unique, and if they are not unique, we take the first one. And so, we are not dying, at least. We suggest that implement our syrup up die, yes, but they should just render something weird and show an error message.

---

So it's more like, yeah, it feels like the HTML approach of, like, the way browsers go to great lengths to render broken HTML. Yeah, even though we all know it shouldn't be formatted this way or that way or the other. Yeah, well, we'll make it work.

---

For the notes we discussed earlier, some meters ago, the order of the list is also the order of how it's rendered, at least the fallback set order. Yeah, although you can also use this `z-index` for that, I think.

---

Yeah, and it's also—and actually you can do the same with it. If it would have been a map with—yeah, just the same as if it was a map, you can also use that same order. But this is even more tricky because it's now a JavaScript standard that maps have an order, but I think it's not a JSON standard that JSON maps have an order.

---

So if a JSON map is by default an unordered bag, then the JSON parser might show it in any order. Like, if you use, for example, a Java map—the hash map behind the scenes—and the order is actually not defined.

---

Yeah, I would not depend on ordering here. Like, I didn't even know that the new JavaScript standard is that maps are ordered. That sounds fairly recent.

---

There's at least somewhere in the spec a way to retrieve the keys in some defined order. Maybe that's not even the standard, but it's possible now, really. If I'm not mistaken, even in a standard JavaScript object that you can pass through to all the properties that are in the object in the order they are stored.

---

Yeah, I think now it's—I'm not sure if all iteration options have the standard order defined, but there is at least one way to be ensured by the JavaScript ECMAS standard that this is now in the correct order. Maybe all of them, I just don't know. 

---

Anyway, in JSON, I think it's less defined. And so, we should certainly not depend on JSON key order. And yeah, I would suggest keeping it being lists for pragmatic hackability reasons.

---

Yeah, that's good. Great. Okay, and good document. We should probably document our reasoning there because this is a great candidate for the design decisions document, isn't it?

---

Okay, it can be nice and short, written as an ADR for that. So now, while I wrote down the spec, I stumbled upon some issues that we hadn't thought through.

---

Right, so maybe we can sort of together look at the stack and see what came out of it. Looking for the screen share option. I think I'm not—oh yeah, not allowed by default.

---

Yeah, I gotta enable it. Oh, I have it—that's a great new green share button. Just found it. So this is—okay, now I don't get zoom. It's weird why I got it again. Why do I get this very, very small just because I'm screen sharing? I have multiple monitors.

---

Okay, yeah, so here you see a very nice CSS hack. Yeah, but it could look nice. I know—that orange bar was also in the front of the whole document. Yeah, I would certainly not—not the intention.

---

Okay, so what do we have? This is all non-controversial. Yeah, these issues should—notes adjacent in area map. This is what we just decided. These should all be arrays, and we can also say why this is all non-controversial. This is fine, no issues.

---

Okay, so we have notes, and they have these default properties. Then we have the first extension. So the ports, as an example, I turned into a node extension, which is, I think, what we discussed a while ago. 

---

So this is how that looks in JSON. So you—in the note—you have the data array. That's where we put all the extensions formerly known as properties. Then we add the type, and this extension has a ports array as defined here in the ports extension.

---

Every extension is described by a name, which is just a convention. I mean, every locale could use its own name, but the URI is the mandatory name. Then it describes the properties it uses in its extension.

---

Here we see an example of the extension being used. This is simple and understandable, and every extension author should sort of produce this snippet to explain what's actually happening in the extension.

---

Then, as another example, I also wrote down the relative constraints extension. This is now just, yeah, a suggestion from my side. We never discussed it so far, but as an example, you could say you have a port that is somehow placed relative—a node placed relative to another node. 

---

So you say the source node to which I refer, and then I have a local position and rotation. But actually, my numbers are added as a delta to the position of the other node, and that's it. So for position and rotation, I am just describing how rotation works.

---

Okay, yeah, I like this. That's where you'd want to use relative constraints. Does that mean that you would not specify the position? Is position required at the top level already?

---

Yes, of course, but if your app understands this extension, it knows that this other node is always placed 0.5 next to the A node. So if the A node is going to be moved and the other app does understand, it could, like, move the B node next to the A node because that's what the relative constraints extension wants to express.

---

That's interesting. I would have expected that to be expressed with, like, a set or a group—like a group relation. Yeah, that would also be possible. And there are always two ways to express it, right? Like, you know, they don't all have to be the same.

---

No, and we should reconsider this, and maybe your idea is good, and we should actually change it. But let's leave it for a moment because relations—which we come to next—are slightly harder to understand.

---

Okay, all right. So we have a relation, and relations are really simple because a relation has these basic properties only: some kind of ID, just like nodes have. They have a type, which is actually a schema name or schema URI. And we have the data array because a relation can have extensions on its own, like visual nodes can also have extensions.

---

So if we have a set relation, we have a type. A set relation has the `member` property, which is of type ID array. So this is how you use a member relation, which is very nice and clean. 

---

Then you can have an edge relation, which is `from`, `to`, and I also gave it a Boolean, `directed` or not. And you can have a rel type. This is to model the RDF relation type. So it goes from this subject to this object, and that's the property of the triple. You can optionally put it right there in the edge if you need it.

---

You can also write a relation as "work add" and just use a string that depends on your app and use case. So this is still gentle. Then you can have hyper-edges, and then I went a little bit over the top and just modeled every possible hyper-edge you can have because I know exactly what to put there.

---

So the hyper-edge also has a relation type, just like a normal edge, but it has more endpoints. The endpoints here actually are an array. You can have a number of endpoints in your hyper-edge. Each endpoint is its own object and has its own target ID to which it links, like an edge has a `from` and a `to`. But this hyper-edge has many more endpoints—not just `from` and `to`, but maybe 17 endpoints or three endpoints. We don't know.

---

Each endpoint has a direction. So some edges are a little bit like a block between the nodes, and some nodes flow into the edge, some flow out of the edge, and some are undirected in relation to the edge. That allows you to model directed hyper-edges, undirected hyper-edges, and even all these mixed weird cases.

---

Okay, you can also have that. Then you have weights. You can have a weight for the whole edge, which is quite common. You can have a weight for each endpoint, which is rarely useful, but in some cases, you do edge bundling. Like you're modeling flows, and two and two flow together, and then the edge has a weight of four, and then it splits into four, and each of them has a weight of one. 

---

If you render that aesthetically, it looks really good if you know exactly how much flow you have at which endpoint. So the weights could be helpful. This is, like, we probably won't need more edge types given edge and hyper-edge. So this is nice, and it's still almost compact.

---

Yeah, so then we have the group relation we discussed. So a group is like a set and has members. It has a bit more semantics. It defines, for example, that we explicitly say groups can contain other groups. When a group is deleted, all members are deleted. When a group is ungrouped, the group is deleted, but the members remain.

---

And I think this is a section of the spec that has to grow in length and precision for the other parts too, because this is really the meat. I mean, when should I use a group in my app? I'm doing this, and is this a better group by OCWG or not? And then you have to look up the semantics, and then you understand, yeah, that's exactly how it should behave in other apps.

---

I'm using a group. Maybe have a parent-child, which is, I think, what Jin said. We need it for inheritance. So we have a parent and a child link, and we can say inheritance is true or false. It's like semantics of inheritance are defined by the application. 

---

This is a bit vague at the moment, but we can tighten it if we learn more about what to put there. Maybe remind me—what was Jin's use case for inheritance? He had a good example from a 3D model, like for transforms. You say you have some nodes, you group them, and then at the top, you add some group node. Then you say you have a rotation, and all the other nodes underneath should inherit that rotation angle. You only define it once, and they all rotate.


---

Which is different. Each member rotates then, not the whole group as a whole. So it—right. Or you define a background at the top, and all the members should get that background in its content. So it's property inheritance, a bit like in CSS.

---

Yeah, and you're defining a rule that you can then inherit around the different places. Yeah, interesting. Because those are typically what we would think of as node properties—data on the node—and we're using a relation to express that inheritance, an inheritance of node properties. I don't know. That feels—

---

Yeah, this—yeah. So you have a template node, and the other ones apply the template. So I think that's a good candidate for a relation, actually. 

---

Then we have—actually, I'm not even sure this is the most recent version, does it? Yeah, I remember. So there we have assets. These are, I think, less problematic. We know with resources and schemas, and they are similar but different. 

---

For assets, we have—for resources, we can put them in an external and remote. We define location, mime type, and content. This was—oh, easy. With data URIs, because if you have a data URI, they implicitly already define the mime type and the content. 

---

So yeah. So if the user also stated mime type, that should be ignored because it's already defined in the URI, and actually redefining it overwrites here—it doesn’t make much sense. Then we have the fallbacks defined. 

---

Can you go back to that example real quick? Do remote—in order for a remote data URI to be valid, does it have to have a mime type? Data URIs always have a mime type. Yeah, otherwise, they're not data URIs. Okay, gotcha. Yeah, cool. 

---

So in that case, if you were to specify the mime type—oh, I see. You're saying in this case, it's binary, and inline content is that as the remote did. Okay, got it. I understand now. Okay, cool.

---

Yeah, then schema. Yeah, we probably need some kind of tooling for validation, but this is not really an issue in the spec per se, but rather—yeah, I mean, that’s reasonable. Like you're saying, okay, so a schema is defined as that table right underneath that.

---

Each entry is an object with the following properties: a URI, a schema object (JSON schema inline as a JSON object). Got it. And then the location and the name. Yeah, and then it depends a bit on what you define, what's required. 

---

So you can have an inline schema. Then you always need a URI. And if you have an inline schema, you need to actually state the schema; otherwise, we don't know what the schema is.

---

If you have an external schema, which is rather like a local file, then you need to give that path so that we can find it. And if you use a remote schema, and the URI actually does resolve to the schema, we can find it there. That's cool. 

---

And in any case, you can give the schema a name if you want. And if you gave it a name, then in the other parts, you can refer to it by name and don't have to state the URI. So this is just nicer and shorter than the long form. Got it, got it. 

---

And the name—the name is the key to the map right here and your URI. Yep, yep, exactly. Yep. Which actually makes it quite funny because how can a name be optional and not there? So that doesn’t work. 

---

I was just gonna say, like—and how do you specify it? Yeah, okay. So now we have two options. Required then, or we turn it into an array, which we’re using elsewhere.

---

We would end up with the concatenation problem again here, right? Well, the schema array is super short. Yeah, I mean, it’s the same problem you mentioned. I mean, it has that kind of consistency to use just arrays everywhere. 

---

Yeah, so it’s—I kind of feel like consistency wins out here a little bit over the readability. All right, so I took a note to change it to arrays, and that also makes the name truly optional. Like, you can, if you want to, leave the names out. You can spell out the full URIs of each one of them. 

---

Actually, you don’t even need that entry if you just use the URIs to document. If you use the URIs to—what? If you—yeah, if you use URIs to reference an extension and not the name, then why do you need an entry here? 

---

If you have a resolvable URI—yeah, you can define it here, but you don’t have to. You can just leave it out. Right, use the URI. Did you mention that up above, that that's like a shorthand? You don’t need a schema entry if you would like to use a fully qualified URI for a non-inline, for an external remote schema? 

---

Not clear enough yet. Seems like a reasonable thing. I think our preference, though, is that these schemas would be self-contained, right? That’s kind of one of the sort of local-first values, or at least my preference. 

---

It would be that you would actually include the schema in the file itself. It has pros and cons. So that would say that every exported OK file everywhere contains all schemas—which is just the schema so much—I mean, just the schemas it needs for that file. 

---

Just the schemas, nodes, and relations that are defined in it. If I put the value—I mean, the value is you can open it while offline. You don’t need a schema to open a file.

---

True. The schemas are just adding extra validation. Actually, the URI is the key, and you either understand the URI and know how to handle it, or you don't. 

---

But I'm imagining myself as an infinite canvas tools author, and my thinking is that I would load the schemas and load the JSON schemas in order to dynamically build objects that I could then load. So I would want to do that validation myself as I'm loading in the OCWG file or the ocif file.

---

But for reading JSON, you wouldn't need the schemas. No, I understand. The schemas are just constraining the space of legal JSON structures. Yeah, and that's what I was saying. As an author, I would want to—ideally, I would say, give me the JSON schemas so that I can put these objects together, and then as I'm loading the file, I can catch any validation errors as I'm loading it.

---

But if you don't understand that part of the JSON tree—let's say that's the ports extension—and you don't know what the ports extension is, you don't gain anything by saying some of the ports arrays are valid, some are not. But I don't know what ports arrays do at all, so—

---

What? You have a really important point. I think there should be a description field for extensions. Bear with me, right? Yeah, something like that. Like free text where you can say what the extension does for a couple of reasons. 

---

One, for human authors of, like, "How does this extension relate to the canvas at all?" And that could be so—you could describe how you expect this extension to be used. But the other reason I'm thinking is for, like, LLMs that would consume this file format. They could actually learn about each one of the extensions by reading the description.

---

Yeah, maybe. So let's park that one too. We are almost done, and then we need to talk more about extensions. So we have—we could add some built-in schema mappings to say these are always just built-in. And yeah, here we come to one interesting point.

---

So we have node extensions. Nice. We have relation types. Nice. They have schemas. And then we have, of course, relation type extensions. So these are—let's say I have a set, and now I have an extension to the set relation type. 

---

Then we have the set. Of course, it has a version. All our schemas have a version. So we have a set version 2 with an extension version 5, maybe. And version 5 of that extension applies, of course, only to the set extension version 2. 

---

And then if a set extension version 3 appears, then the extension also has to—this set relation type needs to reconsider whether the extensions still apply and port them, and so on.

---

What if we flattened it here and said that extensions don't apply to relation types—they apply to, like, every relation type is an extension of the base relation, just like every node extension is an extension of the base node type?

---

That way, all the ones you defined aren't relation types; they're just extensions. Then a relation type can at the same time be a set, an edge, a hyper-edge approach, I believe. Yeah, and that is really tough to interpret. This is true. 

---

But I mean, I could make the same argument for a node that at the same time can be a rectangle, an arrow, a circle. Like, you could just stack extensions on top of a node and make just as much gobbledygook of your file as you could with a relation.

---

Yeah, that's true. And flattening it and turning every relation into an extension of a base relation just simplifies that base. I like that. Cool.

---

Yeah, and it makes it nice and parallel. It makes relations even more parallel with nodes. Exactly. And this is one thing that really—I didn't like how it turned out, but I'm glad. I mean, I think you put your finger on the problem. Now this is just a possible solution.

---

You're right. It is awkward, that possible solution. I'm trying to think if it boxes us out of anything in particular. I don't think so. But I think what you were trying to capture was also valuable, which was there are these relation types that are kind of default or included. It's like the default set of extensions, and these are the ones defined in the spec.

---

So they don't feel like extensions—they feel like first-class extensions or first-party extensions. You know what I mean? And I feel like we have the same thing that we haven't really done yet with the nodes, where we're like, "These are gonna be the ones that OCWG is gonna kind of ship with," but we're still treating them as extensions no differently than the rest of them.

---

Yeah, yeah. If we—thank you. I appreciate what you've done of going further to spell all of them out, because we need to do that on the node side and haven't yet. 

---

So if we say we have a set extension and that's it, then it's not possible to attach custom data to sets. We say we have—in order to do that, you need to define your own set. And there's no hint that your set has anything to do with my set.

---

Ah, no. It's still in the same relation. It just has two extensions: the set extension and the other one. That's actually fine. That works. That's like multiple inheritance. 

---

Yeah, it's like we talked about with arrows. We talked about this with arrows too. There's gonna be a zero and a teal draw arrow. I like that.

---

Technically, one other thing was slightly interesting. If we have a relation—let's go back to an example where we use a relation extension. For example, here—

---

For example, here we have a normal JSON object. It has a `type` key and a value for that key. It has a `type` and `endpoint` key and a value for that key. And you can put any keys you like. But the `type` key—it belongs to us. That’s the magic key.

---

And for a magic key, it has a surprisingly common name. So if you want to call anything a type, don’t call it `_type` or call it—I don’t know—find another word. `Type` belongs to the reserved type.

---

Yeah, but is it still a reserved word now? Like, I thought—yeah, yeah, of course. All our extensions are of this same shape. They have a `type`, and then they have other properties. That’s how we put them.

---

Yeah. So can you show me a node extension as well, just to jog my memory? Yeah, I guess I could look at the file on my side too, actually.

---

So here we have a node with an extension. It has the ports extension active on it. And of course, it has a `data` array. And in the array, you have the extension objects. And each of them has the magic `type`.

---

Yep, and that’s just a reserved keyword. And yeah, I don’t know what you’re saying. The `type` might be too simple of a name for such a magic word. Maybe we could also call it `OCWGType` or `ocifType`.

---

Or `extType`. Or `extType`, yeah, because that’s what it is. It’s the type of the extension. So it could be like that. It’s already a nice improvement: `extType`.

---

I could—do you have an opinion on this aesthetic idea? I like `type` the most, actually. Yeah. Because it’s—it’s nice and simple. One word. I’m ambivalent either way. The `extType` or `type` feel good to me.

---

`extType` only adds three characters. But we can stick with `type` for the time being and see what others say. We’re just three now, so I just want to bring up that this is the only magic key in that set, and it’s the only kind of conflict where we do have that.

---

Mm-hmm. And nodes themselves need a `type`, no? We just discussed how we unify nodes and relations. So nodes have no `type`, but they have extensions with a `type`. And relations will also lose their `type` and just have extensions with a `type`.

---

And that way—yeah. Yeah, relations can have multiple types if they need to, right? So `type` is not—right. But something is a node because it is in the node array. It’s implied. It’s a relation because it is in the relation array. Therefore, we don’t need to add a `type` field to it.

---

Yeah, just nice. That’s good. I like it. We have not defined what a relation without a `type` actually is. I was gonna bring that up. You know, it’s—it’s just there and empty, like a—I don’t know, why not? You can have it. It’s like a reserved ID. 

---

Yeah, yep. We have the base node type, which does have stuff on it. I mean, it’s gonna have an ID, and it’s gonna have a `data`. And that’s it.

---

Yeah, and `data` is optional already. So right. It is optional, but it will have an ID. `Type` will be removed and delegated into `data`. And then it’s just—it’s just an ID. It’s fine.

---

Yeah, yeah, yeah. It’s—we simplify. I like it. Yeah. Then we just have, like, a concluding list of the sort of types we use internally, which are more precise than the JSON type. 

---

So we have angles for rotation. What do we mean by an angle? Are they in radians or in degrees? So that’s defined. What’s an ID in our spec? What other IDs does it need to be unique? What is a mime type? 

---

And I looked it up—actually, it has to be called `mimeType`, not `contentType`. `ContentType` is just in HTTP, but `mimeType` is the generic. Yeah, then maybe do an IANA registration one day.

---

Okay. Yeah, so the list of open issues is really quite short. So this is how this schema built-in stuff would look like right now. Mm-hmm. And this will be reformed to an array. 

---

And as an example, we have the extension—yeah. Now it’s, I think, a good time to talk more about extensions. So right now, we only talk about the schema of an extension.

---

And here in the spec, we already say a good extension is described by its URI, by a short name, by a table describing the properties, by explaining the semantics of the properties, like maybe giving examples. And none of this can be found in the schema.

---

So we have no agreed-upon way of how schemas are published or documented—how extensions are documented. So we could have, like, a convention. You should have a document that has this structure, these points. It should be named this way. It should be put there in your GitHub repo, and that’s the usual way to find the documentation for the extension.

---

That would be nice. And then we should follow that guide ourselves and maybe remove our relation types from this spec and put them in the extension folders.

---

Makes sense. Yeah, I’m happy to help. I’m happy to help write node extensions as well. This is something I thought a fair amount about when Orion and I started working on the spec—like, what are the base nodes that are being used across canvases?

---

---

Once we have a format, I can start—I can knock out a few of those. Yeah, there's sort of the first proposal for most. Well, great. So I think what we’re saying is that there’s, like, a GitHub repo or a file—a folder. 

---

Yeah, you’d probably need a folder and two files: the JSON schema and the documentation file. Yep, exactly. I was gonna say the same. Probably a `readme.md` file is our recommendation, but it could be something else if you want. 

---

The nice thing about `readme.md` is that it reads well in GitHub if you’re browsing. Yeah, yeah. So we should use it to our advantage. Yep. So I think it’s a `readme.md`. It looks like it has what you’ve got right here of an H1—you know, the name of the extension, some common name of the extension. 

---

And then, yeah, schema: the name, the property, the schema links to the schema file itself, which is a JSON schema—valid JSON schema schema file. Then a table that, like, you know, shows the properties. 

---

This goes back to my thing about a description field. Yeah, so this would be much more powerful than a mere description field in the file. So I agree it’s more powerful—it’s not as easily queryable. Whereas if it’s a description key, when you pull down the JSON schema, you get that description field along with it.

---

I’m not saying that’s better. I’m just saying that it comes along with the schema itself. I do think it’s better for machines like LLMs. You can hand them the schema, and you don’t have to hand them a separate `readme.md`. 

---

Yeah, but honestly, for LLMs, breaking up the spec into multiple files would be a bad idea. For a machine, having it all in one document would be much easier to handle.

---

I think we should probably have some tooling that does that, basically—that, like, this is why I was saying I like those inline schemas personally. I think it makes—I want a tool that flattens it all into an inline schema so that I have it all in one place in a single file.

---

There’s a TL Draw example of this, I believe, where they have a JSON version—a `.json` version that just has the data structure. And then they have a `.tl` draw file. I’m going to go check my exacts here. But they have two different files: one of them just has the data, and one of them has the data plus the schemas fully fleshed out.

---

And then the advantage of the data plus the schemas is you can have the exact version of the schemas in that file that were used at that time or used to create that data. And you can kind of package it all up as a single file that can be opened offline by the TL Draw JavaScript viewer without having to connect to any schema servers or anything.

---

If those schema servers aren’t available, or the schema versions aren’t available, it doesn’t matter—it’s all in one self-contained file. And I’ve made the mistake before of getting the JSON file of a TL Draw and not having the `.tl` draw file. So I didn’t have—and I wasn’t able to do a few things that I needed to do.

---

And it was actually around validation. I had a weird validation problem with my JSON file, but I didn’t have the schemas available in order to do the validation. So I had to go back through their repo and manually pull them down. It was kind of a—anyway, long story.

---

But this is why I think having schemas hydrated in a file can be really useful. So what—would we then have two flavors of ocif? The ocif pure and the ocif hacker version of a file?

---

Okay, what’s the difference between the two? Pure is just the data, and schemas are just linked. And hacker is the hacker-friendly version where the schemas are all inlined.

---

I think both of them are valid ocif files the way you’ve defined it, right? One of them has external URIs for the schemas. I mean, but should we—like, if we write a spec, we should tell the application author what they should put in. Is it common practice to always put everything in? Or should you offer two export options, or what? 

---

Yeah, it should be done. I mean, it’s onto us, right? The way—if I were writing that section—and this is just me—I would write that section to say, "Our recommendation is that you bundle the schemas with the file for the sake of having a complete file that can be opened offline and allow maximum flexibility for infinite canvas authors to do that full validation without having to hit a remote URI."

---

All that—that’s the recommendation. But if you want to save space, like if you want a smaller file format, you can omit the schemas and pull them down from an external URI or package them up as, you know, an inline or a file alongside that. 

---

They can—you know, like a local URI if you wish. And that could be the ocif bundle I was just referring to, like the TL Draw bundle. Because you could actually have the data and the schemas separately, you know, and resources. 

---

You can—there could be some kind of ocif bundle. But yeah, that’s the way I would write that section. The recommendation is all in one place.

---

---

Okay, that’s fine. And I think we can offer a command-line utility that takes an ocif file in any format and then hydrates it. You could do the same thing with external resources as well, by the way. 

---

Yeah, like turn them all into local data URLs. So, you know, it might be a five or ten megabyte ocif file because it’s got all the local resources in it, but hey, it’s got all of them, right? That’s—

---

For the spec, if we put the description of the extensions in separate files, then the spec itself would be harder to read and less ready for LLMs because handling multiple files is not so nice for LLMs. So there we would also need some kind of bundler to create the long version.

---

We could do a very simple version of that, which is basically just concatenating markdown files. So, we could specify our bundler could basically be, "Here’s the full spec in the node section, an array of OCWG node types that we say are kind of the default." And we just literally iterate over those, grabbing their `readme.md`s, and then—

---

So we could make—I mean, I think I could write that bundler for us if we follow this `readme.md` format, right? Where the readme can be just literally embedded—like concatenated inside the file. But this is how the `readme.md` should be formatted so that this concatenation actually does work.

---

I mean, but that will be—but okay, you also need some heading adjustments, and headline one becomes headline two—something like that. Yep, that is true. I was thinking the same thing. It does work in AsciiDoc.

---

I think you’re going to have a hard time selling that one, Max. I know you like AsciiDoc, but—

---

I think, for pragmatic reasons, it would make sense to leave the built-in extensions just in the main spec and maybe as an example say, "Oh, that would look like `readme.md`." Yeah, I think that’s pragmatically—I think that’s entirely reasonable to make it one easily readable doc.

---

We can even link to the—we can have a link inside that from the main spec to each child node extension and relation extension that links to that folder where the readme is, and that kind of thing. Yeah.

---

But it’s super cumbersome to maintain. So, for the built-in things, we would, in the readme, say, "Actually, this particular built-in extension isn’t documented here. See the main spec." That would be very pragmatic, and then we have one example extension where we say, "Here you actually see as a template how that should look like." Okay.

---

And that’s it. It minimizes maintenance. I like it. Sounds good. So then, as we iterate on the versions of the—not the high-level version of the OCWG spec, but as we iterate on the versions of the extensions, we will have to make sure to update the main spec.

---

Yeah, either way. So we need to decide hard which are really built-in types and extensions and which are not. Yeah, I think that’s a great topic for the next meeting. Like, let’s go through our list of—I think you’ve already done it basically for relations. Now we need to do it for nodes.

---

Yeah, and maybe—maybe your last thing is—yeah, what do you think now about the relative constraints? I mean, obviously—yeah, it could be a relation. It could also be a node extension. It’s very—I don’t know. It’s not very structural or semantics.

---

It’s addressing the visual properties, like position and rotation of one node, relating these visual properties to the other node. So I don’t know. It felt closer to the visual domain. So, it’s a visual node extension, but I think it’s also a node extension. I’m not—

---

Yeah, I think it could be implemented either way. You could implement it either way as a group extension where the group or set has, like, a relative property on it. So you could call it a relative set or something along those lines.

---

Now, that would make it more powerful, maybe. That feels—so, the difference, I guess, is that—yeah, that would make it more powerful because then you could have—wait, because this extension doesn’t have an array of nodes.

---

You put it on one node and say, "This node is actually positioned relative to another node, and my relative delta is the position of that node plus this, and the rotation plus that."

---

Okay, so I would define—I think it’s better as a relative set because in the relative set you can basically specify an array of all of the nodes that are relative to the source node.

---

But you need not only to state the IDs of the relative nodes—you also need to say what’s the offset. So you need an array of the same length for all the offsets.

---

Oh, yeah, you’re right. Okay, then you make sure that the arrays have the same length. And yeah, that is—that is kind of dirty. Yeah, no, I think you’re right. So it is a node extension. 

---

At least for now. Yep, for now. No, I think you’re right. And what—what made—are you proposing it as a built-in or a default one, whatever we’re going to call these official ones?

---

Yeah, but this was just to—I don’t know. We had some notes on that topic, so I wanted to put it somewhere. Great. Yeah, no, this will be a great start. And yeah, I like it. Michael, what do you think?

---

Well, this relative constraints extension—I can see that it can be really helpful for something like spring, like some kind of spring behavior that you want to build in or define. But those nodes are not in a group, but there is a constraint between them and how they move together. 

---

So I like this relative constraints extension, but it’s good that we have this in the spec besides the normal relations. 

---

Yeah, you kind of have to take a hard look at what we have defined and think what’s missing to define your tool in it. That’s exactly what I’m planning to do. I’m planning—I’m looking at TL Draw and Scalar Draw, like we’ve talked about, and going through it. 

---

The other one that’s very simple, because it’s just such a simple spec, is the Obsidian Canvas spec. Yeah, very—very—we cannot express that one. We did something wrong. 

---

Exactly. I think we can capture that one pretty quickly. So I’m curious to write an actual ocif file that captures everything from Obsidian Canvas, like an example. That’ll be fun. 

---

I will—yeah, I will broaden my implementation for my exporter. You’ll have the first tool that implements ocif 0.2. I hope so, if I can find the time. Sorry, 0.2, not 2.0. 0.2. 

---

All right, this is really good. One logistics before we jump off the call—I’ll go ahead and hit stop recording for now.

---
