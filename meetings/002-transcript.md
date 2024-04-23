# Meeting 2 Transcript

date: 16 April 2024

Let me go.  So,  uh, let's see.  So, yeah, I'll, I'll go through that again. We have, uh, the discussion that Chris started on,  uh, GitHub around what we actually mean by interoperability. We have, um,  some questions around what the needs are for this spec for the kind of, like, non whiteboard canvas tools, for lack of a better word.

That's things like stately and the systems that are less about drawing and more around, um, kind of structured system diagrams and that kind of a thing. Um,  some suggestions came up around, uh, kind of utility library support for helping people integrate, uh, this spec and do things like migrations as new, new versions, uh, come along.

Um, I did some work to.  Demonstrate interop between Excalibur and teal draw, which we can touch on. Although there's, there's more than needs to be done there. And then a couple of the specific schema questions that I thought would be good to discuss, uh,  how we handle, uh, objects in a canvas in a tool that doesn't support it.

So for example, if we have a tool that has free hand drawing and one that doesn't, what should the, what should that second tool show? Um, if anything, Um, like do we show, do we show the bounding box? Do we just show a point in space? Or do you have a little, a little, uh, message somewhere that says, you know, some shapes could not be displayed, whatever it is, there's some questions there, um,  there are questions around freehand drawing.

Some of that discussion happened on GitHub already. And then there's a kind of broader question around how to handle. the, the locality of schemas. So  one option of course, is you have a base schema that applies to the kind of entire document and defines all the, all the stuff within that. Um, another option is to have it more localized, but you have a base schema, but then you, you can also have further schemas, for example, for individual shapes.

Um, so you could, you could have, for example, a kind of a base of shared interoperability, but then you might have. You know, two tools might have a support for a specific kind of shape, uh, with, with that schema and others might not, um,  that's everything on the, on the agenda. How does that, how does that sound to everyone? 

Fine for now, I think. 

I saw you speaking, Dragan, but you were, uh, muted.  Sorry, it was just a footwork. 

Sweet. Um, so I guess we can, we can go through these kind of in order then.  So 

I will also.  link to the the discussion that Chris started. Is everyone here in the um, in the discord by the way?  Or I guess I should ask if anyone isn't in the discord.  You don't, you don't have to be but that's where we're currently dropping all these links. 

So yeah, there was this discussion started around. what, uh, what interop really means. Um, which I think we can kind of take as  for this spec and the, and it's implementation in, in these different tools, what are the things that we actually want to kind of make assurances around? Um,  so, you know,  one thing, for example, is, is what came up last week around not, uh, interfering with data that you don't understand.

So.  some, there's some extra shapes in a canvas that you don't know how to interpret, you know, choosing to, or well, making sure that you leave those alone for other tools to, to consume. Um, but then there's, I think, harder questions around things like, um,  What are the visual properties that are important to preserve, like,  and, and Lou was talking about this on,  yeah, on that same thread, right, like these questions around, um, text as an example, where it's probably fine for a different font to be rendered, but if, for example, the, the bounding box is changing, maybe that's going to cause problems. 

Um,  so let's, well, let's see here. I will be trying my best to  take notes as well. Although it might be hard to both, uh, both host and take notes. So we'll see. 

So  maybe, maybe where we can start here is just kind of getting some ideas from you all around  what is it that we actually want to be preserving and kind of assuring interop around and also maybe. Which things we explicitly don't care about or don't need to  make interoperable.  I think, I think we have a small enough group to just kind of  unmute and speak. 

Yeah, I think the crux of that. Go ahead. Yeah, I  guess the crux of that is called out in Chris's last sentence there. It's like, maybe we need to look at the particular kinds of archetypes. Of canvases to help guide us in terms of what sorts of information. I think it was just last week. The last meeting who,  uh, pointed out that we may end up with two specs that are able to interoperate between them project between them because there'll be situations where Visual fidelity and the presentation of visual information is the primary concern versus others, where it's more structural.

Or relationship or topology. 

That sounds,  sounds right. I'm just getting up some, some notes here so I can, uh,  turn this into a, into a summary at the end. So maybe just on that  point, or actually let's, I'll put that aside for a second, but maybe after we get a bit more info here, we could come back to that question of what are the kind of archetypal  Canvas tools or use cases, um, because that might be a useful thing to think through. 

But anyone feel free to, um, unmute if you have, if you have thoughts on,  um, kind of what interop means and what we're trying to preserve in the, in the spec between tools.  I was wondering actually the, that also can be a difference between the open and safe, uh, format and the copy and paste format that probably don't are the same  copy and paste is just, just a part, small part of, uh, of a whole spec. 

That's, that's definitely a good point. And, and that does connect to something, uh, later on the agenda around kind of how localized the schemas are. And I think maybe that is kind of a point in favor of having schemas at the, the shape level so that you could do something like copy and paste and you're essentially copying a fragment that includes the, the schema for just that object.

Um, and if the receiving. And can interpret it, then, then that's good. 

And, uh, is there a difference? Um,  I'm, I'm also building a visual programming system myself.  I don't, in my system, I don't have a difference between the, the edges and the notes. How is this with other, um,  how is this for the spec or for, in other tools?  Yeah.  For example, in Excalibur, we also don't have like separation between nodes and edges.

Everything is just like objects on the canvas. Um,  so yeah, uh, we do have arrows that, that specify kind of from which element to which element they go to, but they are, uh, like they would be,  uh, on, uh, according to like a spec of the, uh, right, it would be a separate object within the,  uh,  like the taxonomy, I guess. 

Yeah. They have type. Yeah.  Yeah, exactly. Yeah.  Yeah. I think there's some really good questions around that. And I've. I've been trying to think about whether there is some kind of fundamental distinction that can be made and, and have really struggled to really come up with one that's not mostly arbitrary.

Um, in, in the sense that, you know, uh, edges like in, um, Obsidian, for example, they do describe a relationship, like they are edges in the graph sense. Um, but they're also visually shapes on the canvas. And, and so it's not clear kind of how that distinction can be drawn. The one distinction that maybe can be drawn is anything that is expressing relationships that is, you know, not itself  visually represented.

So if you have, uh, some primitive, uh,  groups, let's say, but that group doesn't actually have any visual representation, then maybe you could, you could make the case that those, uh, kind of ontologic ontologically separate from the, the objects on the canvas.  But, um, I'm unsure.  I think that was one of the more fascinating, um, things that I learned from both the TL draw and the Excalibur folks is  the notion that in their world, even the things that they do have, you know, relationships that they maintain long term as you move around, you know, these, these connections with things, between things are maintained because of the richness  of the thing that they were encoding into an edge, they don't represent it as an edge. 

And I think why, why most of these. You know, pieces of prior art do have that distinction between the node and the edge is to have a, um, normalized regular interface for saying like, Hey, this is the thing that expressing relationship here's, you know, how that can be predictably, uh, inspected and applied.

And so I wonder if it's. less a situation where we don't want nodes and edges, but maybe we need more rich edges. Maybe,  you know, it's the is a versus has a sort of thing, you know, um, is do, do these special kinds of nodes have relationships? Is that something we should express as subordinate to the node rather than as a peer?

But I just, I think there's something hidden in this, um, you know, realization that we're seeing across those two pieces of prior art and even the visual programming example that was just called out to  right. I think one,  sorry,  go ahead. Was that I think what's I  think what's fascinating in these canvas tools is that they're both visual and structural and some are more on the drawing side.

Right.  And if you take it to the extreme, you just have a 2D vector drawing program. And if you're at the other side, you just have, I don't know, an ontology editor. And in between you have these canvases. And they have vector drawings. And for some of them, they understand the structure and also know which vector drawing represents which item in the structure.

And then they might also have some additional structure. So it's really maybe  these both worlds, visual stuff, structural stuff, and some mappings in between, which somehow need to be represented in the data exchange format.  So this would also resolve the edges. So you have an, a visual object representing a drawn edge, and it maps to an edge object that actually has some semantics, or maybe it doesn't.

It depends on the tool that created the edge.  So it's not restricting the user that I just need to have any semantics,  but somehow you have these both  layers and  they might be connected or not. Yeah. 

My feeling on an edge is that it's, it's its own object. But in general, it's just an object that depends on one or more other objects. So it's an object with a dependency on other objects, and that's how I've done them in the past. 

Yeah, I, I, I've, I have a similar feelings about this. And like, in general, I think if you have like a graph of nodes and edges, you can kind of transform it into, you A graph consisting of  nodes that represent both nodes and edges in the previous, so like, I think both of those only having nodes without like having edges represented as a separate data structure in the format,  or, uh,  Or having them, like they are both interchangeable to some certain degree, right?

I think the, uh, importance here is do we want, like, do we want to call it out in the format as a separate entity? What advantages might it have over not doing that, right? So,  um,  I, I think we, we can think about like, What may be the reason to have edges as a separate,  like if there are any specific things that maybe I don't know, help with optimization or with some algorithms. 

Thank you. Oh, one thing that came to my mind and it was mentioned like, uh, edge is just the thing that references two or more other objects that exist in the space. Um, how far maybe we should take that concept and like have each of the properties on the object just be a reference to something else, like color of, uh, of an edge.

Is just something that references the concept of a grain color. Um, so can we just like relate everything, even at the level of individual properties, does it make sense?  I think that might make, Oh, go, go, go.  Oh, I did say that. I definitely think that it might be very interesting to have.  Like references, what you said, I don't know if I understood correctly, but what it reminds me is,  uh, open API and like referencing,  like you have a map with general entities and you can reference, uh, things from different places to different places.

That's kind of how, so like, for example, I had five shapes and all of them have the same color. And instead of each of them having hard coded the same color, they are referencing like one. Thing that is like an abstract coral color variable inside, like a call color node variable or something like that.

Is that,  is that correct? Yeah. Okay. 

Yeah. If, well, if you also, if you go that path further, you end up pretty much with a copy of RDF,  very, very fine granular, everything can relate to everything it's it's, it's cool, but also it's so generic that it's  hard to use for anything in particular.  Um,  what we also have in biology is edges on edges. 

So if you take that to the extreme, you have, you have objects that can have a visual representation,  and then you need something like a structure that can say, well, this object actually  depends on these two other ones, because it's more or less, this is really an edge.  So, so some structural primitives are needed besides just  having these entities. 

I think one, one distinction that we might be able to leverage here is that part of what  unifies all these canvas systems is the fact that they have some underlying set of addressable objects, whether they're on the canvas or not, which is not the case elsewhere right? Like if you look at, um, the DOM on the web, part of reference there is often structural, like it's like, you know, the, it.

the second child of the element with this ID or something. Um, and so one way that we can make a pretty kind of formal distinction between just kind of regular objects and stuff that is kind of relational in nature is that the relational stuff  has to refer  to those other objects on the canvas, whether it's like an edge, uh, like, like a binary edge or a hyper edge, or it's some other structure that's expressing relationships.

Part of how that must be defined, or at least the most kind of straightforward implementation of that, requires that that definition include references. Which is something that we could also pick up, like, pretty automatically, right? Like, you could look at a shape or an object on the canvas and be like, Does this include the IDs of other things?

Um, in which case, It is in some sense, like a relational object. 

Um, I was wondering in general, how close do we want to get to like a DOM object model in this, in a sense, right? Because we could kind of  use XML and call it a day,  uh, more or less.  Uh, but I don't think that's the point. Uh, however, there is a lot of, like, for example, DOM is obviously, uh, By structure, uh, tree like, right? 

Uh,  we, is this something that we all agree on that we want to keep the structure of the file flat? For example,  do we want to allow for, um,  like actual,  um, embedding within,  uh,  Like actual children inside JSON, like, I mean, like, like actual, actual subnodes inside of nodes, or do we want to like, just using references, right.

Okay.  We have one  basically array with all of the objects. And if one object relates to some, like, for example, groups, right. Or, uh, tables or whatever, uh, we want to do, uh, we use only IDs, right. Embedding the entire nodes inside.  This is pretty like, uh, I think everyone is agrees on that.  Well, for, for, for my, uh, the tool that I'm building, that would not be enough to have one flat, uh, list, um, even with references.

I think I'm thinking of, for example, the state machine. Which has a state chart. It's a better example, I think, which can have, um, multiple, uh,  state charts, uh, as children  and even deeper. 

And in that situation, you, um,  yeah, you need to, uh, when you say, I think for me. The idea is just to have a checkpoint of  whatever scene you have. So you can flatten it when you export it. So it's easy to, to pass around. Cause I think what's, what's the goal at the end? Like if you have a visual programming environment, you have boxes and arrows.

Why do you copy it to TLDraw? It's just to make it nicer and edit it a bit, the colors and the text or something like that. So  I would be really practical and  where it would be.  For me, at least at first step, it would be like a checkpoint thing. You just more or less dump and flatten your, your scene because you don't know what the other person is going to do,  or you have to export it separately if you have so,  Uh, some diagram, maybe you export them independently or something like that.

And,  um,  and for a standard coordinate system, when I export it,  I kind of reset the coordinate system because when I select a group of object,  it, uh, the bounding box of the group determines the coordinate system of what I export for instance, so I can drag and drop it any place into a new canvas and the new coordinate system would be the one way I drop it and stuff like that.

So, uh, Yeah, I would keep it as simple as possible for me. And,  and even the, the, the edge is, is just,  yeah,  there's an edge to be drawn, but what do you want? It's like the two boxes still move together or they're still attached in TLDraw for instance. Cause TLDraw like arrows change, changes every week.  If they fine tune the arrow system every week and it's like perfectly tuned and stuff like that.

So I don't think you can encapsulate that.  In the file, you really won't let the tool do their best,  you have to draw an arrow between those two boxes and do what you can or, or if your tool doesn't draw arrows, you ignore the arrows and stuff like that.  It, it does seem like, um, if, if you're, so if you have say a state chart or something, right, and you need these, like, Subsystems to be contained that you, at least in principle, you can express that relationally where you, you have your, your, your node and you're like, okay, this.

This other cluster of nodes and edges is a subset of this node, for example. Um, it could be the frame, the frame system, is it in Figma or something like that? So basically you have  a series of groups of objects, which are independent more or less.  I think one important part of that though, is this question around kind of.

Uh, like coordinates and, and kind of coordinate systems. And  I, I think it's maybe worth distinguishing like a couple different kinds of, of grouping primitives that we have. One is where you, for example, select some shapes and you put them into a group. And then all of the shapes in that group are now kind of, their coordinates are relative to their, to their parent group, right?

So if you rotate the group, everything inside is going to move with it normally. Um,  that's different from the kinds of groups where it's just basically just a set of  And you're saying like, here is just a, like a bucket of objects on the canvas. There is no other kind of, uh, affordance given in terms of like UI or UX by default.

We're just, we're just making this bucket so that we can refer to the bucket as a whole, which would.  you know, be enough potentially for, um, you know, uh, defining some subgraph, for example, and being able to refer to that as a child of another node. If you wanted to kind of encode those semantics, 

um, what I think should be possible to express exactly what you were, uh, talking about now is Like just having two types of links between nodes, to call them that way. And like one type, uh, kind of just takes the geometry, the transformation as they are, versus the other one kind of takes it from the parent and then kind of builds on top of it.

Uh,  it seems that like in principle, it should be able to kind of represent that, uh,  in correlation to the edge between the two objects. 

Could you, um, could you just  explain that one more time? I didn't, I didn't quite catch.  So if, uh, one wants to, um, represent a relationship where a child object is in kind of relative coordinate space of a parent, uh, having one type of edge for that and for a child that is kind of independent in the absolute, um, coordinate space, uh, then like a different kind of edge could signify that.

Again, at least in principle, I'm not sure, like, that would be the way.  Yeah, I think, I think that makes sense. And part of this is also a question around what is encoded explicitly in the spec versus what is kind of  Some level of coordination around expected behavior when you're interacting with these things.

Um, it does seem, at least at first glance, that something like groups or those kinds of, uh, coordinate changes where you're making something relative to something else should probably be, like, a spec level thing. Because if you, if one tool expects,  you know, coordinates to be relative and one doesn't, that's going to, that's going to break everything.

Um, but it might be that those, uh,  like those could either be explicit relationships relating to those kind of coordinate relationships, or they could be a part of how like a type behaves, right? Like if you have a, A type that is a group and it has a bunch of, you know, references to some, uh, member nodes or something, then maybe that's  Part of the, like how that's implemented.

I'm not sure if that quite made sense, but yeah. Maybe it also makes sense to simplify and just say everything is absolute and we have groups and the importing tool then might convert it to relative coordinates if required, just to, to not have every edge case in the format. 

Also, one thing that.  A dragon, I think, mentioned that  gave me a little bit of thought is that we don't really have parent child relationships, right? Since we are not,  there's no such, we cannot define it. I mean, at least currently the way I see it, for example, in Excalibur,  we have this flat structure.

There isn't really such a thing as a  parent child relationship, right? Because one element in theory can reference many other elements. And like, this is not one  to one, and you know, a  child in theory could have its parent inside of it. So like, uh, I think standardizing this would also,  maybe not standardizing, but you know, this is, like, thinking about this as  parents and children  is, uh, I don't think, not really defined currently yet, right? 

So that's also something that would be It does seem like any, any attempt to, to define a kind of like exclusive parent child relationship is going to cause problems, right? You can still have, for example, an edge that is a child or a parent  edge, but you, but that's different from enforcing the, the lack of the inverse, right?

Like, like a child having its parent. As its own child, which like doesn't make sense semantically maybe, um, but it feels like it would be problematic to try and enforce that. Because then you're getting into actually enforcing like a very specific ontology of like how the stuff in the canvas can be structured.

Which defeats the whole purpose of the video. Of the, this effort?  Well, an keloid would just be a group and the children would be the things in the group.  So that's  what, how you currently have current child. Yes, yes. I mean, we do have, we do have groups and uh, we have frames as well,  and they do reference each other. 

However, I don't think that this,  um, is necessarily like necessarily.  Spec thing is more like implementation detail. And, uh, in this particular case, I don't think, I don't think it should be spec maybe, I don't know.  Well, if you import stuff and then move stuff around and other stuff moves with it, that's a great feature to have to not have everything move around, but some parts, and that's actually exactly this grouping you have, so that maps  maybe a little bit to the other groupings and other canvases. 

Um, one thing, the, so we're. As far as I can tell, we're also talking like, should we enforce certain types of relationships and like relationships all together? And it seems that, uh, it was mentioned in that GitHub discussion, like visual fidelity doesn't, um, tell anything about, Topology or anything like that.

And it seems to me that if, um, somebody was talking about, uh, say pixels in a P PNG image, it's basically like each pixel is a node that is completely independent of all the other pixel it's like not enforcing any kind of relationship between those, any objects in this case and in general, it seems that, um, like, um, canvases don't have to have any links between them.

Like all the objects. Can be completely independent. Um, and to also connect to a comment, uh, I think it was Max, uh, like if we go to a specification that where everything is linked, such as RDF, uh, and kind of on the other end of the spectrum, uh, something like, uh, roster images where everything is completely independent. 

It, it seems to me that like, we might be looking for something in between that we get some sort of semantics and some sort of rules and dependencies between, um, different concepts, but like try to make it sensible and for different tools to be able to cooperate.  Yeah, I think the result will be something like a visual part of the spec for vector drawings and bitmaps. 

Just where is what and how, what does it look like, and then a structural part or graph like part, how are things connected structurally, and then a link between them. Actually, this thing in my graph is the thing for the rectangle, and this thing here in the graph is actually the thing with the circle and the squiggle line.

So then you have three parts, the visual part, structural part, and the mapping.  And no matter what we do, I think we will end up with something like this.  Yeah, I strongly agree, I think.  In terms of talking about those sort of RDF triples, it's a question like, what are the predicates that are relevant to the, you know, set of common relationships that we would want to express and manipulate and share across these tools? 

Yeah,  to the point around, um, finding a middle ground between these, I think  the kind of naming those two sides as something like, you know, purely visual and purely structural is quite useful because I feel like What we're trying to shoot for is to, to have a spec that kind of occupies like the middle 90 percent or so.

So if you're entirely on the visual side, then maybe.  Like bitmap, like all, all this stuff that you'd, that you'd use in something like Photoshop makes more sense. And then on the other extreme, you have something like RDF that is purely expressing kind of, you know, relational, structural stuff. And we want to have a, a spec that can go pretty far in, in either extreme, but also like mix them together so that a tool that is almost entirely visual  can coexist with a tool that does express more structure and that a tool that. 

Is much more structural, like, you know, a state chart tool, um, can also interoperate with tools that you can scribble on. 

Go ahead,  Dragan. I'm wondering, uh, do we have any reason to believe that there is only visual and kind of, uh, that topological aspect, or should we be suspicious that over time there will be a third and fourth and fifth way to, that is semantically meaningful? 

If that made sense. 

I don't know the answer to that. Like auditory, for example?  Uh, yeah, okay. I mean, yeah. 

Okay, now that I started thinking about this, like, imagine you have a graph of things and as a visually impaired person you want  to have an order in which read, like, the software reads it to you, right? That's also, like, another  Yeah, I think I understand what you, what you mean, John. 

That does also raise a really important point that we should probably table for, for a future discussion, but really making sure that this spec is built in a way that is, uh,  accessible, not necessarily out of the gate, but that it, that it encodes the information that is required for tools like screen readers and other things, and potentially the kinds of things that you could have browser support for in the future, I think is, is really important.

Um,  Which I, I suppose is mostly going to be for  visual  impairment, although I'm,  I'll, I'll happily, uh, claim plenty of ignorance around how to think about accessibility there.  Also, one more thing is that, like, I think  every tool,  Someone correct me if I'm wrong, but currently every tool is more or less 2D plus  z indexing, right?

Some ordering to the elements.  I can see a lot of use cases for like canvases that are not bound to only two dimensions, right? But also for three dimensionals with like things like VR becoming more and more approachable. Why I don't think anyone here represents a. product like that or an app or a library like that, but  it could be something to look into in the future as well. 

Yeah.  I, I think the way we're going, uh, it should be  fairly trivial to, to include that use case in the spec where the main difference is that you're obviously using a third dimension for your coordinates and that something like Z or like depth ordering doesn't really apply in the, in the same way that it does in 2d.

Um, but as, as long as we're not Oh, enforcing  something like z ordering as a kind of first class part of the spec, then I think people will be totally fine to, to use this for a VR or AR  application.  Yeah, I think that's the part that's been evocative about Apple's spatial computing terminology is that sort of overlap with the spatial canvas thing and the notion of these being tools for thought and imagining a scenario in which we're in AR, XR,  Contexts and can, you know, explore that information in those ways.

And to that extent, it was really interesting that the suggestion there. I'm wondering maybe three dimensional objects or auditory, um, you know, sources are just more objects that could be expressed within this graph or hypergraph. So as long as we've we've made it.  Flexible enough that those sorts of objects could be expressed with their unique properties via that kind of property back thing you suggested.

I think this could scale, but that's definitely a wonderful idea to keep, you know, in mind.  Yeah, I think, as has been pointed out, no one here is kind of representing one of those, one of those tools, but I definitely think it's a useful kind of mental check to test whether, you know, our current thoughts would extend to that and be flexible enough to do that.

And then if they're, if they're not, then we're, we're potentially doing something or like potentially making a mistake in, in kind of the thinking around the spec. 

So we have about 15 minutes. Um,  we've, I think covered  like a good two thirds of the stuff on the, on the agenda, the, the important stuff. Um,  let's see here.  So one, one of these points is really just a, uh,  A very small aside that I don't think  warrants all that much discussion yet. Um. But I was talking to Jess and, uh, the idea came up, uh, for kind of developing, uh, like, a utility library that can be, you know, used for this spec for things like, um,  validation and potentially schema migration and that kind of stuff.

I don't know what, like, languages are being represented. It seems that most of these tools, uh, Based on some kind of web stack. So like starting with a, you know, a TypeScript library could make a lot of sense. And part of the motivation there is that it kind of, it gives us a, a point to coordinate around.

And ideally, turns into something that is a kind of a labor saving thing, right? Like that it can actually reduce the amount of work that, uh, full authors would otherwise have to do entirely themselves. Um, and I think, I think hitting that bar would be a really good one to help kind of incentivize adoption of, of a spec like this.

Um, so I'll mention that as a, I think to come back to in the future, it's not a need that we have right now, um, but I think it could have some like strategic benefits to pursue.  Um,  oh yeah, I'll also mention there is a repo up on the org now for, uh, tldraw, xcaldraw, interop. I didn't get as far with that as I would have liked.

I basically only, uh, got the two sides kind of up and running. Um, but I, I think, uh, now that the, like all of the work to do the work is out of the way, there's only a few hours to get something, something basic going there. So we can, we can look at that, uh,  more asynchronously.  Um,  So sorry, what does that  consist of?

Does it mean there's example files?  That  both tools are running or,  so the, the kind of the experiment there, or like the, the design of it is that we basically have, um, we have two clients for Teal Draw and it's Excel draw.  And then they are, they're both reading and writing to a file. I mean, they're, they're, they're actually, they're gonna be going through a, a server so that we can kind of manage the, the reading and writing of that file safely.

Um. And we're basically gonna  take  a JSON Canvas esque spec,  um, to kind of, uh, expand out interop between the two as far as we can go until we kind of hit a lot of friction and hopefully we can get some kind of informative, uh, results there. It's basically just a fork of the, uh, The very quick demo that I chucked together for the, um, TL draw Obsidian GIF to post on Twitter.

Yeah, I see there's a test, test dot canvas file. So at some point it would be interesting to see if people wants to share their test files and  we can try to load them up in different software. Cause I started producing some too, but, um, yeah, I would be curious to try to load other people's.  Yeah. Once it gets more concrete,  exactly in, in like a couple months time when we're kind of at that stage, then I think building out data sets for, for test cases would be a really valuable thing to do. 

Um,  there's, there's two more points on the agenda that I think would be  good to touch on. touch on. Um, I'm sure much of this stuff will, will turn into more future discussions and we'll kind of, we'll organize how we do that async. Um, one is a question around  how we think,  uh,  objects that are kind of unpassable by, by a tool should be handled and what, what is kind of required or Or desired to, to make the handling useful.

Um, like for example, does a tool need to know, kind of  know, or be able to compute bounding box information to kind of usefully display the space that the shape occupies, for example. Um, and then the other one, and I think we've kind of, we've maybe already moved to what moved in a direction on this, but it's the question around how we do, uh, Kind of schema scoping and whether it's sufficient to have this kind of one root level version schema Or whether we need to get a bit more granular.

It feels like a lot of the stuff we're talking about  is Easier and perhaps even requires that more kind of granular schema like the example of copy and paste Where something needs to know  you know, like you can't just paste a fragment of like, uh, a shape that just happens to match, but like has a, but is something entirely like it's type might have the same name, but it's, uh, you know, version one, as opposed to version six or something, and then it's going to be,  it's going to be passed correctly, but  interpreted entirely incorrectly or whatever it is.

So maybe some  granularity that makes sense. The other thing that that can get us.  is um,  kind of a more, I'm not quite sure like how, how you would, how you would describe it, almost like a kind of federated interoperability. That's really not the, not the right word, but what I mean is that you could have a kind of a base level of shared interop  that's incredibly wide of just the underlying core canvas spec.

But then if a group of tools that were, for example, doing state chart stuff wanted to have, you know, you know, maybe, maybe they had like a couple of shapes and a relationship that they needed to express that was like really specific to that use case that they found incredibly useful. And there was basically the same thing across those tools.

Then they could. independently kind of standardize that themselves into a, um, a very small kind of spec fragment of sorts. And they could share that so that they'd have that more kind of local interop for more specific things while having that broader interop for the, for the rest of the tools.  Yeah, I think that resonates.

I mean, ideally the core spec  Is is in line with the rule of least power, looking to Tim Berners Lee's learnings from from HTML and why that's scaled and why that continues to exist.  But I think there's something interesting there at like the object level of almost something akin to how MIME types, um, you know, enabled that kind of, uh,  alignment around a particular object type or data type or how that is interpreted or, or trans, you know, transformed or adjusted by different sets of tools that care at that level of fidelity about that object. 

Yeah. It, it also matches, um, other really successful kind of examples of protocols, like how email has this kind of relatively small underlying spec in the sense that you have, you know, only two or three kind strictly required fields, but then clients over time were able to extend that for, you know, like rich HTML rendering and that kind of stuff, which is  incrementally become standard, but they didn't, they weren't standard in the sense that they were imposed in the core spec.

They kind of came out of more local coordination because the underlying protocol was, was able to be  arbitrarily extended with other, with other additional data in those, in those emails.  Yeah, I, I, I kind of want to second, not second,  second this sentiment as, uh, in general, I think that not all the tools have to support the same features.

That's definitely, I don't think anyone's goal here. Uh,  I mean, it would be amazing, right? But like, we have to be realistic. Uh, but at the same time, it, it would be nice to have those paths of kind of,  What comes to my mind is progressive enhancement, in a sense that let's say someone wants to make a library that is perfect at rendering like mermaids  diagrams or only things that mermaid supports syntax,  mermaid syntax supports, and then you kind of export from that.

Program into another program that allows you to, I don't know, add colors to things or maybe scribble something on the side and stuff like that. So, um, I definitely think that  this idea of having like this global, like this kind of top level spec that is defines like very base level, um, things and then like specific.

Shapes or objects, uh, have separate specifications. I think that's something, uh, that would work really well, for example, for Xcode draw. 

Yeah. I think that makes  a lot of sense. Um, 

I, this is, this is not particularly relevant, but I'm just kind of thinking of like this mental model of, of how we're trying to take the, the kind of  some like middle ground of, of sorts and realizing that And this is kind of obvious, but I'll just say it out loud anyway, that, you know, there are some things in that, that are going to be, um, they're going to kind of cover the whole thing.

Like the needs to uniquely address objects applies to visual tools, exactly the same amount as it does to stuff that really cares about, about its topology. Um, but then something like.  Whether something has explicit coordinates or not, um, is something that kind of towards that, uh, kind of more structural and becomes like a, a question.

Um, and, and so I suppose, we'll,  that'll be where some of the harder decisions will be of kind of where to draw that line on the, on the edges there. Um,  but yeah, I think that broad goal of, of having the, the call back be really just the.  the most widely shared basis and figuring out what that is, um, is going to be  kind of the most important thing, right?

Because if we get that right, and we get the kind of extension, like extensibility affordances, right, then we've set up to be able to evolve over time. Um, cause I think it would be insane to think that we're going to kind of nail something that should never change for like a decade and get it right.

That would be, that's, that's just a bad way to, to do this kind of stuff. Um,  and I think like one, one question that  for me is around, uh, coordinates. Like is, you know, are,  Is that like a required field, basically, of the spec? Um, which, I guess a different way to put that question is,  Is that  something that you leave as a core requirement? 

Either, or an optional requirement? And then do you deal with that  as  like on the implementation side of, cause, cause you could go either way and still have kind of mitigation strategies for whichever way you went. If you had a tool that didn't require those explicit coordinates, they could just be kind of required to provide,  you know, they could just put everything at zero or something, um, some, some default fallback behavior.

Um, and you could also do the same thing. If you could have explicit coordinates and then a tool that didn't need them. Could ignore them or.  you know, produce them. Um,  my, my inclination with a lot of these things is to lean towards making them optional,  but I think it's probably also possible to go too far in, in that direction. 

Um, I'm not sure if people have thoughts on, on if there's a really good solution to  kind of optional versus required coordinates or like explicit coordinates. It's really important. Go ahead.  Yeah, are you thinking about a tool, like, uh, if you're laying out, um, a graph, you're doing, you might have to do force directed layout, and then if the coordinates aren't in the document, then anything that opens it up has to run this really complicated layout algorithm to even show it. 

Right. So it could be useful to have a suggestion there, uh, from the tool that knows the information,  uh, to be in the file. Okay. Bye.  Yeah, I would favor to, to make X, Y, width and height to be mandatory. So at least if I don't know how to render the node, I have, I can draw a box and then ignore the rest.

Because, yeah, if you do a graph algorithm, at some point you have X, Y coordinates. Your tool calculated X, Y coordinates, so when you dump into a file,  just put them there.  Then the tool can ignore them if they want to, but I think as an external tool, like TLDraw, we don't know what to do. You would have a stack of boxes at 0, 0, so I think  X, Y width, height for me would be really mandatory. 

Yeah, I feel like this is the heart of the wicked problem here that if you're imagining a tool that lets you maybe copy some structural relationship information from a programming language, like a  entity relationship, or even just the  property class diagram of that thing effectively by just its description of its relationship, paste that into a visual tool that's able to say, ah, I see these things are related.

I'll, I'll render that in the structure that ends up appearing as a, you know, ER diagram or as a, you know, class diagram you, you have, you know, complexity there. Like,  do you want a constellation of tools that each have unique things that they're capable of doing from this format?  But then how do you show that outcome?

Like if I have a TL draw thing, uh, that I export and I bring that into Excalador, are they going to agree on exactly the font spacing layout? It's it's infidelity there. And how difficult do you make it to enter any new tool into that space? If they have that burden of getting to that perfect lever level of render ability.

So it's, it's the heart of the wicked problem here.  Let's, let's go, uh, Dragan, then Max. Um,  um, just in that example of the force directed layout, uh, I think the information that, uh, allows you to reconstruct the state is not the coordinates itself, but kind of the initial conditions and, uh,  kind of algorithm that was running to get your layout.

Uh, and so like you have a point in time that you are trying to kind of copy between the two tools and coordinates are just,  yeah, one current, uh, derived state from it. So  maybe there are different representations to get you to the same output, but. I actually would stay away from like requiring coordinates specifically because again, maybe there is a different type of representation and just to maybe also like give an example, like if the first layout algorithm  is still running and you copy an intermediate stale to state while it's still not settled.

You're done copied something that like might end up looking a bit different in a different tool, if it's still running its own, um, layout algorithm. So just  some thoughts. 

If we have items that are not visible, then they don't have coordinates. So obviously we then allow items having no coordinates and then a visual tool having no coordinates can choose to either put them all on top of each other, run sophisticated layout, or just don't show that item because it has no coordinates.

So it makes exchange between tools, super easy. And if you have coordinates, whether derived or hand painted, Just put them in because it makes interop easier.  So make them optional, but put them in whenever you can.  What would be my suggestion? 

And I suppose that would, that would extend the same to, to, to three dimensions there where you're just, uh, the,  uh, uh, sorry, specifically, um, well, it would extend to three dimensions, but then also that, that question of kind of width and height as something desirable to have like a bounding box or something, um, if we go that route, then that would, that would extend as well.

So your, your kind of bounding box representation or whatever that would be would just match the number of dimensions you have, which.  At least to my mind, it feels like it's probably just two or three.  I don't know if, if there is a point other than kind of  being completionist to have one dimension as an op, as an option in there where everything is just on a line, I don't know.

Um, 

Well, even if you have 3d just put in X, Y, Z, and if the 2d tools imports it, it just drops the Z or use it just for Z ordering,  something will come out good. Might be useful. Maybe not, but  that's fine.  Yeah, so maybe,  uh, so maybe, uh, at least my model currently was that there's like this array of like vertical objects, but then we kind of stumble upon those horizontal things, like for example, uh, positioning, right?

So maybe those, maybe it's worth kind of specifying  them. If you have position, then. Like, you're going to follow this kind of  specification, right? If you use bounding, if you have a bounding box to provide, then it has to follow those certain rules.  Right. And that could like those horizontal things could extend well into like, for example, ordering, right?

Um,  if you want to present all of the nodes in certain order, then you use, you do this in this way, right? So those kinds of horizontal that go across all of the possible objects slash node types  that you have, uh, maybe it's worth like thinking about it that way. Okay. 

So I, I've noticed that we, we are running over time, so maybe we can, um, just end on a few notes. Happy to keep chatting for a bit, but I just want to be respectful of anyone that has to, has to head off. So, uh, as part of this, I'll, I'll obviously chuck up the, the recording, the transcript, take some of these main points, put them into the summary, and then, um, either out of that or, or beforehand, um, for listening. 

People can feel free to start some discussions. I'll, I'll, I'll definitely make at least a couple there. Um,  let's see, are there any other admini notes that I should hit on before we, uh,  before we wrap up?  I had a question about,  so I think it was mentioned in one of the GitHub discussion about the file nodes.

And in our tool, we use a lot of external files. So we have like PDF and CSV file and GeoJSON and images and movies and stuff like that. So at least a minimum, it would be nice to have the, the, either a type or MIME type stored into the file node. And then,  um, so it looks like there's. It's, it's very vague description of, but is it a URL or is it a local file?

And so then if it's local files, how do you manage those local files, those assets, which are external to the fires, like there's different tools that people just.  To upload the asset in the same folders or this path. And then it gets really annoying because between the platform,  some sometimes format might describe, uh, basically a zip, zip folders with all the asset inside. 

Uh, so there's different ways to manage the assets. Um, right now what I did some tests with exporting, I just put public URL to everything. But it's, I don't think it's really scalable to, to share files that way. So, yeah.  That's a really good point. I, I've added that to the notes. Um, and that, that second question as well, I think is really important of not just how we do robust asset handling or external references, but how to, how to make that portable in the cases where you really want that.

Um, so having, yeah, something like that option of being able to, to,  you know, package up the things you're referring to, uh, in a, in a kind of automated way. And still I'd be able to unpack that on the other side, like including a, a bundle of images and other assets with your, with your canvas file. 

But right now they had to block for me, the blocking one was a type because almost all our nodes are assets. So if I don't know what the URL is pointing to, it's really, really annoying to have to discover dynamically. Is it a movie or is it an image? And then.  Build the representation. 

Yeah. I'll add that to the notes as well. So around assets, we have the question of  how to do assets in general, how to make them portable and how to have proper kind of typing on those assets so that we, so that we know how to, how to interpret external data.  And that quickly, there was a, the drawing nodes that was mentioned in the,  in the discussion on GitHub.

And  for me, the only experience I have with drawing is using perfect hand draw tool from the TL draw guys. So that's what I use to store the information as an array of. points, but yeah, I don't know if there's other, because very quickly you go into like SVG or if you want something very complicated. So I don't know if people have ideas on how to store hand drawn notes or  drawings. 

I, I mean, I, I want to be respectful of time. Like this is a topic that's very deep for me. Um, I'm working on like freehand representation and how to store it and how to draw it and things like that. So that's definitely, there's a lot  of ground to cover there and we don't have time. It could be ignored at first.

We can say maybe 2. 1 or something like that.  I suspect that the, the number of tools that kind of  want support for that is big enough that it is something that we should include in the first spec. But I think the, The amount to discuss there is definitely, uh, we'll have to wait for a, uh, a future call. 

But I, I think it's also, it's part of a, there's a broader question there around, not just freehand specifically, but kind of geometric information like paths and, and so on. Um, or, you know, uh,  kind of the enclosing geometry of, of a shape that isn't, uh, uh, access aligned bounding box, uh, that kind of stuff.

Um, so those  questions there for, for a future one, um,  we're a nice, uh, 10 minutes over, so, uh, thanks everyone for, uh, for, for sticking around. Um, I will end the recording now. Doesn't mean we have to head off. Um, but let me hit this button. 
