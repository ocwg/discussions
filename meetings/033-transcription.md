[ Silence ]  
>> Hello.  
>> Can't see the --  
>> Oh, here, and Max, cool.  
Yeah, it had shown on video participants hidden so I couldn't see who was here.  
>> All right.  
>> All right.  
>> Hey, Max.  
>> Greetings.  
>> Greetings.  
>> All right, how are you all doing?  
>> Excellent. We have some new stuff.  

>> It all seems like life, you know, like natural selection, like just -- did you make do a bunch of random things and then take the best one?  
>> Yeah, genetic algorithms get really interesting in this area. I don't know of anyone that's doing like genetic algorithms around agentic stuff. That would be a pretty fascinating research area of like generate the agentic loops, see which ones actually survive by some metric. Anyway, it'd be crazy.  
>> I think I even read the paper on that, where the synthesized program trees, which then can mutate better than text. Anyway, let's talk about our new additions to the spec. Maybe we start with the easy one with a page extending because that's mostly straightforward.  
Yeah, let's do it.  
>> I'm happy to share. I was just pulling up the repo. Should I pull up -- let's see.  
>> The 051 draft.  
>> Okay.  
>> Cool.  
>> Yeah.  
>> All right, let me share my screen. Let's see.  
>> Yeah, maybe I can already talk about the biggest change.  
>> Yeah, please.  
>> The distinction between core extensions and the extended extensions and move them all together into extensions.  
>> Or, oh, thank you.  
>> Of course, I was always confusing everybody, including us.  
>> Yep. Yep. And we had been saying over and over again that it seems like these are just the same thing. We should just call them all the same thing.  
Okay, cool. Is there a PR for this? Or should I just navigate the branch?  
>> Yeah.  
I haven't created a PR yet.  
>> There's this PR.  
>> Looks like you did create a PR.  
>> Okay, then that would work. That would work.  
>> Okay.  
>> So you just go to spec MD, our trusted core spec.  
>> Mm-hmm.  
>> And there we have --  
>> Oh, but it's not going to be -- it's going to be everything.  
>> Yeah, it's also going to be everything. Right? We need to --  
>> Well, actually --  
>> It's medium.  
>> Yeah.  
>> Okay, look for page note extension, maybe in the browser search.  
>> Mm-hmm.  
>> Yeah. Here's the page note. That's an example of one. Do you want to put it up in spec MD?  
>> Yeah.  
>> You can use it.  
>> Extension.  
>> And then this --  
>> Here we go.  
>> Second.  
>> Yeah. Can I jump?  
>> Yeah, well, not jump. That's okay. I see where it's supposed to be.  
>> I see it. It's right here. All right.  
>> It's rather short.  
Yeah, that's all. So we have an extension, we have two small properties. One is the page number, which is an optional number, starting at one. We can discuss each of these points. So in books, there's an ISO standard for book page numbering, which mandates books started number -- page number one. So I thought, okay, maybe -- maybe started one as well.  
>> So you could also start at zero, but -- and then we have a label for pages, which implies that this is somehow a label that nobody really knows what it's for. But if it's there, you can use it in the UI. But it's not a page title. Because if it's a page title, you would want to see it on the canvas as well, somehow, because it seems important. But if it's just a label, then maybe it's -- so it should be the optional label for the other UI's view.  
>> I like that. That's one of the challenges with Markdown is that you have both the file name and potentially also an H1 in the file itself. And both of them can be used. It is not clear which one to use as the title. And so I like calling this label to explicitly say this is not the title. Right? You could use it that way if you want, but you're not -- we're not going to call it the title. So I like that.  
>> Okay.  
>> Yeah. This all seems straightforward. So then you would end up with -- and this is a node -- just to repeat back to you some things. This is a node extension. So I could have a node in my set of nodes that is the page node for that thing. That node, since it's a full node, can have like spatial orientation on the overall global canvas, right? Like you can have X -- like can have dimensions, size, and all the other stuff that's on the base node property. And then if I want to, I could optionally use the parent-child relation to say that these nodes belong to this page node, and/or I could also, if I wish to, use the group relative extension to make that page into a group with some other nodes. It's like -- is there a recommendation for how to do that?  
Oh, here we go. Indicated by the parent-child relation. Okay. It's very brief, yeah. That makes sense. Indited by the way, instead of in the -- in case you have it up in your editor right now.  
>> Yeah, not this typo.  
>> Yep.  
>> Yeah. Cool.  
>> Okay. Aaron, any questions about the page node extension before we burrow into transclusion?  
Honestly, this page node extension is very far outside of my area of expertise, so I have no feedback to give other than to just, like, close my eyes and give you a thumbs up.  
[laughter]  
That'll work.  
All right. Well, should we talk about transclusion? Do you have the material in the -- in the spec, or should I bring up your message in Discord?  
It's exactly the same, it's -- I just copied from the spec. So no -- as a result, it's actually the right thing.  
Great. Yeah. So, motivation, maybe motivation doesn't belong to the spec, but I wanted to mention the word "transclusion" at least once in the spec for people who know.  
Mm-hmm.  
I'm not entirely sure the best, like, way to include this, but I think that the motivation for a "by" feature exists is extremely important, and if it was nowhere to be seen in anything related to the spec, then I think that would be a mistake, because when you're designing the spec in even when people are using the spec, you have to know, like, why does this feature exist, what problems is it trying to solve?  
Mm-hmm.  
Yeah, it might be that this all deserves an entry in the design decisions document once we, kind of, have actually decided -- I guess we're working on the design right now, and we haven't fully decided, but once we have, maybe that's where that -- and we could potentially even link to that from the motivation, like, for more information, see design decisions this entry.  
All right, but let's talk about it. Using a node B, do you mind if I just read through this, like, narrate a loud Max, and is that okay?  
Yeah, it's greasy enough, yeah.  

Okay. A node B as a resource in another node A can be seen as a form of transclusion. Okay, so resources prior to now have been not -- we haven't supported the idea of pointing a resource at another node. This is especially useful if a node contains a complex inner life, such as a number of child nodes, the apparent child, and should appear in multiple places on the canvas. Okay, I guess that's the two. I might break those into bulleted, like, to make it clear that those are two conditions. I guess this is the end-order, right? Not to be persnickety, but if you wanted to a node to appear in multiple places on the canvas, this is the way to do it regardless of whether it contains a complex inner life.

That's true, but it's especially useful if you have both, because if you only want to display the same image on two places, you can just copy the node and just have it display the same image. That's easy. But if there is more on the node arranged and it should appear in two places, then really the transclusion is what you want.  
Yeah.  
Yeah. Okay, so that nodes to be used -- I agree with the motivation, I'm with you. Nodes to be used as resources are not explicitly added to the resources array, okay, interesting. So resource -- I'm trying to remember how resources work. That every node in the OCIF document is automatically available as a resource as well. Okay, okay. They're addressed by prefixing the node ID with pound. So -- oh, here's an example node, and then there's the implicit resource. Oh, interesting. So it's kind of like a relative link in HTML. That's the inspiration, yeah. It's very cool.  
Yep, and IDs are unique. I mean, yeah, this is like the way that CSS works, right? More or less. What's the -- yeah, classes are -- yeah, yeah, this is the pound is the thing. Classes.id is pound, okay, great.  
All right. So then -- wait, oh, it generates this implicit resource, gotcha. So this is not actually -- so this is not going to be in the resources array. You're just showing what is -- yeah, how can I --  
Okay. I mean, implicit resource, I would just like maybe add a note here that's like this will not be present in the resources array, but nodes -- other nodes can leverage it as if it were. We're there. It should be as a part of this should be also defined that an explicit resource should not have an ID that starts with the hashtag.

That sounds like really smart.  
Yeah, that is a good point. Although I'm trying to think if -- let's look at how resources are defined resources -- say, let's see, go up to -- I think we don't have that restriction yet. I think you're right. And I was just going to run down to what we do have -- what we do say about resources right now. A reference to a resource which can be an image, an audio file, or node, see resources. Resource can be empty, in which case, or node is acting as a transform to other nodes, maybe. Resource content is cropped or limited by the node boundaries, it's commonly called clip children only in this respect to resource content as a kind of child. CSS is called overflow hidden. Resources can be defined ornamental borders. Resource fit. Okay. Size and resources. I think it's down in the resource array explanation. Yeah. It is in the style though. Yeah, assets, resources, okay. Okay if there's two kinds of assets, resources and schemas, those are managed similarly. So the ID property down there says OKIF-type ID, and it says CID for details. So all the details of the ID are globally defined somewhere else. Yep, right over, it's up towards the top here. Yeah, there's the OKIF-type ID, and it says it's a string which should be unique. So we should probably define a list of disallowed characters, or maybe a list of allowed characters, but disallowed is probably more sensible in case people want to use different languages or whatever in the IDs. I would recommend avoiding, like just straight a band, the hashtag as we've seen, and also dots and slashes and colons, because these are often used as like path specifiers. So maybe somebody wants to specify like a series of three node IDs in like a hierarchy by doing one ID slash another ID slash another ID. I would like to allow most characters and most rings, but yeah, we could disallow just the leading hash mark.  
Yeah, okay, that's a helpful point, Aaron, thank you.  

Let me run down back to Transclusion, which thankfully doesn't show up all over our spec. All right, so yeah, you're saying when you define a node like this, this Berlin node position 100, 100, size 150, and you don't have to do anything else, and it will be implicitly available as a resource in the resource array, so semantics, my type. So my type is the same as for canvases, so I have not introduced different mind types for different parts of a canvas.  
Yeah. But maybe we should. I am not sure.  
Is that a valid OKF JSON that?  
I would say that an OKF node is not an OKF file. So that the mind type doesn't really make sense.  
Yeah, that feels strange.  
Okay, so then maybe we need a new mind type for the node.  
Yeah, possibly, because yeah, right, because we would expect it to be able to be evaluated as a valid OKF file. We could have fallbacks for a node, like, so that we would be talking about this fragment right here, yeah, yeah, okay.  
So then the question is, if I evaluated this with an OKF validator, would it be valid?  
Not at all. Not at all.  
Yeah, the problem is we don't have this nodes. If we only have this, it's valid, but we don't have that nodes thing above it.  
Yeah.  
Well, Aaron is right, and we need another -- Are you making nodes max on your side, because I'm not taking those today?  
Yes, but then what is the name? Is it application slash OKF dot node plus JSON, because this application slash foo plus JSON is an established convention for JSON subtypes, but now we need to subtype the OKF subtype or it could be OKF minus node plus JSON.  
Right.  
Yeah, I think OKF dash is -- Like a formula.  
Yeah, well, I mean, not really, I mean, it's in a string. It does because of the slash and the minus and the plus and all that kind of stuff. But I think we're thinking of it as a mime type. So I think OKF dash node plus JSON is probably the most sensible thing.  
I agree. That makes sense to me. I mean, how else do people break multi-word JSON types, right? They probably break them with -- I guess let's look and see. If it's broken, is it snake case, is it underscore case or whatever, when you do multiple words here, my guess is probably snake, so probably cat dash or minus. And then, yeah, you might in this -- you might actually -- I'm tempted to expand this example to like not -- not elide the content, but actually just replicate it.  
Yeah.  
And just say, like, this is the entire thing, like, it's all of it.  
Okay. We'll do.  
Yeah. All right.  

If a node A contains a node B as its resource, we call this importing, imports node B, all properties and extensions of node B are copied into an empty node A prime, then the original node properties and extensions of A are copied also into A prime, possibly overwriting things. You know, let's talk about that. In particular, the effective position in size is controlled by node A. That makes sense. The temporary node A prime is used instead of A. So we're -- you're saying -- I don't know that you specifically say it here, you sort of imply it, but A takes precedence over B. Any duplicative properties and extensions in A overwrite those in B. I think that's what you're saying, right? It's like an array merge or an hash merge.  
Yeah. I think we define the merge process when we define the inheritance we have parent child.  
Mm.  
Okay. I think we've already got it similar to that, but here it's not parent child, here it's importer and importee or something like that.  
Mm-hmm.  
Well, it might be worth mentioning then that it's the same -- it follows the same process as parent child. I wonder if that's going to be a generally useful primitive, like when you're merging two nodes.  
It is. I think it is too. Here's like defining explicitly how they're merged based on the -- which one has precedence, you know.  
Yeah.  

Okay. What's particular tricky in the semantics for transcription is that actually this important node is used like a template and generates actually new nodes in the canvas. So if I have -- I have one node, let's call it a "D" as a child, and now I'm just playing this over here and over here. So the "C" can be merged into that one and into that one, but the "D" needs to be replicated out of nothing as a child to this one and another one as a child to that one, otherwise we don't have different nodes on the canvas with different positions. So the process of transclusion actually generates new nodes. That's quite fancy. It's more complex than in the parent-child example where we only talked about. How is it generating new nodes? I think of it as overriding the node properties on --  
The direct one, yes.  
So "A" is importing "C." So these are merged into one node and "D" is also importing "C." That's also merged into the existing node. But the child "D" of "C" -- we have these two, let's say, pages, and they're both just play the same thing. So this "D" needs to be on both pages, so these "D" needs to exist two times. But it wasn't existing two times before. So now we need to have "A" which is imported "C" and has the "D" which got cloned in. It doesn't work otherwise. We are effectively generating new nodes in the Canvas, at least visually.  

I should mention something. The semantics here are exactly the same as if you were to use another "OKF" file as a resource. The only difference is that the set of other resources are shared between this and the tree of nodes.  
Can you say that again, Erin? That's awesome.  
Yeah. The semantics are what?  
The same as if you have a entirely separate "OKF" file and you include one in the other as a resource.  
You're so right. This is wonderful. That is cool. Yeah.  

Interesting. Going on that topic, how it compares to just using a separate "OKF" file, I'm curious as to what actual applications will make use of this feature and how it is like semantically done. My experience is obviously with Godot Engine and my thought goes to using a Godot scene and another Godot scene, but those separate Godot scenes are separate files which have their own separate things. Having a separate "OKF" file is the natural translation of that. I wouldn't have a way to generate nodes as resources as a concept inside of Godot Engine, but I'm not saying it's not a useful concept. It's not a concept that maps in that case.  

Let me ask you a question on that. If you have a scene file in Godot, let's call it your master scene and then you import a sub-scene called "A" in two places. What is Godot doing with that then?  
So the instances of "A" each would have their own name and then it would have the same semantics as you already discussed here, where any children of "A" become their own nodes, it's effectively instancing as a template and duplicating.  
Okay, so it's the same semantics.  
Yes.  
Yeah, and I think your observation that it's like importing an "OKF" file is brilliant because that's exactly what we want and the only difference is instead of importing a file, we are pointing it to a node with its children, and that is like an implicit file which we are importing in another application of a map.  
Right, and then mechanism.  

Yeah, and your question, Aaron, I want to try and motivate an answer real quick of what would people potentially use this for. So I mentioned this last meeting that Notion has the concept of transclusion in the application and what most people use it for are cases where they want to duplicate content across many different locations and then be able to edit the content in any of those locations and have it update everywhere. So it would be the case where, assuming that these three were like these were transcluding this original set, I might want to come in and change this to C and have these things automatically update to change to C as well.  
Right, it makes sense.  
Yeah, and so you end up with that to give a practical use case in Notion. You might have a policy in your company that you want to reference on multiple pages of your company's internal wiki and you want that policy to only be represented canonically in a single place. And when you change that policy, you would like it to be changed, like all the references to it to also be changed because it's very important to not have like out of date policies in your internal knowledge base. And so that would be how you might use a feature. Transclusion makes a lot of sense in that case because you're referring there, all those transcluded locations are pointing back to the original canonical reference.  
True, but that also assumes, I guess, that you're working with a single Okif file where you have multiple instances of that policy. The alternative would be if you had a dedicated Okif file for the policy, which was included, and then that could be used in many Okif files potentially.  
Mm-hmm.  
Mm-hmm. Yeah. And you're talking about almost the same behavior as the Transclusion.  
Right.  
Yeah, I love that. If we can make it the behavior the same between those two cases, then basically authors have two choices of ways to handle this. I think in the case where there are cases where it makes sense, it's just strictly more convenient to have a single file, and these would be cases where I would expect that people might even do things like embedding the assets in the file itself as base 64. Like you just want to be able to pass around this big file and not have to pass around a directory with all these files that are relatively related to one another. And so authors can choose that direction or they could choose the direction that you're mentioning, Aaron, where we actually have to pass around those multiple files together in order to fully institute the Canvas, but it has a lot of convenience mechanisms because of the file system. What we also can define is how to copy or export a node. If we say when copying or exporting a node, all its direct children and recursively sub-children are also to be exported, then we have always the same notion of what's belonging together even for importing for Transclusion. It's always this parent-child structure that defines togetherness. We could also think about using groups also for that. I think using the parent-child structure, using one structure and advising us to use one structure I think is wise. When I was narrating this, I was thinking about the fact that it could be parent-child or group, but I think having one way of -- one preferred way of implementing this is probably a better idea. Parent-child can have inheritance, group can have multiple -- I think can belong to multiple groups.  
That's right. Yep. So we need to think clearly here what we need.  
Yeah. What happens if you transglue to group?  
Well, a group has a difference, so all members of the group should be transcluded. That doesn't seem complex.  
Yeah. Both would work. I can't think of any strange cases there. And yeah, if you have -- even if you have a group, like let's do some drawing here. Even if you have a group that contains multiple -- or a node that is contained in multiple groups, that should be fine too. So like these two guys are both groups, and I've got another thing, C. And in this case, B is in group A and -- or group one and group two, group one, group two. And if I transclude B, then I'll get both A and C, interestingly, because I'll reconstitute both groups.  
Well, now I'm not following. So we have two groups that are called one and two. If you transclude B, you get neither A and or C, because you just transclude B. You can transclude a group, then you get members of the group. Can you transclude a group?  
Why not a group, and -- groups are relations. You can't do that. They're not nodes.  
Well, we could extend that as we did for almost all concepts here.  
Oh, no. Relations and resources. Oh, my gosh. Well, okay, let's think about this. So transcluding B, I don't know that it's my desired behavior as an implement -- as like someone who's managing this canvas or building this canvas, that transcluding B would also include every node that it's grouped into. I think that's a special situation for parent-child, right? The fact that B happens to be in groups one and two, like I just want to be able to transclude it down here and edit it into B good and have that update here, even though it's in two groups here.  
Yeah, we just don't care at all. We just don't care. I think with groups, it's outside of the transclusion concept, really. But it would be nice if you could just transclude a group, why not? It would be. What would it mean, then you would say, A, contains --  
Right. So.  
Actually, no, it's -- right now we define transclusion by merging. We merge the important node into the master node, but we cannot merge a relation into a node. That's just outside our type system, but it's different things.  
Yeah. I don't know that I get what you're saying and I get your intention here. If you have a node and you want it import multiple nodes, use parent-child. Can we not have a representative of a group? Have we really defined that on the groups?  
That's a good question. I haven't looked at it in a few months. Use that node. Great.  
Yes. I think there is a way to do this, let me see. Group has members and group has cascade delete, that's all. What are we losing if we don't include group in the transclusion concept at all? You can't transclude a group, you can only transclude a node. You can transclude that node and all of its child nodes.  
What happens if you transclude a child? What happens if you transclude a child? That node is transcluded, and if it has children again, then they are transcluded. It doesn't matter. If the node has parents or not, we don't care. Got it. We only walk down.  
Okay. Yeah. Make sense.  
Yeah. I wanted to chew on that for a minute. So open questions of what to do with groups. Max, did you give them, we've got about 10 minutes left. Were there other things in this discussion that you wanted to hit on, or do you feel like you have covered?  
This is our last point, sort of the transclusion.  
Okay. Got it. You covered everything within transclusion that you wanted to cover.  
Yeah.  
Okay. So let me try and get at the main point that I was trying to get at earlier with the transclusion, being similar to the file inclusion, because they are extremely similar. And of course, it's a powerful tool by itself to just explain that feature to people. But the main thing I'm wondering is, is it useful to have both this feature and the file, including a feature? Or should we just instead find a way to embed files inside of Oakf somehow as a blob of binary data, or just maybe a resource that's a base 64 string that has all the file data? The reason I mentioned this as like a potentially preferred alternative is because it is simpler to not have transclusion. And I believe in most use cases. Now you can certainly tell me if I'm wrong here about the use cases with canvases. But I'm thinking about the resources, the non-file resources within those files that could potentially be shared. And now with a, with the domain I'm used to with like 3D characters, it's almost always the case where stuff like that is not shared. So for example, if you have one file with like your scene and it has five instances of a character, Bob or whatever, then the mesh for Bob and the nodes for Bob skeleton and the material for Bob are all going to be contained in that Bob file. But the Bob mesh is not used outside of the Bob model. Like the, you're not going to have a static Bob mesh just like sitting out there in the world or like Bob's face plastered on another object. These things, those things are usually self contained to that specific place. This is not always going to be the case. Like you could have a 3D modifier that just has like generic grass material and just chuck it on many objects, but in a lot of situations in 3D content, stuff like that isn't typically like quite reusable and quite that generic. And I'm wondering how that would work with, with canvases if the individual pieces of a subtree of nodes could be, are typically expected to be reusable outside of that tree of nodes.  

Well, at least in, in knowledge management apps, like in notion and infinity maps, Transclusion is a built in concept, which is more integrated than importing sub files. I think you can somehow switch to English if you want.  
Yeah.  
And I've looked at this before at your reference. I think they have example points or something.  
Yeah.  
Yeah, I know this tool has Transclusion. I wasn't aware of notion, but so. But the point is that the current way how we define Transclusion in the, in the canvas and importing a file is different because in a file you can have other resources and other relations. And our current way of Transclusion does not. But also what does it mean if I, if one file imports another resource, which happens to be an OK file, we can take that root node and merge it in as we defined. But what happens to the relations in this other file? We can just add them to our own relations array. So Max, you mentioned relations is actually brings another interesting point here. We have to explicitly define what happens to the relations of a transcluded node hierarchy. Because if the relation, if the node hierarchy is acting as a template and let's say like, you know, some, some of those descendant nodes are in a set. When those nodes are duplicated, do we, do we, does the duplicated version of the node get added to the set? Does the template like node exists in the set in any meaningful sense? Or is it just there to indicate that its instances are in part of the template it set? Is there the correct questions?  
Yeah, those are good questions. What this is pushing me towards Max is what this is pushing me towards is wanting to only allow the transclusion of individual nodes and not supporting the entire hierarchy. I know that that is that maybe by the time, yeah, that's not that's. The motivating use case was to have a reuse of logic on pages. Yep, and this, it goes all the way back to our motivation, right, where I was saying. I said that I believe that it is sufficient to have a transclusion that supports the idea of a node appearing in multiple place on the canvas. And you said it's especially useful if it contains a complex inner life, such as a number of child nodes. And so there's a there's a question of whether we can achieve both of these motivations in a way that's conceptually simple enough and clean. It's possible that we can only achieve the second one and that we decide it's valuable enough to leave it in as an extension that people can then choose to export to a support or not. It's an important thing to remember in terms of like remembering that we're currently a container format for interrupt interchange between applications as opposed to true interoperability. And so as people export, if there are no canvases that support transclusion and they export to a canvas that does not support transclusion, then just simply duplicating the nodes is an acceptable step down, so to speak. And then when it gets round trips back to that canvas, then that node is no longer and transcluded. They're duplicated, which is they've lost some fidelity between those canvases. But there is sort of a natural way to fall back to a less rich feature here when exporting.  

Well, we're coming up on time, Max, what do you what do you want to do for next steps here?  
Simply fire seems to be the right angle. What do you want to do? Is zero five one generally do is this I haven't. Do you want to wait until we figure out transclusion before we release zero five one and then kind of move from kind of bundle it all up together? Is this possible? I mean, I have no opinion on that.  
Okay.  
Cool. We call it craft one to get it out quickly or finish unscrewing ideas. I really don't mind.  
Yeah, I think we can wait and put it all together in one. The release process has some overhead to it. And there's no one that's particularly saying, you know, I need this feature now. So I don't think we're under any time pressure here. So I think we should try and get get them to get done together. But probably also shoot for something in the next like two to four weeks or so of getting zero five one out there.  
So, righty, I love coming to these meetings and stretching my brain every time.  
Fantastic.  
Yeah. Thanks for the good questions, Aaron. You.  
Yeah. Both helped to simplify and complicate.  
Well, that, you know, it's, it's our job as fact designers to poke holes at it in every opportunity we can, right?  
Absolutely.  
Yep. Successful day when you brought up problems that someone has not thought through yet. Honestly, when, when I've been designing like my own format, especially, I've been thinking to myself a lot, like, gosh, how is somebody going to screw this up? Like, somebody's going to read this and get it wrong. How are they going to do it? And how can I prevent them, whatever, whatever that future possibility of screwing up is.  
It's a great mindset, Aaron.  
Well, well, thanks guys. I'll make sure we get a meeting on the calendar for two weeks from now and talk to you guys soon. Thank you. Have a good time.  
Okay. Thank you all. Bye.