# Meeting 6 Transcript

June 25, 2024

All right. Hello, folks, and welcome to OCWG meeting number six. I'll go ahead and share my screen real quick. So, yeah, we're working on reviewing the spec has been something we've been working towards and some folks have done some implementation on it.

So, if you're watching this recording and you don't know anything about OCWG, then you can head to our website, which is protocol.org. And that has links to all the relevant things, but all the goodness really is in GitHub. There is a discord where you can chat with people who are working on this stuff, but we encourage you to go to the GitHub discussions. You can find those at github.com/OCWG. And then the spec that we'll be discussing today is at github.com/OCWG/spec. 

And I'm looking around and I know all of you and therefore introductions are irrelevant. So we can skip right over that and jump right to the proposed agenda. So definitely want to honor Steve's and Orion's work in putting together a demo for today and let them go first. So that's why they're at the top of this agenda.

But I was just as I was lamenting the fact that I can't automatically break a text box into multiple lines and TL draw. I did it manually. So feel free to like, if you want to reorder the agenda, feel free to do that or vote on something that we want to talk about today. I put one thing at the top that I want to talk about right after the demos, but we'll let the folks demo first and then we'll dig into some of these discussions. We probably won't even have a chance to get through all of this today. There's a lot of progress happening on the spec and some some gnarly open problems to work on. 

So all right, Orion or Steve Orion, I'm going to give you the prerogative to go first if you want. Unless you're saying I need like two more minutes in which case Steve can go first. What do you think I can do? 

I can do 15 15 seconds. I've just tried to add a note, which I want to just write down before I forget it. 

No worries. No worries. That sounds good. This would be the part of the show where the guy with the guitar does like an ad-lib and tells a joke and you know, as the next guy is getting set up. 

Yeah, if I don't know how much y'all have like dug through the discussions recently, but I spent a bunch of time in there over the last couple of weeks and there's a lot of a lot of good stuff. I actually haven't looked over the weekend to see if there's more stuff since the weekend. But yeah, really appreciate all the stuff going through. And there's still a couple that I have left to respond to, specifically one max where you addressed. So a few things that I haven't yet responded to on the non visual nodes stuff. So there was a couple things in there that jumped out to me. So I'll get to that. But it's coming along. I guess I can do that as well. 

I think you're a host right now. Oh, yeah, I got to do that every single time. And all right, it is enabled. Take it away, friend. 

Are we in? Yep. All right. So I haven't got a much of a demo. I was hoping to have arrows working and finish up the round trip part of this. But I got really hung up on the Excalibur side of programmatically dealing with arrows specifically. So I'm going to have to reach out and figure that one out. But I think it's already exciting that we can take a rectangle and have it, you know, in TL draw on the left Excalidraw on the right. And we can take a bit of text. And that's gonna, you know, the these kind of bounding boxes are gonna roughly, roughly line up. Wow, at least their origins, origin points, like they're gonna line up. 

So yeah, I'm pretty, pretty excited about this. We can start messing around. One thing which has so far stumped me on the Excalidraw side, which is something very basic. But like if I make a little rectangle over here, right, and this is the origin point in TL draw. But if I rotate this shape, Excalidraw seems to want to rotate it around the bottom right corner. And I, I have no idea why that's happening. I need to go back and look closer at the, at the, the spec. 

And this, can you do the edits on the Excalidraw side? Or is it just one way right now? It's one way right this second, I got that working. And then I, and then I broke it, you can, you can see that I, it's gonna deselect every time it updates, which is currently very often. So I need to change a bit of behavior there. But they are both reading and writing to the same, same file. 

And wish I had a soundboard to give you a clapping sound. That's awesome. Or send with effects. 

It is exciting. And it is, I will say, especially for building out integrations with this spec, I think actually that having environments like this, where it can be done in real time, are actually going to be really important, right? It's not the, it's not that we want to prioritize like real time multiplayer. But it's, it's actually that that is kind of necessary to debug this. If like, if I had to open and open a file every time I made a change to see if it worked, that would be a nightmare for development. Whereas here is just going to read every 50 milliseconds or whatever it is, or, or wait for the server to, the server that wraps around the files and notify that that has changed. Yeah, fun stuff. I'm really looking forward to expanding on this now that we have. 

Steve has a question. Yes, your demo is going to be way ahead of mine. But my question is for the real time stuff, how are you checking what changed? Are you doing it manually? Or is there some kind of, how do you know what is being updated? 

I don't currently. And I assume that everything, I refresh the entire canvas whenever anything is changing. And on the hardware side, that's just every 50 milliseconds, because I don't, I don't really know how to do that differently there. But hopefully soon on both sides, it'll just be whenever the actual file changes. 

Yeah. Another thing we were talking about showing here is basically having like a third panel. So imagine, you can imagine Excalidraw, TL draw, and having a third panel that actually shows the render, the JSON of the OCWG export. Yeah. That's here. I wonder if I can. Oh, pretty print it. Yeah. Yeah. The format JSON is the usually the thing. Yeah. Yeah, I can do that. But the problem is public. Man shift format. Yeah. The second option should do it on that list. Oh, you have to save it as a JSON file. Yeah. But well, I, this won't be live updating, but you can at least, at least just show you what this looks like. Oh, now it knows. 

There we go. So it's just this right now. We have IDs, schema string, X, Y, and then a properties bag. And we just have that for, for text and rectangles right now. And then there's, there's no relationships at all in this, in this particular case. 

Very cool. Yeah. I agree. A third panel for also for kind of live debugging, but it's going to stream updates there and keep it formatted. I think that'll be ready. Yeah. I think that's one thing we can probably use the Canvas protocol website for two of having this a live deployed web app that people can go play with and then just have a big button in the top right of like go to the GitHub and fork this yourself if you want, or like load a stack blitz with this exact repo in it. If you want to mess with it, that could be a great way. I think that's one of the things that TL Draw has demonstrated so beautifully as a company is that this problem space lends itself so well to visual explanations of what's happening. And so yeah, pretty neat. 

What I would love to do for both TL Draw and Excal Draw is something that I've, is, is like be able to do this kind of stuff more easily. So like this is a shape and be able to in Excal Draw, in TL Draw, pipe out not just their insides, but like the kind of OCWG version of that. So the people that are working in either of these worlds can quite easily get to like, oh, let me just like, so, you know, it would just be something like, yeah, JSON Stregify, you know, you just slap on OCWG function in there somewhere. And then all of a sudden this is not TL Draw schema, it's like the mapping to OCWG and gives something to copy and paste. I think that would be, I think that'd be great. 

Yeah, that's pretty awesome. The other, the other tool that's related to this that we talked about was potentially having a browser extension that does, that can sit on top of any individual canvas that, at least a canvas that exposes its underlying data representation. So the TL Draw exposes the entire data representation on the window object. So a browser extension can read the window object and then convert that to OCWG. So you could imagine a browser extension that opens a separate panel and, and it doesn't do any round tripping to another tool, but it's a much simpler tool that just gives you the OCWG inspected version of any individual canvas. And you could have easily have like a save to file, save, you know,

 save this to disk or export to disk or whatever, or potentially even a load from disk that would load an OCWG file and overwrite the TL Draw that you're currently looking at with that OCWG. So another, another slightly different tool that I think would help a lot with debugging and developing these things. 

So Steve, you want to show what you've got so far? 

Sure. Let me share my screen. I did make a mistake. I should never make anyone follow Orion on a demo. He should always be last. Let's see if this works. All right. It says I'm sharing my screen now. Yep. And let's see if I can, I can't switch tabs because it's overlapping, but I'm just going to click here again. All right. So when you click on my link, you get this stacklets, which is kind of like a souped up code pen that I've been using. And then you can see some, I only spent about half an hour on this just to see as a proof of concept. Because this is going to be the first step to getting a third column on Orion stuff is the export and import. And it's just taking a moment to run here. I don't know why. There it is. So the first thing you have to do is make the window larger. I put a warning there. So here we have this output in OCWD format on one side and a drawing tool on the other. So as I click, and I think my computer is really slowed down or something as a result of screen sharing. All right. Now it's working. So here I'm just drawing stuff and the clicks aren't very responsive for some reason. Probably because of screen sharing and I'm using Ubuntu, some interaction there. But here is the output. And we can see this is a brush stroke. And one problem I had was I don't really know what a brush stroke should look at, look like with the schemas. And so it's just putting the raw properties in Zwiebler format. And other tools would not know what to do with these. So the next step would be to translate them. Once I know exactly what they should look like. And it occurs to me that that rotation problem is going to be the first of many problems. Because when you have rotate, what does that mean? Is it around the canvas origin? Is it around the shape center? Is it around one of the corners? And that is just something that has to be specified. I have a matrix. And that's what I would be translating to your rotation. Why can't I click? Oh, there it is. Here's a circle. Rectangles. I have that clicking problem. But that's essentially it. And the export code from my format from my tool is pretty simple. But it's got to be filled in. It's just getting a list of all the nodes, finding out their x, y coordinates and getting their raw properties. And over here is going to be a lot of code to translate it into whatever format we decide on, translating it into the schema. And I'm going to be looking at Orion's code if it's available to see what that schema should be. And that's all I have. Go ahead, Orion. 

Yeah, just one thing that I wanted to mention here for maybe a future discussion. Is something I'd never considered is the option of actually defining the origin on the shapes themselves with something like a matrix or whatever representation we end up using. So I wonder if it would put the owners of doing that translation on the clients to go from top left corner to center origin points, that kind of thing. I'm not advocating or kind of suggesting that that's a good idea, but it was just something that I had never crossed my mind until just now. 

Yeah, I think one of the things we need to think about is does rotation origin need to be a ideally rotation origin would be something we could assume without having to specify it for every object. And then canvases would know what the assumed rotation origin is and would do the translation themselves. I think that's a simpler way to handle it, but maybe I'm missing some of the vagaries there. 

Max, were you going to talk about the rotation origin? Yeah, exactly. The rotation should be defined in the spec. I mean, if we say the rectangle is rotated, what do we mean by that? But the rotation origin doesn't need to be exchanged across quotes. That doesn't serve any purpose. 

Agreed. Yeah, that seems like I can't think of any edge cases where that's a problem right now. My mind immediately went to shapes that are irregular and calculating their center point is actually be somewhat challenging. And then if we go with top left, top left is like, okay, so what is top left either? Is it the the furthest, the largest x value and the smallest y value and it's the go perpendicular from there to that. Is that top left for irregular shapes? 

CSS has solved these problems. They have a similar thing in their transformations. We could probably look at that as a basis. 

Good point. I'll put it on our growing list of open problems. Something to go look at. Yeah, you're right. There are other tools that have certainly solved this. The thing is, yeah, we're trying to strike this delicate balance, right, of being between two low level, like all the way down to the level of like an SVG, where there's no there's no notion of rotating an SVG. It's just it actually changes all of the points in the, well, actually, that's not true. Rotation is a thing in SVG as well. So, I need to think. Adding this to the, yeah. 

All right. Well, let's jump back over to, I'm going to share my screen. Let me jump back to this and we can throw them. That's by rotation.origin. All right. I'm going to push this down. 

So, the main thing that I wanted to talk about from an agenda perspective is, I think, Max, I think this was your suggestion to have multiple schemas per object, if I'm remembering correctly. I think we need that in order to support better run tripping. 

Yeah. And that was actually what Orion was hoping to demonstrate today and got close to demonstrating was arrows in TL draw and Excalidraw are slightly different from one another. And so demonstrating the ability to have a sort of base arrow, well, have an arrow. It's like an inheritance tree. Kind of, you'd have like an OCWG arrow. And then a field draw arrow and Excalidraw arrow, which would both inherit from the OCWG arrow. And so what he was hoping to demonstrate today was, and this will be like an important thing to figure out when round tripping, is you create an arrow in TL draw. That has some parameters that Excalidraw doesn't understand, but it can at least display it because TL draw inherits from OCWG. TL draw inherits from OCWG arrow. So it can display the things that it understands. 

Then you edit that arrow and Excalidraw. That adds some properties that TL draw does not understand. And so then how do you represent, and this was Max's point, you need both of these property bags, the TL draw arrow and the Excalidraw arrow property bag to fully represent this one arrow because it's been edited by both canvases. And then the important thing that we've talked about over and over again is each canvas then needs to respect the property bags. It does not understand and preserve them when writing the file back out. 

And unfortunately, you can still run into a bit weird problem. So you have your arrow in Excalidraw. And let's say the label is something really special in Excalidraw. You change it in Excalidraw. So now it has a different label, but TL draw doesn't understand, it puts the label in a very different way. So now whoever sees it sees it with a different label. And in reality, it will not be labeled, but it might be the background texture or whatnot. But it will sort of not be the same. 

So some properties may semantically contradict each other. And this is, I have no idea how to solve that. 

Honestly, I'm unsure that that is a solvable problem, kind of agree. Probably not solvable. And that is probably okay for given the purposes of this particular this particular project is we know that we know it's not going to be exactly the visual fidelity between the two. There will be visual fidelity and even meaning at times that's lost between the two. 

I think what it would probably require in that specific case would be the TL draw and Excalidraw, that whoever is the author of these two schemas to kind of talk and say, Hey, I mean this with this thing, is there any way that we can kind of can we can we move it up to CWG arrow would be would be a good question. And that would and that's that's another reason why I'm glad that we're versioning these specs. So this could be, you know, in the 1.1 spec, it takes those two parameters from Excalidraw arrow and TL draw arrow and they agree to use the parent spec. 

And given that we're using like a hierarchy, I don't know how far we want to go with this, but we could even there could be a case where pushing it all the way into arrow doesn't make sense. But there's like a sort of TL draw plus Excalidraw arrow that then inherits from this one. And these two guys then agree to inherit from this guy. So they could kind of work together on that one share a property across the two. I don't see any reason why this wouldn't work. It could get pretty complicated, but all of the we probably need to recursively resolve all of the specs to build up the property bag. 

So cool. And I think that one made sense. That was a really good call out Max. And we'll hopefully have a demo that kind of demonstrates

 that working within the next week or so. There's a lot of other stuff on here. I added these things to the list based on the discussions in GitHub. Is there anyone that's like a burning thing that somebody wants to talk about? 

What about the multiple underlying representations? What exactly? 

Oh, that's a good question. I think I meant this. That's a good question. I could talk through some of these if they don't make sense. Oh, yeah, I think let's talk about this real quick. So as we were looking at how to represent, I can't remember how this came up, but we realized that TL draw at least when it exports its schema, it actually exports the current viewport of the person who does the export. So kind of where they are looking on the canvas. And then the TL draw, guys, and Orion in particular has done some messing with that viewport attribute. You can do different projections of that viewport. So you can basically modify the camera in some interesting ways. I'm pretty sure that's not supported by probably most canvases in terms of modifying the projection. But if we store viewport, we're able to pass a canvas to someone and when they open it, it's looking at the thing that we want them to look at. That's basically the advantage here. 

When we talked about it, though, would this be a node or would this be a relation? And the conclusion that Orion tentatively came to is not, neither. This actually is legitimately a third thing. We basically have nodes which are all visual things on the canvas are represented as nodes. This is not a visual thing on the canvas. Then we have relations which basically represent an idea or a conceptual relationship between things that are on the canvas. And this isn't that either. 

You could argue it's a kind of node. It is a kind of visual. This is the rectangle the guy exporting it was looking at. Feel free to zoom to the same rectangle if you like but also zoom out and see still the same rectangle in red if your tool maybe doesn't support it. Just import it as a red rectangle maybe. So this could fit into the node land. I've shifted over the last days in that direction and one of the reasons for that is I think a useful way of thinking about the camera when it comes to sync and its utility is maybe it's more a question of having a reasonably first class schema for bounds. Basically just defining a rectangle with little elves. No rectangle with color or anything like that. You're just saying here's the min x and y, max x and y that they're always going to be in the correct order. It's just a very basic axis aligned bounding box, no rotation or anything like that. 

Because then you can give that some data that's saying like hey, these are the bounds of the current camera view. So if you want to lock yourself to that as you're syncing or when you open a file you can do that but we're not going to treat it as something entirely special. One reason for that is that I think there's a lot of utility and being able to represent just bounds. I am thinking here that these would be nodes even if they are nodes that you might not always want to see. There's a lot of stuff you can do with that from defining where the camera is to multiple views of like here's a region that you should look at for whatever reason. Or future kind of deep linking stuff being able to say hey, open up this canvas file but open it up at this particular location where the location is not like a coordinate or something, it's a bounding box. 

That's a really good point. And I guess in our representation that would be x and y would be min x and min y and then you could either have a width and height or a max x and max y as properties. 

Okay, you're starting to convince me that this could be represented as a node and that that's a reasonable representation. The other thought I had, I don't know how many of you have used 3D modeling software, but in like 3D Studio Max or those kind of different tools, you'll have different camera angles that you're looking at the object on. And very frequently the camera for the different camera angles is actually also visible from the other angles. So the camera is an object in the scene. It just happens to be an object through which you can view the scene at the same time. And that seems like the analog here is that we're basically saying viewports are a type of node. You can have zero to many different viewports and then you can represent kind of like the current viewport or whatever when exporting the canvas. And then more advanced tools could do more advanced things with those viewports, like you mentioned. I was thinking about what was that canvas based tool for presentations, Prezi? Was that a P-R-E-Z-I? That basically allowed you to like set different viewports and they were numbered and you could jump between them for your presentation. And it had a really nice like animate between viewports. That's kind of a cool idea that you could represent those Prezi viewports with this representation as well. 

And you get a unique ID per viewport for free because nodes have an ID. 

Yeah, we inherit all of the other nice stuff, including the bounding box stuff. 

Orion, I'm not sure that I understood what you meant by making bounds more of a first class thing. Are you actually recommending a change to the way that we represent bounds for the base node type? Or are you okay? 

I was saying that it's like in informationally, it's redundant to have one corner of the bounds because x and y are embossed. So you could use x and y to be the min x and min y. Or if you want to be more explicit, you could have the x and y the same as the min x and min y, but then have min x, min y, max x, max y in the properties would be the other thing, which would be... 

Cool. Okay. I think we're still in agreement that the default node type is not going to have bounds associated with it. In other words, it's xy only. And then if you want bounds, that would be down to the schema to figure that out. And I think the use case... 

One use case that I'm actually aware of is the Canopia doesn't have bounds for its text objects. It only has x, y locations, and it relies on the horrors of text wrapping that Max addressed earlier to compute its own size for those text objects. And so we could force it to export bounds, but it seems like there are cases like that where you just want to say it's at this xy location. But most of the... It is likely that most of the schemas will have bounds of information. 

Okay. Great. On to the next thing, unless anybody has anything else to say there. 

We've talked a little bit about asset storage with nine types. I don't have anything more to say there, so I'm going to bump that down. I would like to give us some questions. So typically, if you have such a canvas and you have some external images imported at place somewhere, this image data will not live in the file. That would be too messy to have a base 64 encoded in the JSON. It could do it, but for larger images, it's just ugly. So you probably will export some kind of archive that has files attached to it. But for shorter text nodes, you have them in line. What about a medium-sized markdown document? 

So in Obsidian, they have a distinction between nodes and documents, I think. So you have like both kinds of things. And we could sort of unify it and say, well, we have blocks making up the canvas, and they have positions. And they're different types. They might contain a rectangle. They might contain a file. The file might be in line. The file might be externally. The file might live on the web, but it's all the same mechanism all the time. And then we even have like fallbacks also defined in the same way. Like, here's this thing. It lives on the web. And as a fallback, we have a node at which we cleverly put in the file right here. So if your internet is not there, you can see something. But if we're not clever, we render a different file somewhere else on the web. We can do our local file. So all ways are possible if we kind of make these decisions orthogonal. So we have a node, and the content has a type and a location, which can be inline attached elsewhere. And that would be very flexible. 

Yeah, definitely. I think Orion and I talked about this a little bit when we were in Berlin. And I think, yeah, that we came to basically the same conclusion that we need the ability to basically the... I think we talked about it via the URI. The URI could be a data URI, which would allow for inline. And it could also be a local URI where it's pointing to something that's in the same file directory structure. So that way we can zip it up. Or it could actually be a URL, right? Because URI is a superset of URLs. And that could try to grab something from the web. 

Yes. And then is that similar to what you were recommending, Max? 

Yes, exactly. Maybe except for data URIs. I mean, data URIs are fine and they work, but the hackability of data URIs in a JSON file is kind of meh. So separating the mime type and have another block for the content would make it the easiest to just actually hack in the JSON file as an alternative syntax, so to say. 

I'm not sure I'm following you about what do you mean by URIs? Do URIs are hacky? 

Actually, what you have here is a data URI which doesn't define the mime type. A very conforming data URI would be data colon slash slash image slash jpeg comma the data. And that is exactly what makes

 it a bit unhackable. So editing mark down in that format where line breaks need to be, I don't know what to make. I mean, it's just very cumbersome. 

Got it. But are you just saying it's good that we support a variety of other options? Are you saying... 

Yeah, I would just say you could have a URI and you could also have a content which just takes a plain text string. And if the mime type makes sense to have a plain text content, then maybe there's some precedence of URI or content, what is taken first, but that's about it. 

Yeah, I see. 

Just so that inline markdown is a bit friendlier to the eye and to the editor. 

Yeah. 

I mean, line breaks in JSON is still not so great. 

I actually haven't heard anything there. I'm not aware of what those problems are. 

Yeah, maybe just put them in the file and it's fine. 

Right. They're okay when you have a computer that's doing the work for you, but if you go in and edit a JSON file, it's very easy to mess it up yourself. 

Gotcha. Yeah, that makes sense. And this is... I should have grabbed all of this. This was from a schema that we were roughly calling asset. 

Yeah. And then what is the difference between an asset and a text node? Is it not the same? 

Yeah, I think they would be different like you're mentioning. And then it's going to be up to the... Well, how would they be different? I think they should both be available. And then it's up to the canvas to decide when I'm exporting my text nodes, do I want to use an asset and an inline markdown file or do I want to use text? And I think this is actually a really interesting design challenge for even tools themselves. 

Like, I don't know if anyone has used Muse. That particular tool has some weird differences between text blocks and inline text, like documents versus a single line of text. And then you end up... I mean, what ends up happening is that you end up in this weird space where you were working with a single line of text and you actually want to turn it into a document. And then you hit return. Does that change its type? Like, it's a really interesting UX challenge, but I think we should leave it up to the canvas author to decide which direction they want to go. And the specific reason, right, is we actually... While the data URI method or the content method on the asset is supported, what this is more importantly allowing you to do is to package up a bunch of files alongside it or point to stuff on the internet. 

Okay, but if we have a text node, let's say we have this asset node and our mime type is text plain. And then we have content hello world. How is that any different from a text node saying hello world? I mean, it's both inline. It's both saying hello world. Why do we need two ways to represent the same inline content saying hello world? 

I mean, that's a good question. The location can be different. Like, what you have in your other tools is the location is either inline or external in the file, but we support that switch in the asset here. So the asset can be the same as it doesn't need to be external asset is ambient node. So we can generalize and say every node can have its content defined inline or referenced in a attached file or external file. And then it's just unified. And we still can have the distinction between the inline nodes and the externalized markdown files if we want that. 

Yeah, this has come up before. And I think it's part of what makes asset handling really important to think carefully about is that they're not really the same kind of thing, right? Because it's about like, where stuff is not not what it is in the way that scheme is defined types of nodes. 

But why is it different? It's like, it's not it like, it's not its own kind of shape on the canvas, right? It's you could have a... 

Why not? Why not? Why can I not import an SVG shape and say it's located in the file? It's a very complicated SVG drawing. I'm locating it in my node here at this XY coordinate. 

Sure. What I mean, what I mean is that, you know, you can have images, SVGs, binary files, PDFs, and so on and so on and so on. And it feels like the the the type of thing that they are is is not the fact that their content is being pulled from somewhere else. But it's like the fact that they're a PDF or an image, right? 

Exactly. 

In that sense, asset handling is like, ideally, something that is, you know, robustly kind of handleable by any shape that wants to point to something outside of the the JSON file, right? 

Yeah. 

I think it's what Max is... 

I think what Max is saying, yeah. 

I'm going to point to an endpoint that's going to give me that string or a local file. There's there's considerations that we need to make that. But my question with that is, what does that look like in a way that is like uniform across different shapes, right? Like we would ideally... Yeah, I don't know. Like maybe it's part of the the passing kind of part of the part of the spec of to have some well defined rules there of, you know, if the properties contains a mime type or or rather, like if it contains a URI, say, then we're going to assume that this is pointing to an asset, not try and pass it with like inline data. And so we're going to look for a different property, like, well, I guess the URI or like we would ignore the some local string, and we're going to try and we're going to try and load it. 

I think what... Yeah, I think what Max is saying, if I'm understanding it, and I think you're kind of more or less agreeing with it, Orion, is that instead of having an asset schema at all, we instead have schemas for each of the different kinds of things, because it's the schemas are about kinds. And when you have a kind of a thing, the content, if there's content for that thing, that can be loaded either inline locally or remotely. 

And what we would need in the properties, so this would be an example of a text node. Before we had a text node, I think we had the property called text that had the content and I just changed that to content. So in this case, we we can specify the mime type of the text. And then the content can be there if it's inline, then it's right there in the content file, or the content field. And if it's not if content is not present, then it's going to look it up in the URI. Also, the URI could be a data URI if you want, or it could be a URL, could be a local reference. So if we if we just kind of had this, like, I guess the first thing would be look for content. 

I want to pause that. This kind of gets to part of my question here. I don't think we can get to what we want here with just having like a single, like content property, because that makes this assumption that the that like assets are like one thing, right, which at the and the hard part about that is that it means that we have to have some like universal sense of like, Oh, well, obviously, every like of every shape having exactly one thing that is the asset part. And then the other property is a like normal, right, for like, like, but how do you know that a shape, the one particular property can be also an asset, but all the others are like going to be in that property bag. 

Does does that make sense as a just reverse it? 

I think what we're right in the sitting at is that multiple properties might require binary external content, for example, elsewhere. Oh, okay. And I would like to add, we need multiple contents anyway, in order to have fallback mechanisms. So so we have like two crossing. Yeah, I was thinking about fallback separately. But as an important thing. Okay, so you're basically, so my second proposal is going to be fine, look to see if there's a URI first. And if there's no URI, then go then go grab and this could be grab whatever you need. It doesn't have to be just the content field. It could be many fields, right? And then the expectation would be that URI, the URI would resolve to the same set of fields that this particular schema actually needs. 

But you go ahead. 

Yeah, Max. So what worked great was the web. So you have one resource, you say get, you have some content negotiation, you get the resource, you're under your representation, you understand that you're happy. So that resource can give you different representations. And now we inline all that stuff. So we need an array of representations, maybe ordered by precedence, or they have different MIME types, or maybe they have same MIME types but different locations, whatever, but we have a list of content. 

And every node has one content, like in the web. And if a node for its rendering needs to fetch more digital resources in some specific way, it can do so. We can put that in the property bag and they can resolve 15 URIs if they want to. But by default, one node is one resource, has one content. It's a model that worked great for the web. And gives us something to lean against. 

I mean, I agree with Orion that we could make it more complicated. And there is some reason for that. But then it gets too complicated. Bro simplicity, where we can find the tools and store robots. 

I mean, yeah, I was just about to kind of hack at an idea for multiple things. But I'll finish this thought anyway. I want to think about how the more things we can not do at all, the better. I'm all for that. So let me just kind of flesh this out. 

Yeah, it looks like you were thinking, I got what you were saying. Right. We'll just, you know, make something up here. 

So the idea would be, one approach to this would be, you'd have this kind of reserved property, which if it was important enough for the shape, for asset handling to be universal, which feels like it might be, it would be a reserved property on any shape if they wanted to have something called assets. They'd have to give it a different name. So it'd be part of the very basic schema. 

Or actually, well, okay, I have too many thoughts at the same time here. But the idea here would be if it has assets, it's going to fetch those resources, whether they're local files or something on the web. And then those are going to take priority over the other properties, right? 

So if there was a text field and a text asset, which might be some long essay or something, it's going to prioritize the asset, but it's going to fall back to the local text field, which could be something like a default error message type short string, or it could be the full content for all we know, right? 

But we would just pick an order, which seems to naturally be prioritizing the remote asset and using the others as a fallback. And then of course, you can still get into situations where the fallback is nothing. But this would be one way to go about it, where assets are really just some subset of properties. 

Right. So the assets could also be validated with the same validation as the properties where you say that everything in the assets has to be a valid property. They have to have the same type and so on. 

Can we maybe generalize this asset idea even further and say we have a node and all of its property and content is elsewhere? 

I mean, I find it hard to imagine we have an open canvas format for exporting a canvas to a file. And then, okay, we make the compromise. Some images are really, really large, and there's no point to move them around. They live on the CDN already out there. So we just reference them. But now we generalize it more and more and say, okay, actually, there's no property. We didn't externalize it in the file; we put it into a reference. 

Why is that really required? Can we not mandate to have it here? And then for some use cases, maybe, no, we have an external node and it changes color depending on the day. And we cannot export that. 

Okay, so the node lives on the web and we import the complete node. But do we really then need to have one facet of the node being imported from the web while the other properties from Excalidraw are actually other? 

I mean, it's, sorry, maybe we need that. 

Are you saying that this text could be that any individual property in the properties bag could be either URI or...? 

No, but what Orion said is if we have assets, these assets might also define properties. So for example, the text content might also be one of these externally defined properties loaded from an asset. 

We have no agreed-upon notion of what an asset really is. So that's why it can be different things. 

Well, I would have a MIME type, right, which as we've already pointed out is problematic or whatever that is at the beginning of a URI line. 

Interesting. So we had one discussion in favor of single resource per node. 

Single, yeah, one node is one resource, but one resource has different representations. That's how the web defines it. So we have an array of representations. And each representation has a MIME type and a location where the content is in line in the local files at URI or external URI. 

Max, could I ask you to write up just a really brief GitHub discussion on that? Because I think I can do on that more and we're coming up to the end of our time. It could just be a few sentences of like, I think specifically what would be helpful to me is seeing one of these. And what do you mean by multiple representations? 

I think you're describing something that I understand, but it's not clicking right now. 

I'm pretty sure that Max is referring to like how you can copy-paste something, right? That can have like the JSON, the plain text. 

Yeah, like in emails, the plain text. 

Yeah, yeah. 

Yeah, I understand now. Okay. 

Interesting. I'm struggling to connect with how to implement that with this. But yeah, we're coming to the end of our time. So I want to make sure that we discuss anything else we want to discuss real quick. This definitely bears working out more. 

I'm glad we talked about it. Let's see. 

Looking through the rest of the pieces, what I would say is like Steve, Max, Jen, any of you guys, if any of y'all are interested or anyone watching this recording is interested in tackling one of these open problems or like one of these subjects and just starting a discussion in GitHub about that particular topic. 

It could be as simple as listing out the problems that they can think of when they're trying to represent this or it could be actually specifically proposing this is how I would think we might implement it. Either one would be valuable. 

And when you do drop a discussion in GitHub, it would be helpful if you dropped a link to it in Discord for those of us who are hanging out in Discord because we may not see the GitHub notification in a timely manner and be able to jump in. 

You and me, Jess, we should set up a bot for that. We should put the owners of that notification happening on us, but we also don't want to do it. So we should set up a bot. 

Absolutely. There should be a GitHub channel in the OCWG Discord that has all GitHub happenings that you can join that channel or not if you don't want to see all of those things coming through.

We are at our time, though, so we're looking at the calendar ahead two weeks. There will be, I think, July 9th. There probably will be another meeting July 9th, and we'll kind of continue working our way through this stuff.

So, yeah. Any last-minute questions, comments, stuff to work on?

I would just like to ask Orion to put the code. I just checked the code on the GitHub, and it looks like it's from two months ago. So I would like to see that code.

I'll put those updates either tonight or tomorrow morning.

Thank you.

I'm not sure.

Jen mentioned the Web App.

Yeah, go ahead, Jen.

Yeah, I forked the website, downloaded it, and I'm trying to load in my Canvas file, and I'm finding out that the Web App is pretty hard-coded in. You don't load Canvas files, so it's like we just need a reference Web App to what you see is what you get kind of following the spec.

That's all.

Yeah, definitely. And when you say you forked the website, I assume you mean the JSON Canvas, Obsidian's JSON Canvas website.

Yeah, I thought, wow, look, I can view the code, and it's like I'm moving stuff around, and it changes it. Can I upload my own Canvas?

Right. Yeah, that definitely is something that...

I mean, do we want to write our own Canvas tool, though? Or do we... I think the more interesting one is having basically different tabs where you can see this in TL draw, you can see it in Excalidraw, you can see it in Swibler, like that.

Yeah, that's such a cool idea.

Cool. Okay.

Like iframes?

Yeah, well, even just tabs up here at the top, it could be iframes, the implementation, but basically you can see the way the Canvas is viewed in a variety of canvases, as opposed to writing our own Canvas tool.

So, Meadow, it's like you get to the website, and you instantly understand what the group's working on. It's great.

Exactly. Yes, that is the hope. It should be a live status of where things are for the web. Of course, not every Canvas is going to have a web viewer or web representation or be open source and be able to be embedded in the website. But I think the more we can show, but yeah, the more we can demonstrate through showing it as opposed to talking about it, I think it'll really help people.

Cool. All right. Thank you all so much for tagging along and all the work y'all are doing, thinking through this stuff. Yeah, it's cool to see the progress and hopefully we'll see where we're at in two weeks.

See you in two weeks.

Bye, y'all.
