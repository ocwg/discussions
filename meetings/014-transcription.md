### Transcript with Paragraph Breaks

Hello. Welcome to our 14th meetup for everybody who's watching this later. We are now going to work to some issues to see if you can resolve them.

All right. Thanks, Michael. So I have not committed anything or sharing is not turned on, I sent a request. Maybe you're allowed to.  
Yeah, you should be able to do it now.  
Okay. I'll try it again. Okay. Hello, Meg. Okay, there's no, okay, this one, okay, this looks good. I need to grant more privacy privilege to Zoom first. I might have to rejoin the Zoom call to be allowed to share it. Let me try.  
I'll be going to Mac, New Mac, yeah.  
Yeah.  
Yeah.  
Yeah. Zoom says that you are sharing, yeah, there it is.  
It looks good, right?  
Okay.  
I'll put you on the left side. Bigger screen.  

All right, so I tried to boil it down to a few files. In order to have a spec that's really precise, I moved some points to separate documents. So we have like a design decisions document, I think, which I presented last time already.  
Yeah.  
And I just look at slightly and I think we should keep it that way to keep the design decisions and discussions out of the main spec and maybe follow more rigorously the architecture decision record structure. I haven't done that yet. Then we also have a document listing the goals which we have, which we also stated already. And we have a sort of a requirements list which we can distill. All that is left out of the spec which is supposed to be very dry and concise.

So I tried to look into how W3C is writing all these specs. And there is something called markdown to spec. And you just write markdown. Then you can add additional metadata files for bikeshed for the nice file extensions BS. And then you can convert it into the respec format which is really an HTML file with a respec CSS and the respec JavaScript which then allows folding of the site or stuff like that.

So all in all, the first step of the way would be this document to just have a markdown document actually stating the actual contents of the spec. So this is something we can evolve into a very nice looking spec later on. Yeah, manually copied the structure of such a spec which is always listing which version I'm actually looking at. I decided that we are currently looking at version two and the start of a 0.2. And the stuff we have already in the existing full request I consider this to be 0.1 just to be able to distinguish the two things.  

So there’s a 0.2. And then these are the usual things to have a feedback editor. This is not the people doing the spec, just the guys actually typing the spec. So this currently is just me, but as this is just markdown, I think we can easily have more people writing on the actual spec.  

All right, so we have a very short abstract. The status of the document needs to be clarified that this is not official published in any way. Then we need some kind of license to let other people know what they can do with the license. For the moment I settled on the CC by SA. That means everybody can use this spec as they want if they give credit to the original authors. So aside the Open Canvas Working Group, if they change the spec, they must say how they changed it. This probably helps to avoid confusion. And they may use the spec commercially. Otherwise, it would be prohibitive for all these tool vendors. We can change this, but this here at the first glance seems to be the best-fitting license.  
Yeah, it sounds good to me.  

Oh yeah, we always need a current state and then we can change it. Then I have some conventions in the document. I found out that in the final spec we will not have to-do lists. And I drafted a CSS snippet so that this markdown with a to-do item in it looks really scary, like an issue so that it is easy to add issues to the document and not overlook them. So this is actually quite nice. You just have this to-do item, and it will render it as an issue.  

Then for the types, the JSON types which are defined are really brittle. I mean, they don’t say much about the actual contents, and we define our new types or reuse other types. So I think it’s wise to have a catalog of OCIF types.  

This directly brings us to the next question. What is this spec called? I think it’s the Open Canvas Interchange Format. There are the words exchange and interchange. And interchange is more between different applications. And exchange would be more over the network, but more between similar applications. So interchange seems to be more fitting. So then OCIF would be the acronym of the spec.  

Sounds good.  
Does that already exist, by the way? Check if OCIF already—  
Oh, well, that is something already.  
No, I didn’t.  
I don’t know.  
Well, there is the Orange Corners Innovation Fund.  
OK.  
But I think it’s OK, they are actually good.  
It can also be the Outbound Call Interface function.  

OK, then we have a table of contents. And here we go. And soon we will encounter our first issues.  

So, yeah, what is a canvas? There is no definition or whatsoever what a canvas actually is. So we live to infinite canvas.tools where like 100 tools are listed, and there is even one post I found about all the canvas, but even Wikipedia is not mentioning this concept we are using at all.  

So this could be maybe something we should add to Wikipedia actually.  
Yeah.  
I was just thinking that’s very good at it. Because ChatGPT now has this canvas option, which is not an infinite canvas. I don’t know why they choose that name, and maybe they have plans for it.  
Yeah.  
Oh, it’s good to have to write something on Wikipedia about it.  

From the game engine perspective, what comes to mind as close is that this is like the 2D equivalent or the text and relation equivalent of like a 3D model. So it’s just a file that contains this data that exists in two dimensions.  

And specifically with canvases, we have these relations and such. But we even opted for so it’s not strictly 2D.  
Yes, the Z and X is good for rendering.  
It’s still broadly two-dimensional though, even with the Z index because you have like, you can’t rotate into the third dimension, you know?  
It doesn’t have a size in the third dimension.  

Well, we discussed it. Maybe it has, maybe we should also remove it. But I remember in earlier discussions in the current stack, we actually have actually a real tool Z coordinate and Z dimension for the size is also legal currently.  
Oh, fascinating.  
Yeah.  
I’m not sure if that’s a good idea, but we’ll come to that.  

All I can say for sure is that such information would be discarded if I imported a canvas into a Godot engine.  
Yeah, that’s true.  
OK. That’s actually something I need to take a note. It should not be discarded, but also it cannot be not discarded, right?  
Yeah.  

**2D versus 3D.**  
We’ll come back to that.  

So in the spec, we mainly talk about nodes, relations, and assets, and schemas. Should we maybe consistently call them resources here too?  
Yeah.  
OK. Nodes, relations, resources, and schemas.  

And we have the overall file structure. The current spec says we have an attribute called `schema_version`, and I would propose to rename it just to `OCIF` and add the value list URI of the schema in use. This way, it’s shorter, and it’s sort of like a magic signature. If you have just a random JSON object somewhere and you find it has a root level attribute called `OCIF`, maybe what you’re looking at is some kind of open canvas file.  
I like that.  

In fact, it’s actually better than what GLTF does, because GLTF files just have `asset version 2`—it doesn’t even say inside of the JSON data that it is a GLTF. It just says that it’s version 2.  
OK.  

So, yeah, we have one vote for this.  
Yeah, I like it as well.  
This really gives us a separation also from other JSON formats.  
OK.  
So you have no confusion there.  
Right.  
So I counted three votes for this.  
OK. Excellent.  

**Minimal OCIF file.**  
The next question: nodes, relations, resources, and schemas—they are all arrays. Are they required or optional? As they can be empty anyway, why not have them optional?  
Yeah, I don’t think it should be required to specify them if they’re going to be empty.  
What about the nodes? Don’t you always have nodes?  
Not necessarily if you just have relations.  

For a point of comparison, you can have a GLTF without nodes. It’s valid.  
So I keep them optional, fine. We can always change it later, just to have a working consensus.  
So then the minimal OCIF file is really just this snippet.  
Yeah.  
Oh, that makes it quite easy.  
It’s very clear.  
It’s a plus, right?  

And then we have a minimal useful OCIF file, which has a node. It must have an ID, it has a position, and there it is.  

**Talking about nodes.**  
So nodes have an ID, which must be unique for all nodes, relations, and resources. I would say, yeah, then I have a position. And here we had either a 2D position or a 3D position. And we haven’t defined any defaults. We could also say that the Z-axis defaults to zero. We could also drop the 3D part to make it clear.  
Hi, Jess.  
Hi, guys.  
Yeah, well, I think this is fine to either X and Y or X, Y, and Z.  

And we have size, a position, I really have some questions about position. So it’s the position of the node of the canvas, but which part of the node is actually positioned? Is it like a center? Is it the bottom left, what? What is positioned?  
Most UI tools use the top-left corner, actually.  
OK.  
So I will restart with that as well.  

I think I’ll pull up the spreadsheet. I think we actually did an analysis of all the different whiteboard tools and what they regard as position. Let me see if I can find that spreadsheet that Orion put together for that.  
OK.  

We have a question about position: the coordinate system. Do we agree that the coordinate system is left-handed and the X-axis is going right, the Y-axis is going down, and the Z-axis is into the screen? This is what CSS uses.  
Sounds good to me.  
Yeah, so X goes to the right, Y goes down, and Z goes into the screen.  
Yeah.  
Yeah, I think that’s what most of the things use.  

The unit. The unit is pixels, but what is a pixel? Nowadays, we have sub-pixel rendering. It’s on logical pixels as CSS, right? And then whatever the device is actually doing to display a pixel, how many pixels is it used for that? We don’t care—it’s logical pixels.  
Yeah.  
OK.  

The position point is the top-left corner. Just looking at the big sheet, whether that’s unfortunate—the sheet doesn’t have that particular detail, but yeah, I think top-left is fine.  

What about the transform origin, as CSS has? Do you want something like that?  
Seems like Aaron had something to say about transform origins in GLTF.  
I’m trying to remember what that was.  
I think it’s in the GitHub discussion.  

We’ll come to that when we talk about rotation.  
Got it.  

**Position and size.**  
So this is all about position. That’s fine. And size is also per dimension. So it’s width, height, and depth—rather easy to understand.  

And rotation—we agreed to have it in degrees. Do we have it optional, and what actually is rotated? I mean, what is the point of rotation?  
It would be the same point as is the position.  
That’s what would make sense to me at least, and that’s how it works in all 3D tools and UX mentions.  
Yeah, I think, yeah, I think it’s OK.  



All right, defined. Then properties—I propose to rename properties to data. Shorter, easier to type, and makes clear that you cannot just have one level of properties but actual JSON trees behind it.  
Mm-hmm.  
Follow me?  
Yeah.  
Motion passed.  

OK, we have that position. Yeah, very strict. Next.  
Very strict. Are you working?  
Yeah, otherwise, I get completely lost.  

Position—we could have a default position and make position optional to allow other tools to import stuff more easily into an OCIF file. Just drop everything on the canvas, everything’s just on top of each other, and then the user can arrange it. Otherwise, you would have—yeah, or you could just write `0,0` to your elements if you really want to import.  
So, yeah, this is part of supporting non-canvases that are logical canvases that don’t actually support any kind of positioning. Because, like, at least you could get all the elements in, and then it would be on the user to drag them out of origin.  

But yeah.  
So we make it optional?  
Yes, although it’s strongly encouraged. In most cases, it’s going to be included, right?  
So the default, then, would be `0,0`.  
Mm-hmm.  

I think this is one of the things that sets this apart from other standards: we’re trying to include things that are purely logical in nature.  

**Resources and display.**  
And then we have resource—a resource to display, and we refer to it by ID. If it’s optional, then what actually is displayed at all?  
Gosh, OK, so remind me how resources work. We’re going to—with IDs, we’re going to have a resources array, right?  
Yes.  

OK, yeah.  
We can look at the resources. I would like to point out that it actually makes sense to not require something to be displayed at a given node. The key thing about a node is that it gives you the transform. So if you need to just have a transform around the canvas for some use case, then you could just have an empty node.  
Yeah.  

See, like, maybe nesting another set of objects inside of it or something like that.  
Right. It could be that. It could be like—that’s probably the most abundant use case of empty nodes.  

Yeah. There’s also, like, you could have some system that allows copying or taking a given visual object and moving it around to a set of predefined places. And that would just, like, copy the transforms of these nodes to itself.  
Yeah, that makes sense.  

So I guess the resource is optional, plus like one thing we had talked about including in the base layer is some sort of fallback string—like the ability to define, to just describe the node in plain text that you display when you don’t support it. And I don’t remember where, now that we’ve separated resource from node, I don’t know where that fallback lives.  
I’ll show you.  
Yep.  
OK, it lives.  
Hurrah.  

But it makes sense for the resource to be able to describe inside of itself what is the fallback, or maybe even point to another resource as a fallback.  
Yeah.  
That’s sort of what I’ll show you in a minute.  

**Scale.**  
Scale was something that confused me. Why do we need scale at all if we can just change the size? And if we have a scale, shouldn’t scale not be something in three dimensions? Or, yeah, maybe Aaron, you have some strong ideas about what scale is actually useful for.  

Yeah. So out of all the degrees of freedom here, scale—compared to, like, a 3D game engine—scale is the only one that’s missing. And what scale would allow you to do is imagine you have a sticky note with some text. Then you zoom in on that sticky note, and there’s another sticky note inside, like, you know, maybe the dot of the "i" has another sticky note on it. You zoom in there, and there’s a whole other piece of text.  

Without scale, you could probably still do that by setting the size to, like, 0.1 pixels and setting the font size of text to, like, 0.1 pixels or something. So it’s possible to do this without scale, but it’s kind of a helper property that lets you take existing things and rescale them.  

In practice, most things can be specified without scale. When I make models, I try to not include any scale and then leave scaling to the end-user app. Like, if the user wants something to be twice as big as they included, they could just set the scale to two. But in terms of being able to serialize such data into an interchange format, that makes sense to me.  

So is scale an effector and the default scale factor is just one, and larger numbers are larger?  
Yes.  

OK. Because we had zero in one spec somewhere, and that confused me even more.  
OK. To be more specific, it’s a one vector. So the default scale would be, like, `1,1` or `1,1,1`.  
OK. So you can scale arbitrarily.  
Yeah. OK, yeah, that does make sense to me.  

**Size and hitboxes.**  
If size is optional and I’m about to display something, how do I know the size? Is size primarily used for the hitbox, like making it easier to calculate the hitbox? Because you already have position, and let’s say I load a PNG. It has pixels defined, and we work in pixels. So I know exactly how large it is in pixels. That’s easy.  

But what if I open an SVG? An SVG, I think, can define a viewbox to define the size, but doesn’t have to. Then the size is sort of undefined. If we didn’t define the size here, then it’s hard to scale something if the first size is unknown at all. So maybe size is optional if the content clearly defines it.  

Yeah, that feels like size—of all of these things, I’ve been sitting here looking at size and going, "That’s the one that feels the most related to the resource."  


Right, it’s like if you have a just an arbitrary triangle shape or some sort of arbitrary polygon, it’s going to have a size, but not in a strict X, Y sense unless you were trying to draw a bounding box or a quadrilateral around it that contains the entire thing. Why have it at the top level at all?  

There’s also the question of, like, if you have an image that’s 100 pixels wide and you have a size that’s 200 pixels wide, does that just display the image at twice the size?  
Mm-hmm.  

Also, in terms of having it at the top level at all, another benefit of having it here is that if the resource can’t be loaded for some reason, we could still know what size the thing is. That could be useful for positioning things relative to that.  
Yeah.  
Yeah.  

I think the size is really useful. It’s almost as important as position. I mean, the basic building block of a canvas is probably a rectangle of content, and a rectangle needs position and size.  

I’m just wondering if everything is going to have a size—like, everything is going to have different types of size information at the resource level is my—well, I guess we’ll see as we get down into it.  
Well, in the end, we need some kind of size. I mean, if you have just a text document and you have it at this position in the open canvas, you don’t know how to wrap it. I mean, how long do you want to have it? If there is no size information, it’s just undefined.  
Yeah, no, that makes sense.  

I can see why. Like I said, I think everything is going to have a size. The question is whether it’s going to be at the resource level and have a specific meaning.  
Well, yeah.  

As long as it’s optional.  
Yeah, to have the size at the resource level is actually a freaky idea, maybe.  
Yeah.  
Maybe child nodes don’t have size.  

What don’t have size?  
Child nodes.  
Child nodes.  

So if the size is optional, we need to define what is the default size. Would it make sense to have the default size be, like, negative one? And then if the size is negative, then, like, see the resource for the size or something?  
We need to look whether different—let’s maybe jump to resources now. That makes sense. We’re mostly done here.  

**Talking about resources.**  
Let’s talk about resources. So we have two kinds of assets: resources and schemas. They are managed using similar mechanisms—inline, external, and remote.  

If it’s inline, we refer to it by ID. So we need unique IDs for resources. If it’s remote, we just can use a URI. And if it’s external, maybe we can use other names, and we use a relative URI to point to a local file.  

So a resource has multiple representations, and each resource representation—the ID actually needs to go to the resource level. I meant this wrong. So each resource has an ID, but the representations themselves have no ID, because they all belong to the same resource. They are different ways to render the same resource.  

But in order to understand them, we need to define the type—the MIME type. We could have the actual content stored inline for a resource, or we could refer to them as a location, which is then either a local path or both URI.  

So content or location must be present. The MIME types are as defined by Diana. Fonten is just an inline string. I haven’t defined yet how to handle binary content, or maybe it can just be a Base64-encoded location.  
Yeah, that’s fine.  

And then we have data URIs. They are nice. So if you put `location` and then a data URI, and the MIME type and the content actually imply it, this would be the most concise notation—just that location and the data URI.  

In all other cases, you actually need to state the MIME type in order to interpret the stuff at content and location. But if location is a remote URI and it serves a content header, then you can use that as the MIME type and can omit it here. So it’s flexible.  
Yeah.  

**Fallbacks.**  
And this is how fallbacks work. Here’s an example for fallbacks. So here’s a resource R1 with three representations: a locally defined SVG image, a remote PNG, and a fallback string. If our client doesn’t know how to handle SVG, we just load the remote PNG. But if we’re also offline, we display the third fallback representation, which is just a string. So this is how it would work.  
Yeah, very cool.  

Is that array presented in priority order in terms of representation?  
Yes.  
OK. Did you say that somewhere? And I missed it.  
Yeah. Good question.  
OK, yeah, the order for representation is significant.  
Great.  

**Wrapping up resources.**  
Yeah, it’s captured. This is great. And like you said, later representations can be used as fallbacks. It’s cool.  

So, yeah, this is how representations work. If you wanted to display "Hello, World," you need at least one entry in the resource array with at least one representation.  

We also talked about shorthand—maybe allowing a `content` property on the node with the implication of a non-referencible anonymous resource.  
Yeah, we have them in programming.  
Yeah.  

We can add that as required input.  
Yeah, maybe we should.  

**Schemas.**  
Let’s talk about schemas for a second. So we use schemas in two ways: one schema to define the OCIF format itself, and another for defining the contents of extensions.  

We can store them either inline in the `schemas` property or externally. We always need to know the version of a schema. So, given any two schema references in our system, it must be trivial to determine if they are equal. This needs to go to design decisions.  

So, what is an entry in the `schemas` array? Each schema has a URI, and that is required. The URI is like the ID of the schema. URIs just work really well for schema IDs. And this URI also contains the version information.  

Then we have three more properties, which are optional depending on the context: the actual schema (you define it inline as a JSON object), or you define the location for a schema. One of these two must be present. If the URI resolves to a valid schema, you can leave out the location, yes.  

You can also assign a name. A name is what makes this really smooth because you can, in the `schemas` array, define a bunch of schemas and give them nice local names, then use these names because the URIs are ugly. Use these local names for extensions.  

Wait, say that again—use local names for extensions?  
Yeah, I’ll show an example of how this is going to be used.  

So just to summarize, we have three kinds of schemas: defined inline, defined externally, or defined remote—just like other resources. In the `schemas` array, for example, let’s say we have an extension for ports. If ports were an extension (we haven’t added ports yet to the spec), we would define this URI and refer to it with a short name like `@ocwg_ports`. Then, in some nodes array, we can say `data.type = ocwg_ports`, and that’s it. We have the ports extension.  

Or, we define another user-supplied extension for circles, and then refer to it by its group ID and local name.  

Interesting. So instead of having, like, a centralized name server, we’re relying on the system to export non-conflicting schema names locally.  
Yeah. So the real schema in use is always defined by URI, which is global. Locally, we can use any kind of abbreviated strings just to make the file more readable.  

Oh, I love it. This is sometimes called the "pet names" system—where, within any individual canvas file, you can have pet names assigned to different schemas, and those don’t conflict because they only need to be locally consistent.  
Yeah, and you can easily make upgrades. Let’s say there’s a new `circle` version, `circle 1.1`, and it’s totally compatible with all your circle usages. You just add it in your schema array. The file is updated.  

We could also have some built-in mappings, where we have the ten best extensions from OCWG, which are sort of magically always built in. So you can even leave out this stuff for the built-in schemas and just refer to them by name. They always refer to the same built-in URI as defined by the spec.  

This probably makes sense.  

**Schemas and Names.**  
So, all this leaves me with just one question: if we have `name` as a property and the name is what we use to refer to this schema, why is that not a key in an object, like having it be a dictionary?  
That’s another discussion we had a long time ago—how, in general, we use dictionaries and arrays. That’s a bit of a conflicting thing.  

If you use this as a key, then JSON enforces key uniqueness already. But if you’re a programmer and you have such an object in your hand, you can no longer see what the name is because that is outside of that JSON object. So for debugging, this version is actually quite nice practice.  

I see. Well, to be honest, at import time, you can create your own objects in memory that both have a map of keys to use and also have the name inside of it. So you could reformat it on load.  
Yeah.  

I think either way works fine. The only thing, though, is that in the structure of the data, the fact that you have `name` as a field gives the indication that it’s potentially not unique or not meant to be used as an identifier. Can you refer to schemas by index, like "schema number three in the file"? Is that valid, or is it not valid?  
No, no.  

I remember that I created an earlier version for nodes and referred to them by keys. Then we decided to abandon it. But this is certainly quite concise.  
It is very concise.  

**On Arrays vs. Dictionaries.**  
For schemas, this looks fine. But I think for nodes, you still want to list one array instead of a dictionary.  
Agreed.  

Why?  
Because, you know, why—you can also approach it differently from code, of course, because you can easily work through a dictionary and add to an array. But somehow the structure of nodes looks more like a list to me—something that you work through and put on the screen depending on the properties.  

GLTF has nodes being an array. But the difference is that GLTF refers to nodes by index, not by name or ID.  
Yeah, we use IDs to make it more hacker-friendly and to make concatenation of two files manually easier.  

I completely agree with that because there’s a big problem in the GLTF ecosystem where people want to compose files together. You just can’t. You have to reinterpret all the data and rewrite all the IDs.  
I still think you need an ID for nodes, even though it could be a list.  

**Extensions.**  
Let’s talk about extensions for a moment. Any JSON object can be used as a property bag or holder for data, but it has to have one property called `type`.  

The `type` is a reserved property key and defines the type of the extension. I haven’t listed this yet, but `type` needs to refer to a name property or URI-type or a simple name. The rest of the properties in the JSON object are extension-specific.  

You can easily distinguish extensions by looking at the `type` property. If it starts with an `@` sign, it’s a local name defined in the `schemas` array. If it’s a URI, then it’s global.  
Why have both the `schemas` array and the `type` URI? Oh, I guess so that you can, like you said, just make it easier to use.  
Yeah.  

Got it. So the URI is kind of the base case, while the name is like the shorthand for local usage.  
Exactly.  

I also wrote that applications should not roll away extension data. Extensions should remain intact even if an application doesn’t recognize them.  

**Sample Extensions.**  
I created a sample extension to show how extensions could be documented. Each extension should have a schema, a name, and defined properties. It should also define the semantics. For example, a "circle extension" provides a `radius` property. This property implies a `size` attribute because the radius would define the bounding box of the circle.  

This is how such an extension could be used.  

Do you have an example of the circle extension within the context of the resource that it belongs to?  
Not yet.  

I’d definitely like to see a full example of an extension within a resource. And another question—can a resource have multiple extensions?  
Of course.  

We listed that. And how do the properties work together if multiple extensions apply to the same resource? Do we prefix the properties? Or do we leave it up to the consumer to handle conflicts?  
The names cannot conflict because we put each extension in its own object.  

Right. So two extensions could have similar property names, but they wouldn’t clash in the file structure. It’s the application’s responsibility to interpret them correctly.  

**Documenting Extensions.**  
Extensions should define how their properties interact with base properties and with other known extensions. That’s the tricky part. It can get quite complex.  

For example, we talked about having a "ports" extension for visual programming. This extension could define input and output ports for nodes. It might also define how these ports relate to parent and child nodes or how inheritance works.  

**Relations.**  
Now, let’s move on to relations. Relations must have an `ID` so that we can refer to them. They share the same `ID` space as visual nodes to avoid conflicts.  

Relations also need a `type`. This refers to a type defined in the `schemas` section. Relations can have additional data, just like nodes.  
Currently, the JSON schema we’re using calls this field `name`, but I suggest we use `type` instead.  

Makes sense to me. When you say JSON schema currently uses `name`, what do you mean?  
No, our JSON schema—Michael created it just to have something working.  
OK. I think `type` is better.  

**Examples of Relations.**  
For example, we could have a `set` relation with a `members` array that lists node or resource IDs. This would define a group of nodes.  

Another example is an `edge` relation, which defines a connection between two nodes using `from` and `to` properties.  

**Open Issues.**  
We still need to refine the exact semantics of relations. What do parent-child, group, or inheritance relations actually mean in different contexts? We have some good notes from previous meetings, but this needs more discussion.  

**File Extensions for OCIF.**  
Let’s talk about file extensions. What should be the proposed file extension for OCIF files on disk?  
I often like double file extensions, like `.OCIF.json`. This would ensure the file opens in JSON editors by default, while still indicating it’s an OCIF file.  

That makes sense. A JSON editor would still recognize it as valid JSON, but a smart editor could identify it as an OCIF file and provide specific features.  

But maybe it’s also ugly. Would people prefer to drop the `.OCIF` part?  
I like all of the above. I like the double file extension but also understand if people prefer a single extension.  

If we serve OCIF files over the web, we’d need to register a MIME type with IANA.  
Yeah, once the format is more developed, we could request something like `application/OCIF+json`. That’s how other JSON-based formats do it.  
I like that.  

**Namespace and Hosting.**  
What about namespaces? Where should we serve all our specs from? We need a root namespace like `canvasprotocol.org/OCIF`, followed by version numbers.  
Yeah, and we could use content negotiation to serve JSON, Markdown, or HTML files from the same namespace.  

Should we use subdomains, like `spec.canvasprotocol.org`, to make it clear?  
That could work. It keeps things clean and separate from the main domain.  

**Community Extensions.**  
Do we want to host a community server for user-generated extensions? If so, it should probably be separate from the official namespace to avoid implying endorsement. Something like `community.canvasprotocol.org` could work.  

That makes sense. We could let users host their own extensions without requiring a public domain.  

**Wrapping Up.**  
OK, I think we’ve addressed most of the small issues. I’ll go over the document again and prepare the next iteration. Hopefully, in two weeks, we can discuss this further.  

Great work, Max. This was a really productive session.  
Thanks! I’ll make sure to add any additional questions as issues for follow-up.  

