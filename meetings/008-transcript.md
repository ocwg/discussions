Awesome. So, let me send a link to our notes there. I can share my screen for this bit as well. All right. Can people see my screen?

Yes.

Sweet. Put this over here. And we know everyone here. So, we can scribble this out. Awesome. Yeah. So, we're on meeting number eight now. I mean, everyone has these links that are here. Not making any new introductions here. Feel free to rename yourself.

So, in the previous meeting, which I will link to as well. In this previous meeting, we had some good discussions about schema extensions. We continue the discussion about asset handling, which feels like one of the major sticking points that we really need to get right. Z ordering had some discussion and this question of whether we can potentially appropriate the Z dimension that we would use for a 3D canvas and use that for Z ordering in the case of a 2D canvas. There's also a GLTF as a reference point format. I don't know if anyone here has had a chance to look into it much. I've been meaning to, but it's been a very busy few weeks of travel.

Yeah. So, that was last week. I think the asset handling is maybe something that we can come back to. But we could start with the stuff that was just brought up. So, we have JSON schema definitions and validations. Then we have this question of multiple instances of the same shape. I suspect that second one is something that we're going to have to really think about. I think that's a really good point that has not been brought up yet. So, I think let's start with JSON schemas and validation.

Michael, did you bring that one up? Do you want to kind of expand on your thinking then?

Yeah, now we just have some JSON examples on the GitHub and the specs. But I think it would really help if we more formalize that into a JSON schema so that we can validate. For example, I'm also using our format in my tool for export. So, I can validate that export to the schema, for example. And I think it also can help further discussions or to try out some of the things we already talked about, for example, with the assets. It makes it more, maybe more concrete.

Yeah. I think that's a great idea. It feels like we're at a good point to go and do that. I think if we were to rewind it like a month or so, it probably wouldn't have made much sense because everything was so in flux. But I think the core, at least as we're currently planning to go about this, feels quite settled. It would be really interesting to have some schemas there to do some validation and kind of make examples. I think also as a kind of coordinating tool as we try and implement this in different places to build like running software and test it. That's going to make a lot of sense and make that process easier.

Of course, there are other tools for interoperability for things like TypeScript and things like that that we can also leverage. I think JSON Schema makes a lot of sense as a kind of source of truth there just because the ecosystem is so widely supported for conversion into TypeScript types or validation or everything else.

Also, if you are using all tools other than just TypeScript, you probably also can validate JSON Schema, I assume.

Say that last one again, sir.

If you use a different language than TypeScript or JavaScript, then you probably also can validate JSON Schema.

Yeah, exactly. I just noticed that JSON Schema even has keywords for the IANA content media types, so these main types that's actually a built-in thing of JSON Schema. It fits very nicely.

Shall we set and we can talk about who might be able to do this? Is this something we'd like to do in the kind of next two-week time frame?

I think that makes sense. It's not too much work to take the draft that we have.

Yeah, I might be able to help, I think. I don't have a lot of time, but just to set up a very basic starting point. I think it will already help if you have that, you can iterate on that.

Would it make sense to then make a pull request on the spec repo?

Yeah, I think that would be great.

Okay, great. I think that's going to be...

I don't have experience with JSON Schema itself, by the way. I suppose I'll figure it out. I don't know if anybody else here has experience with JSON Schema.

I have some. I've used it before. I think for what we're doing, it's going to be quite straightforward. I remember having a lot of trouble doing more recursive type definitions dealing with messy conditional stuff, but that's not really the case for what we're doing. It's quite verbose, but that doesn't really matter for what we're doing here.

Yeah, awesome. Okay, have we got any other thoughts on JSON Schemas here? Or validation in general?

I feel like this is connected to... It feels like a quite strategic thing to do, because it's actually going to help at a meta level to coordinate and push this stuff forward.

Exactly, because it will really help us, also maybe for others to write an import for the format, for example. You can use the JSON Schema for validation.

Maybe we should also think about the default file name or file extension, and the default MIME type we would have a server serve the file with. For markdown, for example, .md is sort of the standard extension. And I don't know, maybe text plus markdown or something like that is or text slash markdown might be the MIME type. So we also need to agree on one MIME type for our format and one file extension.

Oh, see, it's probably already taken. Also, quickly, I forgot to ping the channel, or just in case anyone relies on that.

We could also say the file type is just JSON. So the extension should be JSON, and the file MIME type should be application/json. It's also valid. We just need to state somewhere what the agreed upon way should be.

Yeah. So we've got JSON, we have the option of overloading existing namespaces like Canvas.

You can even combine it. You can say our extension is .canvas.json. So then the primitive tools know this is a JSON file and open it in the JSON syntax highlighter. And smarter tools can see, oh, this is actually Canvas.json file. This is sometimes done.

Yeah, that's also what the Ultra was doing. But the Visual Studio Code extension.

So it's really like a third option, yeah.

Yeah, that's interesting. I think, as has been said already, the most important thing is that we actually agree. And then I think in many cases, if you had a different file extension, you'd still be able to pass it into tools as long as they aren't too strict. You know, if you say like, oh, no, no, this is definitely a Canvas file, don't worry about it. Then all the parsing and the rest of it is going to be fine.

Are there any other kind of likely choices here? It seems like the MIME types are similar, right? The application/json, or it could be, we can have our own Canvas MIME type.

I wonder, out of the people here, if there is a sense of what range of, how restrictive MIME types are like across various parts of our computing stack. I've never run into a place where you can't just, you know, have some arbitrary string there. But would there be a reason to not use something custom? Like, is that going to get us into corners?

In the past, I've had issues with the internet information server that you needed to add custom MIME types yourself, even well known ones. But that's a while ago. I don't know if that's still the case. Probably using application/json results in the least problems for most users.

Yeah, this JSON, so it makes sense.

I think that makes sense as the actual way to work on coding this is JSON. And you don't imagine that, well, if we are incredibly successful, then we could see a kind of a big approach to have a custom MIME type for this kind of data. But we wouldn't, I guess, having our own, like we wouldn't actually get many benefits from it, as you still need to have support for that with wherever it's going.

So I think, yeah, application/json makes a lot of sense there.

And I was looking, I was searching for .canvas extension. It might be taken already by Obsidian.

Yeah, yeah, they do have that. I mean, yeah, Obsidian does have that. I think if we really wanted to go that route and thought that it was appropriate, that isn't necessarily going to be much of an issue. I think the hope is, well, I think more than the hope, the intention is that we're going to kind of see these two aspects merge and come out with one on the other side.

Yeah. I mean, we'll need to talk more with the Obsidian folks. I think even before that, we kind of just need to demonstrate some success and gain a bit of trust in us making sensible decisions around this stuff. That’s going to work for their use case as well.

I'm here at the TLDRAW offices right now. I know that there are people here that are interested in this effort and that are kind of happy to adopt it as we get to a point where that's possible, which is great because they're one of the bigger Canvas systems out there.

Also on that note, I think in the next one or two meetings, depending on what comes out of this call, it could be really useful to bring in some people with a background in doing this kind of spec building work. I was thinking specifically of Brooklyn Zelenka, who worked at a company called Fission and did a lot of work on a project called UCan and has been doing a lot of serious work on stuff with this kind of shape
