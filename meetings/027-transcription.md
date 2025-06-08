Welcome to OCWG meeting number 27. So a couple things for today. I wanted to show the slides that I presented at local first comp last week, just so y'all have context. According to the local first comp organizers, the talk should be out in like mere weeks, a week or two. So we won't have to wait too long to agonizingly sit through my presentation. But I can show you the slides today. And then she has been doing some integration with OCIF between TL draw and Excala draw. And but they could share what they've learned so far. And then, yeah, Max, I don't know if you have anything like discussion items, Max or Michael.

No, I mean, last thing we synchronized was this PR, bringing everything to 0.5, which you integrate into main meanwhile. So we are stable. Now we accumulate more feedback and become unstable again. That's the goal, right?

Yeah, exactly. So how do we call the next one? 0.5.1.

If it's no, if there's no breaking changes, like if we're just making, which we hope,

Yeah, which we hope it'll be 0.5.1 exactly. We can make a branch for that as we need as we need to.

Okay, cool. Let me see if I can get my slides working here. Let's see. Actually, Chee, how about you go first? And then I'll, I'll jump in with slides when I can get my, I had to move them from my travel computer to my home computer. So I'm waiting for them to transfer over.

Excellent. Really good when the local first comp just demonstrates the need for itself.

Indeed. Exactly. Yeah, I can, I can share the little thing. I can just quickly show like what it is, the context in which like I'm, I'm using it. So this is like a little book, which is not that I'm making with all of the time that I have. And it's just like a thing where you've got like a concept of sources that current create files. The files are files that are backed by like an auto merge document. And then you've got views that can be like editors or they can be a read-only view. Like an editor gets like a full auto merge dot candle and read-only view just gets like the current state of the doc in an unchanged callback. And that's, that's all it gets.

So you've got this, you can make like a little document. This is a like code mirror or like a mark time preview that can open mark time files. And then you can just like hop over and open it up into one and something else like this HTML preview over here. And then you've got like a something that feels like one of those mark time editors that she was a preview on the right hand side. But neither of them have like agreed on anything here. Like they're both just like views on an underlying mark time file that's just like a document with a dot text of string.

And then where I've ended up in making it. There's also actually one of the types of views is like a plugin editor that lets you like make, make your own like plugins inside the app itself. So you can like go here and like install a install like this is a standalone view that just shows the state of all of the different auto merge documents that are there. And we're like I'm building a plugin inside the editor and then installing it from within inside itself. And then being able to use it, you can create new types of files, new views and then like operate them, operate on them all within here.

So you've got like a like a sketchbook for the computer for computation. But in here, one of the types of files I have is like this open canvas file, which is using open using OCIF as the underlying data structure data format. If I like draw like this rectangle here, and then if I open this up in like a new window, let's see if this actually works.

Are we excited? I'm already excited.

Hey, so then we've got like, we've got like rectangles and they're working, it's collaborative between these two things. If I sent you this link, you could also look at it theoretically, but let's not try that. But another thing I can do here is I can now open up this in an excali draw view. And now I have like the same, the same rectangle being, that was exciting, wasn't it when it just turned black for some reason?

And now I've got the same rectangle being being operated on in both like Excali draw and TL draw at the same time. I can make a new one over here. It appears over there. And it's because they're both just like views on this underlying format, which is great. And definitely, there's a lot of stuff that I've run into with the fact that neither of these think about canvases in the same way. And neither of them think about canvases in the same way that like OCIF does, right, which is fine. But it's, it can be a surprise.

They resize this. It will turn red.

Yeah. So like there's stuff trying to figure out what the color should be and how I should pass it across. Like on TL draw over here, you've got one color, but on excali draw, you have a background color and the line color, right? So in those cases, you end up doing things like trying to sort of guess. It's very broken at the moment, but like trying to sort of guess. Okay, so if there's a background color and the background is also transparent, then that should set the fill style to the to white. And it should set the line like the stroke style to being the color on the TL draw side.

And then over on the excali draw side, you would set, okay, background color is white and the stroke color is red. But then if you set it to solid, now the stroke color and fill color are being set to variations of each other on the TL draw style. And you sort of have to have these maps and functions that are going like, what is the closest color to this hex code that I have? And then let me find like out of this set out of the palette that I have what I should use and then try and like, take the solid and and fill styles.

I had at one point this like loop that would always be a four step loop where I would set the color in the TL draw side. And that would call scally draw to like update. And then it would have a slightly different interpretation of what the colors meant. So then it would it would make a change that would send it back to TL draw. It would then like do another change, then it would go back to excali draw and it would be like, well, nothing nothing new. So I'll just I'll just fill out. And it was funny because it like it would have been an infinite loop if it wasn't for just it eventually excali draw thought that nothing had changed. And it just sort of you would see it you would create a rectangle and then it would go that stuff.

There's also things like I had started building all of this color code. You might have noticed in the discord, I asked like, is there sort of a canvas? I knew that the answer was no, but I asked the question asked it like a question anyway. Like, is there such a thing as a theme or a canvas wide color that I could use to to take thing? Because after building all this color code, when I did have it actually working and it not being broken, like it is right now, you then hop in here and go to dark. And now these are different colors. So now this matters.

And like, now what I'm going to be what I'm going to be communicating from this side to this side is like different stuff. Should that be like, should that be encoded in the okith file or not? Because for as far as tl draw and excali draw are concerned, when it's in dark mode or light mode, the color is actually the same in its opinion. It's red, right? But when I'm saving it to okith, depending on what my like operating system, like what time of day it is, this could create a different okith file, right? Which is weird. And if I'm then interpreting it, like the light red might become the dark red. If I'm pulling it into like a light mode, if it was saved as a dark mode tl draw file or saved as a light mode tl draw file, and then I change the thing, and then I load it again. It could be that a dark red rectangle is not a light red rectangle, because that's now what's the closest color to what was in the file.

So these are the sorts of things where I was like, I'm just going to start with occasionally collaborative rectangles, and then I'll move on to circles. In fact, like the default file that I create, if I hop into the lot of merge doc editor here, which is currently also extremely broken, the default file that I create, like actually adds a circle somewhere, like it adds an ok circle, because I thought I'll just have that as the default. So there's a circle on the screen, but I have never gotten as far as rendering this circle that's in every single one of the files.

So every file that you make in here has a circle you cannot see, because rectangles, it turned out to already be an extremely hard problem. Rectangles harder than they look.

Wow, that's interesting. And would you characterize the problem primarily as figuring out how to use the primitives that you have in OCIF to represent what is already in TL draw, and what is already in Excala draw, and then like there's both the right from TL draw to OCIF, and then there's also bring the rectangle in from OCIF to TL draw and map that.

Right, it's like you want that TL draw will guarantee stability between load and save, and then Excala draw as well, right? And they sort of can't, because, or at least at the currently, there's not a clear way of doing that, where if I load a file in as a TL, if I make a TL draw document and save it to OCIF, and then change the theme and load it back up, for instance, like will that be the same document if I then save it back out again, or will there be a date?

Right now that would end up being a different document, you would save a TL draw file, you would as OCIF, you would import that OCIF file, change the theme, and then save, and now you've got two different files, these are not the same file, because it has a concept of light and dark mode, and I know Kif doesn't, but I don't know if OCIF should, it's just that it, that's what happens, so there isn't a guarantee of stability, because the thing that you would, yeah, you would need that whatever TL draw saved when it was loaded by Excala draw, because you've got to sync in this case where you're using this shared language of OCIF, it's like reading and writing, like it's doing import export on every pixel, every change of every pixel is an important fastest possible round trip.

Right, exactly, like if even if Excala draw and TL draw, yeah if they don't guarantee stability on that import export, and you can very easily get into a situation where you create a circle and they disagree, there's also some other little details that are just like just real good fun, like if I open this with Excala draw, and then I go to rotate this, isn't that exciting?

Uh yeah, because I haven't yet figured out, and then if I like rotate this here, like this is then again different, because now it's up at the top left hand corner, it's like there's, there does seem to be some sort of strange mapping that TL draw is getting up to where you're like, I think Orion told me you're like rotating around this center, but it like, it does some clever stuff, it does some math, so the actual rotation number is around the center, but like it does clever math to figure out how to make that rotation be based on the corner that you're on, which is something like that, but yeah, this is just a little detail that I ran into, this is the reason I have not yet moved onto circles, for instance, right, like this is one of the examples, I haven't even gotten the same, even if I get out the Excala draw thing, getting, getting, I was a bit off way more than I could chew, I got so excited by the idea of having this translation happen, and now I realize that I need to just figure out how to have a stable TL draw language before I can even, before I can get thinking about the Excala draw, because if I can build that, if or if someone can build this stable import export, which I assume that somebody's doing right, it's not 0.5, we're all, we're all RC, everyone's implementing this stuff.

Absolutely, everyone, every Canvas maker is, I've been started yesterday morning actually, that was like, Monday morning after local first comp, everybody's like getting to work on it.

So now I can just wait, although the thing is I also can't just wait, because I don't just need Ocif export, so that's one thing, when you load the document, I need Ocif import, but then every change, I need to like translate the individual change you've done to Ocif, because at that moment, I'm no longer doing, once the documents are loaded, I'm no longer doing like direct, here's the entire file, I need like deltas.

Oh yeah, you're doing patches.

Right, so every shape that you create or move or adjust, which actually I can show you why that like how that currently doesn't work. If I think if I try and make a make a rectangle while Excala draws open, yeah, it will be like this, and then because of just my bad code, really.

Oh yeah, there's another great one is that you have like a plain rectangle in TL draw in dark mode, and it's not got a white border. It's, I don't know if I could ever make this work with the current like what we have today, of like I'm looking at Excala draw in light mode and TL dark mode, like I don't know how to make that stable, other than just deciding that there is a subset of Ocif, like maybe even storing a palette inside inside the document somewhere, like it's a separate schema that I've added, like in just storing, this is the palette, and this is what we agree on. There are 12 colors, and if you need a color, you look it up from here, like that's the, so that I can have some kind of named color system if I need one.

Okay, interesting. Max, go ahead, do any questions or?

No, I think we desperately need some more metadata at the canvas level. We stumbled a little bit on that when we drafted the transforms, so yes, the transforms they apply to the parent. If there is no parent given, it applies to the canvas itself, which you cannot configure, but it has some defaults built in. So I think we need something like the canvas node, which is representing the canvas itself, so it has no border, but the color and font settings and whatever else of that canvas node applies to the canvas itself, so that you can set a canvas background, and then maybe even attach more data, like you give the palette extension to the canvas node, and then the palette extension applies to all nodes recursively if needed, so you can have different palettes and different nodes if you need to, but usually you only have one palette at the top node, so if we would have a palette, no, a canvas node, a root node, then our extension system could help us with all the other issues.

Yeah, so I think we need something like a root, or maybe the canvas itself is that root element already, and you can have a data object there and all the usual node properties, but maybe one container more is better.

I like that a lot, especially if you can then, like there can be an agreed upon extension between TL, John Excali, draw that something is a, like has a theme, for instance, right? They could have that as an extension, like darkness is a thing, and then when you load it in, what they should do is switch the canvas to whatever theme it is that's configured in that theme extension, and that could be something that they just specify and they both use, and you've got your palette.

I also really like the idea that for, like in the world of a native OKEF editor, you can like have a rectangle that inside there, you just have a completely different palette. If you need to, I mean, we're a container from it, and I always think about canvases being included in canvases. So if we import a canvas that has its own settings, we need to be able to encode that anyway, so we can also just apply to every node.

Yeah. Oh, yeah, I really like this. We give us opportunity to store the viewport information as well. We discussed, like, TL Draw, it like actually does save out the viewport information so that when you open the canvas, you're looking at a specific spot. That could be an extension. It doesn't have to be. But we would have the thing to extend, which is the canvas node, right? Whereas currently, if we create a viewport extension, it's like, well, what do you extend? Like is that?

Yeah, it's like, so the, the, the absolute simplest way to extend the current spec to have a root node is to have one property root node or canvas node. That is it the ID of the canvas node. And that's it. Or just the canvas node object itself, given there.

Yeah, we could be the object. It could be an ID like you pointed out. The other, the other case that it seems like it's important to handle if we're tackling this one is the case where multiple canvases are included in a single infinite canvas. There's a couple of different pretty common cases here.

So one is, uh, TL Draw itself has pages. Those are just multiple infinite canvases that are all bundled into a single TL Draw file. And so we will, we would end up at a place very quickly where we tried to do a TL Draw to Oakiff conversion. And because we don't support the concept of pages, we drop all the other pages and just convert the first one, I guess. Or we, or we spit out, we emit multiple Oakiff files, like depending on how many pages there are, like there's some not great solutions, but there are solutions.

The other case, though, is where you have canvases that support nested canvases. We've talked about using like groups to handle this. But the reality is, is that for some of these nested canvas tools, like Muse, for example, every canvas is a legit canvas all to itself. And like when you zoom into a new canvas, you have all of the canvas affordances, including an infinite nature where like you can, and like, I don't know that our groups actually handle that, that concept, because they're, they're sort of bounded in XY space. So they're not truly infinite.

No, no, they are, they're just bounded on the outside, but they're infinite on the inside.

That is true. They are infinite on the inside. So anyway, if we added, should we handle multiple canvases in the same way? Should we handle multiple pages in the same way? These all sort of rhyme. Multiple pages could just be note. So we have a root note, and it contains five page notes. They're just normal notes, but they use the page extension. So if there is a canvas importing them, supporting pages, it knows how this is a page. We don't render these as items, we render these as the outline on the side, and so on. But if you just import it to another tool that doesn't know about pages, you just have five items, and you can zoom in and see what's in there, and that's it. So you don't need to have special pages support in order to view pages.

That's really interesting. That's just another view on items, isn't it?

That's fascinating. I'd have to think about that. So I could open like a multi-page TL draw and an Excalidraw, a single Excalidraw portal. And now you have been nice. Why not? Why not?

I bet she could tell us why not. My solution and my original TL draw thing in Little Book, the original one I had done that was doing it to a TL draw file. My solution to the page's problem was to disable the pages toolbar. It's just I got none of my business right now.

And maybe that's also fine, but if the TL draw exporter decides it wants to keep its pages all in one file, then we can say I put it in items and tell these items they have a page extension. And if you just want to export a single page, add a second option, export one page to OCIF. That's up to TL draw. And then we have a file that has a hierarchy or just one page.

That would work. How would we define the relations between the child's notes on the page or on the canvas with a parent-child relation extension? Just a group. They're just five blocks on the top-level canvas. They have a page extension which usually we don't know how to render and inside they have other items.

And they are grouped. We don't even need parent-child. But maybe parent-child would be would be useful. So if you delete a page, all items within the page are gone as well.

Yeah, actually now that you said it, I think, parent-child is a good idea.

Yeah, I can imagine that it will be quite a lot of data. If you have one canvas note with notepad notes on them for each.

Yeah, but it's not just JSON. It's just JSON-controlled data, just the resources out there. I mean, it's just storage. It's not much. It's just a little bit of text.

Yeah, sounds like one of the lessons learned here from talk from cheese exploration is focusing around trips with a single canvas is smart. You need to be able to go from let's see, from TL draw to OCIF and back again without changing the, without, and maintain the same OCIF file. And then from there, that's sort of a stable primitive that you can use, that you can use to go implement without, integrate with other ones. Like opening that OCIF file in TL draw and then saving it back out without making any changes should produce the identical OCIF file.

That won't be nice. I think this is a complex goal. For some tools, this might not be possible.

Right. And that would, well, I mean, one of the things this would imply, to give a specific example with TL draw, they have the color map. There's the color mapping problem in TL draw, right? Like the palette is, so like if we, the palette's very limited, so if we, you know, just have like a random hex 2, 3, 4, 5, that is in this OCIF file, when it goes over to TL draw, TL draw is going to match that to like red or something. And then, and then when it exports it, it's going to come back out as red, as opposed to like 0, 1, 2, 3, 4, 5, unless it maintained that 0, 1, 2, 3, 4, 5, and on export, like looked at the node and said, okay, it was originally 0, 1, 2, 3, 4, 5, I mapped it to red. Now I need to turn it back into 0, 1, 2, 3, 4, 5, which seems like a, quite a burden.

Yeah. You, you need to add numbers to the arrows. If you first go from a OCIF to TL draw, then the burden is on TL draw. If you first go from TL draw to OCIF, then that's a different problem.

Yeah, it's, TL draw could, could make a, could have a situation where if it was the creator of the OCIF file, then it's stable. But if it imported an OCIF file made somewhere else, it may not be stable that first time.

Right. Oh, I see what you're saying. Yeah, yeah. So if I had this case, so we start out by exporting a file from TL draw and then re-importing it and then exporting it again. And then we should get a, that's probably a lot of you here for them to keep stable. But if they've improved journal person's tool, they may break at the first, the first time. Like, um, yeah, import is lossy that first time.

We need his lenses. That's interesting.

Yeah, that seems like a easier goal than what I was implying. This is definitely the stronger case.

Yeah, but the first one we cannot do with our TL draw's help. I mean, yeah, yeah, for sure. This we should be able to accomplish.

And I shouldn't move this arrow so that it's like, yeah,

you were saying that, that, um, I guess still it would require TL draw. But if it does do that mapping on read like lenses, like it does the transformation on read. It just keeps storing it as that hex code and then does the transformation on read that allows it to still be stable in this case.

How does, how does this case require TL draw? Not that case doesn't, I mean, the case about, yeah, here's above like, there's a, there's a, if it, if it's doing the transformation on read and never, never touches that hex code. And remembers that that's what it was. And like, in that lenses world, that would require TL draw to do it. But like, it looks at it as the hex code, but at the moment of rendering, it does the transformation. That's a way that it could maintain. So it's like possible, but that is just in this color situation. Like if your canvas contains like, I don't know, a computer, like a Windows 95 virtual machine or something, I don't know. TL draw is probably just going to throw that away.

Yeah, that's the thing from a muse document into TL draw, there's going to be a lot of stuff that I don't know what it does with. Does it just leave it there because it doesn't understand it or does it throw it away?

Right. The, the imperative we've been stating that we've been telling canvas implementers is, please don't throw it away. Please leave it there. And then also potentially use the fallback mechanisms that are associated with that node to display it if you wish. I think the, I think the issue there is like, does that mean that I now expect TL draws sync engine to let me sync an entire like ISO containing Windows 95? If I've stuck that in my, in my Oka file as an extension for virtual machines.

I mean, yes, people, yes, thank you Max.

Simple class.

Yeah, exactly. People will do anything to transmit wears cheap.

This is how this is the new vector for distributing.

Yeah. So there's canvas nodes, we kind of talked about that a little bit. The color mapping one is interesting. This kind of explores the problem with color mapping. And, but it feels like there should pop, and then you were saying Max, that maybe we have a palette extension. There was cheese ID idea. And I think it's a good idea. I mean, to store the palette in the file. So in our parlance, that would be a palette extension.

Yes. And probably the palette extension would have a set of named colors and then somehow a range of which colors map to these things colors. I don't know how to define color intervals, but we will find a way. I think I think the dark mode and light mode is more brain twisting to figure out what exactly is it that we actually want.

I agree. I was going to recommend we move to that one too. Let's fix it.

Keeping it in if you have something like HSL or LCH or whatever, where you can be like this set of like this set of degrees at these dark these darknesses and lightnesses. I like that. That's quite neat.

Yeah. But for dark mode, what do we really want? I mean, right now, if I mnt draw in dark mode and I exported things are dark. So if I import it again into another tool that has no notion of themes, it should be dark because that's what was what I exported.

But if I now have a second tool that is dark mode, light mode theme aware, that would be nice to transmit that over. But what does it actually mean to be light and dark mode aware? So every color that's stored secretly has two values and they need to both be transmitted along. Is that maybe the essence of dark mode, light mode and then a global toggle, which mode was activated on save? If your palette has named colors, like if that's the way we're going with the palette extension, then dark mode, light mode is like a it's just a boolean at that point, right? Because red, based on what the dark mode, light mode was, you would decide what red meant. So every palette entry has two colors.

I don't think it would.

Yeah, suppose like if you're doing on the on the reading, yeah. Yeah, suppose it would need it, it would need like both ranges because the light is as dark as the dark red on light mode.

Yeah.

And what happens for tool that is dark mode, light mode aware, but not using any kind of palette. So the user is just loading it in dark mode, painting things blue and green, saving it, opening it in teardraw.

So I think the light mode green webs to in teardraw, which is now in dark mode because it's not.

It's not so easy to define even the user expectations, that's what I mean.

Yep, right. Oh goodness. So if we had a

Oh, let's say rectangle has colors. Yeah, rectangles have colors and she has pointed out how wonderful rectangles are. So let's talk about those. So yeah, if we had a stroke color and a fill color here, currently like our oak of color type only supports like hex colors, a single hex color. So geez, I, yeah, I've part of me wants to try and handle this with extensions where like, but it would be so noisy.

Like if you, if there was a dark mode or a whatever we would call it, like dark mode, light mode extension or whatever, basically you would be extending every node that have color attributes on it.

Oh, and you and like, how would you separately extend stroke and fill because they could have different. So assuming that there are no named colors, right, that like this canvas knows that the stroke color for this rectangle in dark mode is a particular color. And then when you export in light mode, it's a different color. You basically want to store both of those on the rectangle so that a dark mode light mode aware canvas bringing it in knows what the two hex modes are hex colors are to toggle between, but how to store those. I don't know.

In an extension, of course, and the extension has two properties dark and light and within them, we have stroke stroke color and fill color.

So we have, so we do the same, we read at redundancy, we have the normal stroke color and fill color for the dump tools. And those that understand the extension can look up which color to choose for light mode. This is stroke color, this filter offer dark mode, this is stroke and color, fill color.

Yeah. And that would work. It's similar to how we use coordinates if we have no transforms. We have global coordinates everywhere and sometimes we deliver the recipe how to calculate them if you if you can do transforms. And now we would, if you're safe in dark mode, the colors in the main rectangle are those of the dark mode. But additionally, in the extension, we put both colors again, the dark mode color and the light mode color. That's at least the one proposal.

Is it possible to do it with a separate light mode dark mode theme and do it and have the palettes extension be like named? I'm just imagining a third canvas tool that isn't a scaly draw or TL draw, but it has like more themes. Like if it has a it has themes that aren't dark, it also has like a, you know, a cute theme which makes everything sort of pinkish and purplish, but it's still the same, it stores underneath is the same palettes and it's current thing. So could it just be that the palettes are like just named and something like TL draw an ex scaly draw could have a an ad hoc understanding that dark and light are their dark and light ones and anything they don't understand. So like the nature of falling back, if someone selected the cute theme and they fall back to like the light theme, that same nature is the nature in which like a a tool that does not understand things would fall back to one of the palettes, like that that falling back is something that's defined but generic.

I think you bring up a good point that we can extend the dark light mode idea also to themes, but I think that's also going to named colors, which is yet another concept to maybe have or maybe not have.

Right. Yeah, we should handle, we should try to figure out how to handle canvases that have no named colors first, and then we need to handle named colors additionally.

Yeah, I think so. Okay, so here's an example, right. We have a data, I need it, I'm sorry, I need it. What's the theme? Is it called SEMA? Is that this would be at okay slash node slash dark mode or like, what's the general term for type? I have to need to say theme. Something.

And it's not SEMA, it's type in our. Thank you. Thank you. And I would wrap right here. I would suggest too, to wrap the colors differently, so to have a theme called dark or cute, and within that theme, we define the colors.

Yeah, because then you can have as many things you want. Yeah. And you can decide to override a color or not.

And is this stroke and fill? Oh, it was stroke color and fill color just above you can see.

I missed the joke. Sorry. Just a few lines up. You see, we use stroke color and fill color. Just the same.

Gotcha. Yeah, perfect. Got it. Okay. Yeah, maybe at the third theme, cute, just to keep the idea of other named themes alive. So we have dark light and cute, funny, gray.

What kind of editor instead of inside of the mode inside of TL draw? Like, come on. And do that a little bit. They do it. You can do it a little book because you can.

Thank you. Might be my one thing that gives me a switch feature that I need the most.

It says that it's a that it's a TL draw file with a rectangle in it with text in it and then just make that a code mirror editor with the them plugin.

There you go.

Yeah, this is exactly how I think of the simple possible theme extension would look like.

Okay. And then the question is how to actually choose a theme instead of just defining it.

Oh, yeah. How do you indicate which theme is currently active? Is that a canvas node thing again? Like, yeah. Where are they? Let's see.

And we've got this new canvas node thing that we haven't even defined yet.

Well, stop interesting. So it would have a data portion that contains a type. Yeah. So what is the theme defining extension and one that they make selecting extension?

Yeah. So type of node select theme or something, right? Or something. And that canvas nodes shouldn't be inside the nodes.

Maybe we should just have the the ID of the yeah, the canvas node up there. I got you.

Yep. Yeah. This looks more familiar. Yeah. All we can just have a magic ID for the canvas node.

Yeah. My mentors taught me no magic strings. No, I may be better not.

All right. So then here's an interesting. I'm totally a masochist typing all this code inside of TL draw, but a mad man. What am I doing?

Yeah. But there's an option or selected theme. And we can name these things better. But yeah, that would be cool.

One worry that I have maybe it's an irrational worry, but like, our is stroke color and fill color really it? Like that's like there's never ever going to be any other kind of color. We're not going to color anything else. Because I don't know. That feels weird. Isn't there also text color? Like how would we handle text color, for example?

In the last minute, we defined the text extension to look at it.

Yeah, it was zero to five. The text I know. Text style. That's right. It is itself an extension, right?

Yeah.

Yeah, it's a note extension. And it has a color.

That's yeah, I think that's what I'm worried about is how would we extend the color of extensions with an extension that can't know about extensions.

Like yeah, like yikes.

So I want to be able to come along and make make a shadow extension. And I want to be able to configure the color of that with my theme.

Yeah, that is sensible. So maybe there's a maybe there's a generic color here that we use and then like the understanding for extensions is you can pick up from the theme a color and decide what to do with it and apply it as you see fit. And there's also strokes and fills.

Interestingly, I think this is what it's called in CSS, right? Text, you're coloring the text in in an HTML element. And just color. I took the names from HTML and CSS as far as possible.

Yeah.

That's not a bad thing. Make it fair a lot of HTML and CSS.

Yeah. So we basically have, I mean, this is this feels like SVG to me.

The other feels like HTML and CSS. And then yeah, kind of from beyond there, it's up to you.

Yeah. If you want to have, I guess if you wanted to have a very robust set of colors for your object that go beyond color, stroke and fill, you should probably manage the themes yourself in your own extension. There's nothing stopping you from doing that, right? Like of like, yeah, create an extension and you can like make your colors as arbitrarily complex as you would like. No one else will see them. No one else will see them except for you.

Well, technically on export, you can export an SVG fallback or an image fallback. You can render an image fallback of those things. No one else will be able to edit them, but they can maybe see them.

Cool.

Okay. Let's see. We've got 10 minutes left and we haven't even talked through all these problems.

All right.

Let's just add another problem as well, which is just the background.

Like, I don't know if it's something you want to capture in OKF, but like the background, it's but there's fill color, right? But T L drawn Excali draw both have like four types of background. They're also both completely different, but there's the hat, like the.

Oh, they have a background pattern.

Yeah. Yeah. I don't know.

Yeah. It's, uh, it's this. Sorry. For those you're watching and maybe not super familiar with, um, Excali and then Excali has its own. That's like, right? Like my mind and then like cross hatched.

Right. So I think this is the obvious case for a like at T L draw slash rectangle. Slash node slash rectangle. Where you ignore those additional these additional things.

Yeah. Max, you agree or no? You look questionable.

So do we have a pattern background? This is a common vector drawing thing.

We can just have an extension for that.

Oh, OK, I see. So, so he would have like a pattern. Background or BG or something. Extension.

The reason that I shy away from that is because all apps handle patterns in their backgrounds so differently from each other. It's rarely the same. And so I would look into HTML, CSS and SVG, what they have in that area.

Maybe maybe there's some common crowd. That's a reasonable thing.

Nothing I can think of in CSS.

He just has a background property, which can be an image, which can you can repeat? And it's gradient. And maybe this isn't that's true.

Repeating linear gradient is a way of doing like doing stroke lines, for instance, or like that.

Yeah. I think it's a reasonable thing to consider. I think also it's. I think we're. I'm pretty sure that cheese exploration has revealed that both. This would be OK, sorry, that both TL draw and. Excali draw are going to require a custom. Extension just for rectangle to store things that are specific to that canvas's rectangle. And try to map everything onto. Okay, rectangle that we can support, but then just for everything that can't be handled, it just has to go in an extension. And that can at least get us to this case, right? Where we export where TL draw exports and OK file, we re-import it and re-export it and we're stable.

Yeah, and if they publish this this TL draw rectangle, then like Excali draw can also try and map that into it internally. If it feels like it, and then you can with their involvement, get to the top case, like they can get they can get us there.

Yes, I was going to say the same thing. It's it's like I should have like you said it seems. That's such a great. I'm excited about it too. Like I think I think that's I think that's the best way we can support any of these canvases is like if you want to go above and beyond and like read read into like add additional implementation to map from other extensions onto your file for a map and go for it.

But I think we're going to need those Excali draw. Let's see.

All right, backgrounds, patterns. Thank you for bringing that up. The other one we haven't talked about is rotation. I think this one's handled already. However, origin, I guess.

We we do in the transform extension. We like

I think origin is not configurable in our spec. Not configurable.

Yeah, that's what we're going to say.

Oh, is this new? Yes, this is from this is in five. This is in zero five.

Okay, great. My my information is out of date. You may have noticed a new file that was new open canvas not point four.

So yeah, we always rotate around and I guess, unless I think it is.

Yeah, it is always around top left. But what I was going to say, cheese, this is going to make things complicated for every time you rotate in TL draw, it's going to want to like you're going to have like recalculate the rotation around the top left because the patch is going to be wrong.

Yeah, patch is going to say rotate around the the middle. And you're going to have to say, Nope, rotate around the top, like recalculate the orientation based on the rotation around the top left, which is actually going to be a move, right? It's going to be.

It's funny because I knew that you'll draw has this code, like I know that Neil and it's like, I want that. But can you just give me the inverse of the code that you already run? Because it stores the things with the correct rotation, like around the correct point. But then it does magic while you're rotating. And it's like get any of the inverse operation.

Well, give a try. I hear it's great. Maybe just ask a little to add it.

Hey, yeah, I suppose this. Yeah, that'd be great. But I think I pretty sure rotation's handled. If that doesn't do it, she'd be curious to hear is like, transforms is new. Maybe it doesn't support personally, Aaron is who's very big into 3D engines and that kind of stuff help us design transforms to work with like good old and game engines. So I feel pretty confident that it'll work for you.

Yeah, it should work for TL draw if it does. If it works, we're good. But it might be a cause of instability, do you know, numerical precision?

That's true. We could have a different idea of putting one guy. It's going to jitter. I'm almost certain it's going to jitter.

You're doing it if you're doing it live and you're treating Oakiff as the this actually brings up a problem for people who are thinking that they want to do Oakiff as a container format. There's something CSS has like in its spec that like only three decimal places exist. It's in this spec. I think it's three. It's like it literally has it in this spec like there is no more precision than this. That's that's apparently you know what I'm with.

It's called float three. There are only three decimal places. This is what we support.

Okay, we only have a few minutes left. I wanted to quickly show slides that I showed not that not because I think my slides are great or anything. But but I know that y'all were asking about it. And so those of you who didn't get to be in the room like she and I, here's what here's what I showed.

Okay, sure.

Thankfully, we do not have time to go through the entire presentation.

Hoorah, because I wouldn't want to do that to you anyway. But I basically I showed a demo of the whole talk was about export and file sorting supporting common formats and why that is important for local first software systems. Like that it aligns with the ideals of local first software and supports them fully. And so in I kind of increased the complexity of the export over time. And in the final demo, well, not the final final demo, but the level three demo was basically what she showed with Excaladron tail draw, except we showed the one that Michael built with tail draw and city and canvas. So I showed that demo here and then basically said, all right, well, how does this actually work?

At this point, I had not introduced Oakiff yet. I mentioned earlier in the talk that that Jason canvas that obsidian had released a thing called Jason canvas. And so I was like, is my question in the talk track was, is tail draw adding support for Jason canvas? Like, how does this work? Because obsidian is on one side and tail draws on the other. Is Jason canvas the container in the middle? And then I showed this slide and I said, you know, when they released Jason canvas last year, Orion pointed out that it doesn't really do everything we want it to do. And so he proposed creating a working group for minimal open interoperable formats for canvases. I said that sounds like a great idea. And that was the OCWG was born.

And then this is actually a picture from last year's local first comp where Orion and I were writing the first draft of the spec. You can actually kind of zoom in and see like that that data structure looks awfully familiar, doesn't it? That is the very first draft.

And then yeah, one year later at local first comp again announcing and it's funny. I forgot to retake the screenshot was 0.5. But Oakiff is now at candidate recommendation stage. And what that means is that we feel like the spec covers most of the technical meets the technical requirements that we set out to accomplish. But we need more feedback from people who are implementing it.

I mentioned that there's been a lot of work. I think we had 26 meetings over the course of the previous year. A lot of people giving input from different canvases, multiple versions of the spec, several new collaborators, and several canvas implementations of Oakiff. And now we feel pretty good about it.

So then to answer the question I asked, how did that demo work? Well, there was an Oakiff file at the center of those two demos. So Oakiff was converting back and forth between TL draw and Obsidian canvas. And then the final demo that I showed was that humans aren't the only readers. LLMs are good at open formats. And so I showed Michaels generated a-- I think I did the three branches of government of the US government and the different-- build a graph of the three branches of the US government and the people who are in charge of each of the branches and show it generated a little graph of that. There we go. Come kick the tires.

And then on the final slide there was a big QR code for spec.canvasprotocol.org. So that's it. And then in the Q&A, you ruined the rest of my night.

Well, somebody asked like, they were like, well, files are great. But wouldn't we want something like a CRDT or something to be able to-- and I pointed at Chee and I said, Chee solved that already. You should go talk to Chee. I said, Chee, raise your hand. She foolishly did. It was incredible. It's the power of the person from the stage calling upon you. I'm sure if I'd been like, you're a PRT. Absolutely. In the moment.

But yeah, then you had a bunch of people coming up and talking to you about it.

Yeah, it was great. It was great. Very cool.

Nice. Well, we're at just after one o'clock. I need to head out. I will post this TL draw sketch to Discord as well as post the recording as soon as it's available.

And then Michael, maybe you can crank it through your transcript generator and summary generator.

See, that sounds like we have a few things to work on.

So--

Yeah, exactly.

By the way, the person-- Thank you. I really appreciate it.

Of course. The person who asked that question, by the way, was like somebody who worked on IPFS, the turndyte, which it all started to make sense. Right?

Yes, indeed.

Was it Brendan, my way? It was Warpfork. I don't know.

Yeah. Yeah, I ended up talking to him as well.

Very cool.

All right, y'all. I'll see you in two weeks, if not sooner.

Yeah, I love it too.