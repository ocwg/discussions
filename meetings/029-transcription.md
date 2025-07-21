All right, so this is a CWG meeting number 29, and yeah, that's got a couple things to chat about today. Aaron, you want to start off? Start us off?

Yeah, sure, I'll start off. So let me actually do pull up a screen share. It's in a request to share. So just gotten an allow. All right, hopefully we don't see that. Yeah, um, boy, this is doing Windows really covering up stuff. Let me move it away. All right. So I, so with the recent updates to the to the spec, there's been a couple updates, including some updates that I made just yesterday while I was reviewing everything and working on it. There is some new features in Oakiff called the root node proposal and the nesting canvas proposal.

And these are things that that I like, you know, really wanted to see is I'm really happy that they're here, and I have implemented them. So here's my repository for my good implementation. I, all of these commits, I just did yesterday. I went like a, like a 10 hour, like, Oakiff, it moment things free yesterday. Um, doing the sets in the groups to anchor refactoring the root nodes and then the nested this took a bit of time, but it was worth it.

Um, so let me show off my little test scene here. So I have, um, there's really nothing of notes here. Um, that's like really cool looking. It's just a tree of nodes. We have a B C D E, uh, like, you know, just just like that. So here we have, um, uh, I should maybe make this, uh, the editors, the editor a bit bigger so people can, uh, can see things a bit, a bit more. Oh, the maximum of SB goes three. I've actually never put it a custom scale before. All right, so maybe that'll show up a little better on the recording.

Um, so, uh, we have a node. This is a, a scene file called A dot TSCN and its root node is A. And then there's B and, uh, there's a child and then there's B is just there to fluff up the, the, the, the tree structure just to make sure it all works with the grandchildren and such. And, um, then we have node C and C, uh, you notice that the text here is white and everything below it is yellow.

That's because C is in this scene and the children are in another scene, but there's also this clapperboard icon on the right of C, which means that C is itself, um, also, uh, an instance of another scene. So if I actually click here, we can see C is also the root node of this other scene file called the C dot TSCN.

Um, and we have C, there's a note D, E and F in here. And then if you look here, there's also, uh, Y and Z. Now, if I open up here, we have another scene called X and X has a root node X, which is Y and Z children. And you may notice that there's two nodes here called Y and Z, uh, and it may seem a little odd at a glance to have two nodes with the, with the same name, which would be the same ID.

But remember, these are, these are actually two instances of the same scene. Um, so that is why, uh, this, this happens, um, because those are both the same scene, but the root nodes, uh, get renamed. So you see X isn't called X here. The instances of X have the name kind of overridden.

So then what I can do here is, um, I have, if I go into the, uh, scene, export, open canvas interchange format, I go to export it to a.okif, I save it, overwrite it, you know, whatever. Um, then when I go over here, I have, um, a.okif, and I can, um, open this. And here's, here's the, the nodes, and I could, uh, show the children of their, and there's, there's more, show the children up there, and there's more.

Um, and then there's also these individual files, uh, see the.okif, uh, and it looks like that. There's, there's the instances there. Um, and there's the X scene. So this, um, it, it's a, it makes sense, right? It's, it's not too crazy, but, uh, it is a little complicated to, to implement.

Um, and let me actually show you what's the, um, what's those files look like on the, uh, insight. So if I go, and that's not the right repo, um, do this one. Uh, so here is a, uh, dot.okif. So we have these nodes, we have A, B, and C. And if we look at, um, C, uh, it has a resource, which is pointing to C dot.okif, which is actually not a file name. Um, it is the ID of, uh, this resource.

Um, and then that resource has one representation, which is set to a location of a file path and the MIME type of application slash, okay, plus JSON. And, um, my exporter implicitly creates a folder with the same name, just because I figured that would be a good way to organize things and avoid naming conflicts. You know, if I can, to nested scenes like had a different, okay, files that were given the same name or something.

Um, so, uh, then you see is the same way. Uh, there's, you know, these two nodes here that each reference, X dot.okif. And then there's a single resource that has X dot.okif and points to that file. And I'm also, each of these files has the root node property that's been recently added. So this points C points to its C note, node is the root node. A points to A is the root node.

And, um, similarly, X points to X is the root node, which gets renamed in its instances.

Um, so that is the, um, implementation of the, uh, the nesting canvas proposal, uh, as described, uh, here and in the root node specification here. Very cool.

What's the, what's the use case in Godot for this? Like where do you frequently see this coming up in real world Godot usage?

So, um, to be honest, the kind of status quo, I think is people typically don't do this because, um, people, um, well, they're, first of all, for 2D things, people don't have a canvas format currently, which is, it's great to see. Okay. If you know, helping to change that. 

Um, but then for 3D, people usually just want like a simple file that can move their meshes. Uh, so the 2D equivalent of that would be like, you know, bringing in your images, I guess. And that's like trivially simple.

Um, but, uh, this enables you to have more complex, uh, scene trees that are set up in a, uh, agnostic way. So imagine having an entire, uh, like nested UI systems split up in the multiple files and you make that in like Figma or something. And you could just bring that into Godot engine, uh, and all of those files can, um, reference each other and import as one unified structure. That would be very cool.

Very cool. I mean, nesting, obviously is, is very useful. If you get more and more maps exchanged in Oakiff, you can just plug them in into your big unified personal knowledge management map and, and everything is organized in one big map via nesting. That's how infinity maps is handling data.

I have a question about the node renaming. I didn't rocket when you presented it. If I, if I have a node called a and my resource points to B and B says B is the root node. And that's how B is renamed into A.

So, uh, so the idea, yes. Um, what, what, if we have like, um, this example file X dot Oakiff where X is the root, but then it's instances. Um, we have, uh, E and F and those are the, what it gets free names to, um, because, you know, you can't have two nodes here, both called X, um, that would be weird.

Yeah. Okay. So just to add some nomenclature, when I wrote that snippet of the spec, uh, I called it the host canvas is the one that's doing the import to avoid the terms parent child. And then the imported one is, yeah, the imported canvas, so host and imported. It's not a nice pair, but at least okay.

Yeah. So, so the host node overrides properties from the imported node, correct, which is clever because in that way I can reuse an imported map and customize it to my liking. And that works reasonably intuitively how I override properties in a JSON tree. So if I define something at the same path, then my object replaces the object that was there.

Yes. It gets a bit tricky though with our extension system that we need to define, I think a little bit better how this overriding actually works because we have an array of extensions in the child in the imported node and an hour node and the default would be to completely replace the array.

Yeah. Maybe not what the intuitive intention would be. So we should maybe define that for our arrays.

I'll be honest. Um, it does need is a problem. It does need to be solved, but I don't know if, um, if that's something specifically that I would need because the, um, the instance of, of a scene usually isn't going to be, um, specifying more data, uh, in, in that describes like the node itself because that's usually defined in the, um, the, the sub scene, um, and not in the, in the host scene.

Um, what is defined in the host scene is stuff that must be different. Um, for example, the, the transform because you can't have, you know, multiple instances of the scene overlapping that will look dumb. So, um, one of the things that, um, that my code does is make sure that, um, the, the root node of the sub scene is, is excluded when we're considering the visible and transform properties.

And then instead these properties are, uh, used on instances of the scene in the host scene.

Um, let's take text styling as an example because those are quite orthogonal. So we have a font size, a font color, uh, and a font family. So I'm importing something, but I'm old. So I need font size to be overwritten, but not the other parts font, a font family should say the same. So then I want to override some properties within the text style extension.

And for that, we need to define if we don't replace the complete area of extensions completely, but treated more like a map. Right. Like a map with like a coalesce where you like coalesce the override properties onto the, uh, onto the map. So if they were defined in the, in the parent, they would be overwritten by the child properties. But if they are not defined in the parent, they'd just be like added on.

Yeah, but avoid parent and child. The host is overriding the imported, which is a bit counterintuitive, but yeah, but, but more powerful.

Yeah. So you're right. That is a good, uh, important use case that needs to be handled.

Yeah. Cool. And you're saying Max that that's not currently clarified in the change.

No, it's not. And we should, we should define how this overriding mechanism works and then use it for this host import stuff and also for normal parent child inheritance because of the same mechanism.

Yeah. Okay. Well, did you make a note of that?

Yeah. Great. So if we have the same understanding there, then I can put it to words.

Yes. I think that makes sense. Okay. You're in a green as well. And then, uh, then Aaron, I agree to all the changes you made except one, which is you said, if you do this and this, then the file is invalid. And that's a strategy we haven't had so far. Usually we do, then we ignore that property.

Okay. Because in well, I mean, we could also do invalid, but we haven't done before. So what. I mean, that's that's just up to you on how strict you want the spec to be. Um, from my experience with, uh, like people implementing, uh, GLTF files wrong and, uh, implementations being too loose and too willing to accept bad things.

And then you send it to another implementation that is completely broken. Um, I, I do lean towards, uh, making it as strict as possible, but feel free to push back on that. If you want to do, do that change, you, you've said to just say, ignore the property.

Um, I'm happy with that.

Yeah. We could also say, uh, a good implementation should emit a warning to, to have at least that in the ground.

Yeah. And we can also, uh, have a validator, emit a warning on this case as well. Right. When we, when you do feed it in, cause we do have a validator, um, right now the validator just validates that it's valid Jason. It doesn't, or it doesn't like validate a whole bunch of things about the spec as far as I know, but eventually we should be able to emit things like warnings like this is not, this doesn't match the schema.

Um, yeah, we're not very strict in that regard. Maybe we should start at this place and say blah, blah, blah, turns the file invalid and implementation should ignore it and emit a warning. I mean, we can also write the implementation should just die, but most implement less useful, like that.

Yeah. And also I think we've learned from like HTML and other things that having a very permissive, uh, implementation, a permissive strategy for rendering the, uh, the markup can be very helpful as well.

Um, the warning would be helpful too, to, to not spread false structures around.

Absolutely. Yeah, that makes sense.

Uh, ready. Cool. Thanks for implementing that. It's awesome.

Yeah. Awesome for writing it up. It's so cool to see the pairing of that of Max writes that adds the idea. Well, we talked about it over the last several meetings. Max adding onto the spec and then having Aaron implement. I mostly brought down good ideas from Aaron.

Yeah. And it's, uh, it's good that we got that into, um, it, uh, a format that kind of fits together well with, with Oakiff. I don't know why it did not occur to me to just have a property that says this is this, this, this is the root node because I was just thinking, you know, GLTF, right? Oh, no, no, no, the, the root node. Well, no, no, it doesn't exist.

Yeah. And for the, the points about, um, like, uh, giving a warning when something's invalid, this is, um, an example of something I've already done, like, in, in giddo, there was this problem where it was too loose and accepting misaligned data in files. And it was just not importing in other engines.

And even though the asset worked fine in giddo, so, but now it shows a warning that's like, Hey, your assets wrong.

Got it. Also, I do want to briefly point out the kind of, um, let's, let's call it, uh, irony that's the only, um, the only resource that I have implemented in my Oakiff importer is another Oakiff.

Uh, wait, I don't even, I don't have like the path node or oval node or images or anything. It's, uh, it's very much a, uh, I'm a nerd and I just wanted to get the structure right importer.

Yeah. That's great.

Well, um, should we move on to other topics?

First, uh, I'd like to say welcome Mitchell, like, um, oh, oh, okay. We dropped screen sharing. Let's go say you like, you guys all disappeared because Zoom decided to reorganize my UI.

Um, hey, Mitchell, welcome. Um, you can unmute, introduce yourself if you like, um, or you can just lurk. It's totally fine.

Um, I am not pro, I'm not involved in any projects. I'm just here because they like open standards and I'm Aaron's friend.

Cool. Sounds good.

Also, Mitchell is a very heavy, uh, user of Figma.

Um, so, uh, you might have a useful, uh, input into like, you know, how we could design stuff to be work well with Figma. Very cool.

Great. Yeah. I think especially, um, I think the play, the starting place for integrating with Figma might be Fig Jam instead of Figma, just because it has a much smaller feature set.

Um, and I think there's probably a higher overlap between people using Fig Jam for things that are like white-boardy, infinite canvas-y shaped as opposed to sort of the, the all-in nature of working with Figma itself, which is so powerful.

Yeah, no, totally understand.

Cool. All right.

Do we have other stuff, Michael, do you want to talk about some of the work that you've done?

I'll go ahead. Look, Max. I have two more, a little issues.

Yeah. Um, so we've, we've added that we can tell the root node what its size is and effectively that defines like the size of the canvas.

So for the initial camera that gives us a little hint, so the initial coordinate system, the root item as a size.

So if then an item is placed outside of that root item, it will initially not be visible.

This is cool, but so we can place the virtual camera in the beginning in any rectangle as long as it starts top left zero, because we don't have any other relative coordinate system yet.

And we cannot say we want to start here. That doesn't work. We don't have an offset.

I like that personally, because that falls into convention over configuration, which is a term that I've always used in my head, but only knew the words for like literally last night when I was looking up stuff.

So just says that like, okay, you want you want this to be like where the camera starts?

Well, then make, make all your objects at that position, because it makes sense to start at zero, zero. It just, it's simple.

Yeah, but what if I have a canvas where I want to share, let's open the canvas and look at bottom right.

Some tools, I think here draw has like a view start position where the camera looks at some other spot.

So we don't have a way to express that yet. And I think last time we discussed, we want to add extra properties to the canvas itself to extend the core JSON schema to have a, yeah, how do you call it camera position defined?

And if we are at that, do we need like a view box or something like that in TL draw?

And do we need multiple named view boxes or just one or what's the, what are the requirements for the view box? I'm not familiar with TL drawing us.

Yeah, I'll go look up the TL draw docs while we're talking.

But I think the general idea here is if we're following the pattern of the rest of the oak if spec, it's possibly, we probably should have the canvas itself be a map that can be extended with extensions, right?

So a third type of extensions, note extensions.

Mmm. Good question.

How different are our node and rel relish relation permission? I mean, extensions.

I'm trying to remember if we, did we unify them or not?

Spent two weeks. It's a different kind of extensions because relations and notes are different, notes have more visual properties and relations are very freewheeling. Relations only need to have an id and everything else follows from this function.

Yeah, sure.

So in just as a point of reference in in GLTF land, there is the way you extend anything in GLTF is you throw this extensions property on something, then you have some prefix, some extension name with a reserved prefix that you don't conflict with anybody else's name.

And then you have whatever properties you want inside of that. And this can be thrown on anything, but it can also be thrown on just the root object. So you could just extend the entire file itself.

So we could do something like that for oak if that not saying it used to look exactly like this, but this is what GLTF is.

Yeah, I would, I would think that the root node would be and would be a, could be a target of node extensions. In other words, the root node could be extended by node extensions.

And I'm wondering if that, if that would satisfy the, that constraint max, although to your point, maybe they are actually a different kind of, maybe it's actually a different kind of thing, because these extensions are very meta, like view box, doesn't make sense to the box extension onto another node, other than the root node.

The root node, it's, for node extensions on the root node is useful when that that extension makes sense for other nodes. And you just want to be able to put it like on the whole document as well. And that's what the root node is there for. So like, you could just put stuff on it if you want a node extension to a final document. But if something is just for the whole document itself, like some kind of like camera position, it doesn't make sense for, you know, a grandchild node to say like, Hey, your camera position goes here.

I mean, actually, well, maybe it makes sense. I'm not entirely sure. But like my, my thought in my head right now is that this is more of like a just, you have one per document type thing.

And then that makes sense to go in like a dedicated area that's not, that doesn't interact with the root node at all.

I think we are on the same page then that we should have canvas extensions. And they are a different thing. And there's, they use the same mechanism, but they are the type of extension.

I think that's probably right, which there's the whole, since we've been hat tipping to rails already with a convention over configuration, which is where that community came from.

We could also talk about the, the drive principle. Don't repeat yourself, which basically says the first time you do a thing, do it the second time you do a thing just create a new thing. And the third time consider creating unifying those.

So we have node extensions, we have relation extensions. Now we have canvas. Should we just have extensions? And is it helpful to collapse those distinctions? Or is it more helpful to maintain the separateness of those different, like I'm reading the extensions doc right now and using over that.

What would it practically mean to combine them? Because like, if you're making an extension, I would assume that it only makes sense to say like, oh, this extension is for nodes, or this extension is for the whole campus. There's, you can't, it doesn't, it would be maybe weird to have an extension that applies to more than one thing, or maybe there should be multiple extensions at that point.

What about extensions that can be applied to relations and nodes or to the canvas and relations? We could have better relation states for what types it is applicable.

True. It's more a cognitive conceptual thing to say. Yeah, there's only one type of extension, the extensions. Yeah, you define where you can apply them, or where meaning is defined.

Yeah, it's a good point. But it's just extensions. And they all follow the same structure. They do follow the same structure. Yeah. And they just, we, yeah. It's more marketing to say, it's just one kind of extensions because the reality probably most fall clearly into one category.

Yeah, no, that's a good point. And I'm looking at kind of the way that we've structured them and the extensions folder is pretty clear.

Yeah, okay. I think I buy that it's just another type of, it's another thing that can be extended with our general concept that we have of extensions, but it's going to be a separate kind of thing to extend the canvas than it is to extend a node or extend a relation.

Okay. Let's send the the target of an extension or the.

Well, it's interesting because what do we call that? Yeah, we don't really specify that if you look at a like a node extension is a node extension based on where it shows up in the file.

Right. We also have the node in the schema. We have different sections for node extensions and relation extensions. So currently we separate them a lot. So technically.

Can you bring up, can you show your screen max and show an example? I'm struggling to find one in the docs right now.

The schemas right now, I'll call blah blah dash node Jason or dash rel Jason to distinguish node from.

Yeah, so we that's one way. It's in the name. It's in the name. It's the way we do it.

Yeah. Okay. Cool. Yep. And we know that's what I was noticing. I was noticing that there's not a, we don't actually have a extensions slash extensions and then a nested map of node extensions and then a nested map of relation extensions.

No, no, no, it's just no. It's just one thing that schemas and then in the schemas, they have a name. In the name, we by convention include the type of extension that it is.

Yeah, Okiff slash node slash thing. Okiff slash rel slash thing. So I guess we'd have okiff slash canvas slash thing. And then the other thing I was going to say, the other thing defines whether extension is a node extension or relation extension is also where what item shows up referring to that, like what kind of thing references that schema in its data in its property bag, right? Like if a node references that thing and it's property bag, then it is a node extension because it's being used on a node.

We like the naming thing is completely arbitrary. We don't, do we even, do we even encourage it like must or should? Maybe, but if we unify more, maybe we should drop that naming.

That's kind of what I'm, that's kind of what I'm wondering. It's like suggestive but not required.

Yeah, that makes sense because really the name of a schema does give you like a hint to how it's it's used. Like here's here's a brief example again from bringing in stuff from GLTF land is this is a the physics body extension and it says the file starts with node dot which indicates this for nodes.

It says in the title, it's a GLTF node extension, but then there's also this other file here, which is extending the whole document GLTF document.

This is for everything that goes to the root document and this is everything that goes into individual nodes. So there's the same like extension standard, but the extension schemas are individual.

But I should also mention that there are some extensions that apply to everything.

For example, there's one that adds like called KHR XMP JSON LD, which adds like copyright metadata.

And that can be placed anywhere in the file because like it allows you to say like, oh, this node is like licensed for this thing, you know.

Yeah, I think the thing that I'm noticing is like in order to add canvas extensions, we don't actually have to do anything other than add a data property to the canvas node, right? Like our extensions already support that. Like we should we should expand on the language in the extension section to say that there's another type, but it's purely like you mentioned Max, it's purely conceptual. It's we'll have like another name there.

Yeah, I would just need to clarify that. But yeah, there's no big change.

No big change, which is nice. I think that's what I was yeah. I think that's what I was going for when I was posed the original question is like, is our extensions general enough that we could extend another type of thing without a significant change?

And the answer is yes. Yeah, taken to the extreme, you could also have extensions extending other extensions because an extension can provide a field for extensions.

That's a very good hint for the next topic, namely themes, because in themes, I was really tempted to do exactly that. So if we have a theme in a very generic way, we could say that a theme is like a branch of worlds. We have the dark and the light mode.

But you could in the dark mode still have the grand parent mode with the big fonts and the teenager theme with the small fonts. So recursive theming.

So you put a theme extension on a node, then it will get inherited everywhere.

So you put it in the root node and it applies to your whole canvas.

Then you have a dark mode extension. And in there, you want to specify the font size.

How do you do that? You just use the extension for font styling within the theme extension.

I think I put that in the current draft and we can take a look. But this is where I got a bit unsure whether that's a good idea.

So you did put it in it's in the draft here.

Yeah, somewhere.

Yeah, in the extensions file. I see it. A good goal. Theme proposal. I'm opening that.

Let's see. I'm going to share my screen real quick.

Yeah, perfect.

All right, sure. Here we go.

All righty.

Okay, so if we have this on the root node and we put data, blah, blah,

Okay, if no theme. So now we are in the theme extension and we put some data there.

For example, a map using dark and light as keys and in there within the dark definition,

we say, hey, let's define how the text search would work. So we put the extension in the extension.

This is one example where nesting might be useful.

The good thing is in this way, the text style extension itself does know about themes.

The application must be able to handle themes. And then if the application asks,

okay, what's the text style? The theme extension says, wait a second, we are in the dark mode.

So I'll give you this text style. And the theme extension doesn't know what's in the text.

Style doesn't understand that, but it can handle, hand out the right JSON object to the other layer.

So yeah, this is a way the theme could be built, but maybe there are less nerdy ways to do it.

Gotcha. So, okay.

All right, so what we're saying is that,

see, this uses it on the root node, like we were just talking about.

Yeah, just as an example, yeah.

I mean, I see how useful that will be of like being able to extend the root node.

Interestingly, that you called it a node extension.

Because we place it on the node, and you can also have it on a node further down the inheritance

through, if you just want to have the yellow font in this part of the map.

By the way, that's the same way that themes work in Kado, if subnotes could have their own themes.

Cool. Yeah, this seems like a pretty expressive way to do it.

So this is saying that this

this particular extension is, yeah, in the data, so there's a called Ocuff node theme.

That extension can have arbitrary properties, arbitrarily named properties in it, and each

arbitrarily named property can also be extended or also has, yeah, can also be extended with

extensions in its data property. So interesting.

This is just really the first draft. I think it came also out of discussions with Aaron, frankly.

Yeah. But now that's maybe something to sleep over.

Imponder. Yeah. Interesting. How are you thinking about canvas extensions?

I know I'm popping back to the previous conversation, but this is a good motivating example.

How are you thinking about canvas extensions versus extending the root node?

Like, would the view box be a node extension on the root node, or would it actually be,

would like the entire, the top level canvas have a data?

For the view box, that really smells like a canvas extension itself, because I can't

imagine what is a view box defined on a lower node. I mean, it will never be active.

Got it. So it would actually be in the...

Sorry. There it is over here.

So then we would have like, okay nodes, relations, resources, schemas, and would there also be a

data property at the top level? Yeah. Okay. So we'd add a data here on any schemas.

That would be an array, which would have an array of extensions, effectively. See how we

describe it here. Yeah. It would look like this, except it would say extended canvas data,

or canvas extension data here. Okay. Yeah. Okay.

Release that forward. Yeah. Okay. And then those extensions apply to the whole thing.

And then you were saying, now, now that we'll have a, whoops, where that's...

Another example of a potential canvas extension would be the,

the PRI made before for the binary data. That could be just chucked in a canvas extension.

Yeah. That would work. Mm-hmm. Mm-hmm.

I'm going to come back to your pull request here.

Improposable. Interesting.

Gotcha on the root node. And then root node proposal.

Still getting my head around all this stuff. I apologize. Let's see. Okay.

Gotcha. So we're going to add a root node and then add, and that points to the ID for that node,

which is in the nodes array. It makes sense. And then we're adding data to the top level.

Cool. No, I think this, I think that actually improves the sort of parallelism

of taking advantage of the extension, this facility that we've already built to be able to

extend the canvas itself. Like you said, Aaron, it handles more than one use case that we can

think of already, including that binary. One. Okay. Yeah. I think sleeping on the

theming thing and potentially writing a few more examples might be helpful

of, and like possibly asking an LLM to generate some alternative ways that theming could be

represented or brainstorming some alternative ways and then being able to pro and con it for a

second of like, which looks better, which is easier, which is more robust. We had some thoughts

about color palettes. Do color palettes somehow sit into that seeming idea? I haven't thought

about that, but it's somehow the same area. So color palettes are interesting.

In the sense that the way that both Obsidian and TL draw work is they have named colors effectively.

And those, those smell like canvas extensions to me of like, these are the named colors that

are available in this canvas. I think, I think I'm right about this.

Yep. Here they are. They're very specific. The number one is red. What red? Just red?

I hate that so much. I hate that so much.

Oh goodness. Yep. So yeah, they're, you can just specify using numbers.

Yeah. Anyway, no more to say about that. But anyway, these smell like canvas extension,

like you could have a canvas extension that says like, here's your color palette,

and then when specifying a color, the real question is, do we want to change how we

represent colors to enable using a named color? Because right now,

we don't support a named color. We support our, so, yeah.

Interesting. Oh, that's wrong. Oh, that adds transparency, right? That's the eight digit one.

So rarely see this specific, see it specified this way. I mean, it's to RGBA, not.

Yeah, it's easier to parse. Yep. Yeah, it is. Okay. All right. So,

so to recap what we've discussed so far, root nodes seem good. And this is should have extensions

by adding a data property. Seeming could possibly happen by allowing extensions to extend other

extensions. And for about a general facility. Okay. Any other topics? We've got about 10 minutes to.

If I can put a theme on a node, yeah, and have it inherit down, why not also inherit color

palettes with named colors, so that the later node overrides what color two shows up as.

Oh, I see. So this would be like

either override single colors or whole palette. I mean, but if teams can be inherited and travel

down, then why not color palettes? But they seem to be so similar conceptually.

Yep. And they could also be at the root node. They could be that could be an extension to the

root node. The use case for these color palettes is I'm assuming it's something like you have a

color in your canvas named like background three. And that's just like defined somewhere else. And

that way you could just change that one definition to change all the places that's just using it.

So it's like a semantic meaning. As opposed to like a find and replace where you have just like

10 instances of the same red tone and you have to like replace them all.

Yeah, I've been I've been tempted to like push this responsibility onto the TL draw

exporter importer and obsidian exporter and importer and be like, look, the fact that you do weird

things with color palettes, that's your problem. When you export a oak if pro oak if file,

like map your weird colors onto good old fashioned like hex codes. And when you import things,

map them back onto your weird internal thing. Like, when you see this X code, it maps to your weird

internal color red or oak, oak, oak, or kid, or kid, whatever we saw in obsidian. And then we don't

have to absorb that. So we just sell into the specs. Just don't simply just don't need named

colors. I don't think so. That doesn't think we need it. I don't think we need it.

It might be nice to have and she mentioned this, I believe last meeting,

that there was that challenge of how to represent the TL draws colors. And I think my answer is just

X code's yo. I think this could easily be done with an extension too. You could just

provide the actual colors there is like a fallback and then just add an extension that says like, hey, this color is actually background three. And then like you provide the palette and then you

know, the app could use that if it was or if not, it'll just have the colors that it is.

Yeah. Yeah, I think kind of an extension. But if we specify the extension, the chance that

more apps use the same extension is higher. Sure. But yeah, I'm just not, it feels.

Yeah, I don't know. Okay. Let's wait where that comes out more often.

Thingo. Yeah, exactly. Speaking of implementations and getting more usage of the spec,

actual usage, Michael, do you want to talk about, give us an update on like the lib work you've

done with the utility? Yes, I've started work in a repo of my own, but I want to move it, of course,

to this repo on the root, I'll share the link. There's one moment.

Sure. It's it's in the discord.

This is the link to my repo currently. I really want to move it to the root of this,

this repo might feel it's good enough to do that. Currently, I can share my screen and show what

I have already. That's maybe your best. Sure. Let me, uh, I'll stop sharing. Go for it.

All right. I've used an X to build this mono repo,

which has currently pre apps. One of them and the fourth one is just for testing and library.

This library is used by those three apps, JSON-Converse app, Node.js API and the OKF tools app.

I've just included this Node.js API to test if the library also works with Node.js.

And this is the JSON-Converse transformation application converter.

This is the current pallet data that we have.

You can run them both on the same project and they say they use both that same library.

Nice. So both those apps use the same library in the in the mono repo.

Yeah. You can just want this fun data can export to JSON-Converse.

And after JSON-Converse kind of import it back. At least it should.

It seems to hang now, I think, I'm not sure. Let's try again.

I thought that this works, but that doesn't seem to work.

Yeah. The nature of demos.

Yeah. Never know if it's going to work. All you can say is watch this.

Yeah. Let's see. Maybe I have.

I should have a file somewhere, but that's.

That's right. Again, with this one, export.

But I think the idea is clear. This should import the Converse file.

Yeah. This one works.

Nice. This is just the same tools that you already have.

From you, just that they use the same library.

Yeah, which is huge.

Yeah. This library is publishable to MPM if you want, if you want to.

Very cool. Just through the library right now.

It's probably not. It's a very simple implementation of.

Probably not even following this back at all points.

Because I think I've implemented an asset Converse in here, some time ago,

we've already been discussing it further.

This is the top script version of the schema, although it's not.

It's just JSON, so.

Not strictly validate yet, but this is coming from our repo on this back.

Very cool. At least it's a start.

There are some in the read me, there are some comments that you can use to.

Do the annex build.

Yeah. To start, to start everything.

I think annex is a good way to set something like this up.

It's fine if you don't know if you guys know it or have heard it.

I've worked in several companies that used it and I never got good at it,

but had worked within those monorepos. I've never set one up myself. This is cool.

That's some good defaults I think.

It's a very nice thing that was shared some time ago by somebody on our

discord that uses burn for the monorepos.

I think this is much more because it depends on an ampere and that's probably better.

Although burn itself is very good, of course.

But I don't think that everybody probably has that.

An ampere can be used probably also all pipelines that are hosting providers like Fossell or PowerFlare.

Yeah, that's still very basic, but at least let's start.

Yeah, you created a whole little ecosystem of apps and libraries.

Yeah, but then that's what annex helps you with. It's not that much work.

Annex can create a monorepos and you can just say, "I want the library, I want an app, a React app,

an Angular app, or whatever app." If it's supported by annex, then that's pretty easy. So that really helps.

Where's the process by which you would

publish to NPM. You said that that was already in there? The library?

It should be. Let's say, I think it should put commands in the scripts over here.

That annex has a release command that you can use to publish.

That we probably should set up an organization in NPM. Yep. Add some users to it.

Then you can publish this, I think pretty easy. That's good. Yeah. Michael, do you want to

set up the organization or would you like me to do that and add users? Happy to be the admin?

Yeah, I think you can do that. That's better, I think. Okay, we'll do. I'll make a note to do that.

I can create a pull request for

to put this in our own repo. I'm not thinking what's the best way to have it.

I probably can just move over the files. Yeah, I think you can move. I think you're an admin,

so you should be able to just move it. I can, of course, transfer the whole repo, but

that's not what we want, I think, in this case. Oh, you could, if you want, and we could just

rename the old repo and deprecate it. It's up to you. Let me know. I'll keep an eye open.

That's what we're going to do, I think. That's better. Yeah.

I'll move it. I will transfer it. That's better, I think. Great. Okay. I work from there.

I have another meeting I have to run to. Got a lot of good stuff this week.

And yeah. Talk to you guys in two weeks.

Yeah, I'll plan a new one.

I'm not home. I'm not sure if I will be able to join. I'm really busy upcoming weeks.

Okay. Sounds good. All right. We'll see you soon. Okay. Bye, guys. All right. Have a great time.