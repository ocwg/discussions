Here’s the transcript broken into paragraphs for clarity:

---

We have no agenda for today, but we are going to discuss some ongoing topics.  
So let's start.  

All right, great. We need to decide on a way to use extensible JSON. I will, just one minute, share my screen with DL draw if I can find the link. Let's see.  

We could talk about some of the built-in relations that we want to have, especially groups. And I forgot what we decided on ports. Maybe we can start with that, maybe to refresh.  

So, using my own interface for my tool, I always have to get used to DL draw with the dragging and stuff. Let's see.  

A port is a visual thing, so it's a visual node. And the thing where we have support on is also a visual thing. How are the two connected? We give the big node an extension, the OCWG port extension. And then we have an array of port IDs here.  

So we are not using relations for this.  

No, I don't think so.  

Okay.  

The other recurring structural thing that visual maps are using is probably groups, where you group things. And if they are grouped, they move together. If you delete the group, the items in the group are deleted. There is no style inheritance happening, just the visual grouping.  

We talked on the relations side about sets. Now the question is, how should groups be modeled in Open Canvas, and do sets play a role in that or not?  

What sets are groups as well, or do we want them split?  

Look, I think in the scene, there's something here about it. I'll just open the specs that we had already, just to look at what we have. I think we drafted a little bit about sets, but not about groups.  

What's the difference between a group and a set?  

Okay, a set is something we defined already. That is on the structural layer, on the relations layer. So we have the visual nodes and the relations. And in the relations, we looked at the most common relations and came up with sets. Obviously, sets of stuff are one of the fundamental primitives for relations.  

Even if they are not visually represented, we want items to be able to form sets. That's certainly useful. Now if we have a group in a visual space, we have some expectations for how that group behaves. Namely, the group is like a visual thing, you can move around, but it has no representation on its own. It's only formed by its members. That seems to be more specific than a set.  

And the set is in what layer, or do we...?  

Yes. The set is just a logical grouping of nodes. Both are relations.  

Yeah, we love both.  

So a group is somehow more specific, maybe.  

Is a group defined in a set so that you point from a group to a set?  

We could also call the other element. We say we have a set and now we open the Open Canvas file, and we see that these three items are grouped in a set.  

So then we can infer already, maybe they should always move together.  

Is there a set of visual nodes where the visual nodes should not move together?  

I think there's quite a lot of those cases, actually.  

I think sets are just like—they're such a general-purpose structure that you can use them for a bunch of different things. Like one would just be an undirected edge.  

For example, if you want to make that explicit, encoding that as a set could make sense. Or you can have collections of things where the collections are not groups in the way that we expect.  

It feels like a group comes with its own norms around what affordances it gives you in the actual interface itself, whereas a set is more like a purely structural and semantic thing.  

---

I have the same feeling, yes.  

So if groups and sets are not the same thing, what is a group? Is a group rather a visual node, or is it rather a relation?  

Visual nodes have content they display. Visual nodes usually have a position. A group seems to have neither because it's only grouping the other nodes.  

So a group is maybe more a relation as well. What do you think?  

I was looking at what happens in TL draw itself. This is now a group in TL draw.  

And what we say is this group has a position. In their implementation, it does. Like the coordinates become local to the group, which is an awesome feature because it allows recursion.  

It does seem like, in principle, the position of a group is one that's derived from its members.  

If you delete a group, I would expect the children to be deleted as well. If you delete a set, I would expect the children to remain.  

Is there anything more you can do with the group?  

I mean, I'm aware of PowerPoint, where you create groups of groups, and that's fine. So a group may not contain just visual nodes but also other groups, whatever they are.  

You can copy a group here. Then do you also create copies of the children? You really do.  

When you copy a set, I think, you’re just pointing to the set from a node. Again, if you want to reuse the set, if I copy a set, it should be a different set but pointing to the same members.  

That makes sense.  

So we said visual nodes and relations are not as binary as they seem in the beginning. We can decide on a case-by-case basis what feels better.  

So we can have a show of hands on whether a group is rather a visual node or rather a relation.  

It seems to be pretty relation-like to me.  

You arrived just at the right moment to talk about your feelings—whether you feel a group is more a visual node or it’s more a relation.  

I was listening to the last 10 minutes, and I think it still seems more relation-like to me.  

So, all right, does that fit for you as well?  

Yeah, I think that fits.  

Yeah, I think we resolved the basic group stuff. Then maybe we can talk about extensible JSON.  

The model we had last time was property bags, and they state their type as one of the properties: schema key.  

An alternative could maybe be to first put this into the TL draw.  

Yeah, I think this is what we had in the other TL draw examples last time.  

Yeah, exactly.  

And I think in another meeting, we decided we could merge schema and schema version into one.  

Yeah, similar to how we have like a JSON file with all the different dependencies.  

---

**(Shifting to detailed discussion about JSON models and implementation nuances)**

---

And an alternative to these property bags with a schema key could be prefix properties, inspired by what JSON Linked Data does.  

Like instead of having the OCWG port extension, we would have a prefix. Then we would have one object at the top explaining and mapping the prefixes to schemas.  

Which is JSON schema—JSON-LD has this. GLTF, does that use it as well?  

Yeah, GLTF does it similarly. They use minus signs for prefixes. JSON-LD uses dots.  

And in GLTF, the mapping is known to the standard. In JSON-LD, the mapping is stated in the file.  

To be fully open, putting the mapping in the file seems nice for our use case.  

So yeah, it would just result in a more compact-facing format instead of “new object, schema is so-and-so, port array space, end of property bag.”  

We could just have a property on the level of the path called “OCWG-ports” or “ports.ports” and have the array there, like so.  

Not for an edit.  

So now we—this is inside our visual node. So we have our standard properties, and in addition, we now put some extensions in the visual node.  

Now we need a property name for the extension with a unique prefix. We could just call it “ports.” At the root of our document, in order to make it a prefix property, we needed to call it “ports.ports,” so that it’s clearer.  

Where do I find the link to that TL draw?  

I’ll post it in the chats.  

In which?  

In Zoom.  

Okay.  

---

**(Discussion shifts to tooling and technical considerations)**

---

Okay, if I can find the chat… Okay, I’m looking at how JSON-LD would do this. JSON-LD always has these “@context” mappings, and that’s where they use one JSON object to have the prefix mapping to a longer string.  

Yeah.  

That’s a reasonable example.  

Yeah, I had Claw generate it for me. I put the link in the Discord.  

You do these, so it’s still—okay, I see. Each individual asset or attribute is prefixed.  

Yeah.  

And then you go to the top to understand where the schema comes from.  

Okay.  

---

Yeah, so it’s a different kind of interaction, but it can be more compact because you don’t need a wrapper. You just have your ports array right there.  

Interesting.  

Yeah, in order to make that work, there must… At the root, we’d have to ensure this was in the nodes array and somewhere have the `@context` where ports would have to be defined to something like this.  

And now this, of course, means we have a product, right? Something like this. And it’s... yeah, there’s one difference to be aware of.  

Last time, we said if we want to type a node, we just add a property bag and put an `@schema` inside. That implicitly gives this surrounding node that type.  

Here, it’s harder to type something because I can only use these extensions if I actually state something. So, in order to just type something and not say anything else about it besides the type, another mechanism would be needed.  

Yeah, aesthetically, I kind of like our approach better. To your point, it doesn’t match with our original approach where we’re talking about property types with property bags that have schema specified for the entire bag.  

So which one would you prefer, the prefix properties or the property bags?  

Property bags feel better to me, looking at the JSON-LD piece.  

Yeah, property bags are just a little bit more verbose.  

They are, but the reason I prefer them, just to be specific, is that they group together logically related properties, whereas in JSON-LD, you could reorder the JSON. The properties are sort of grouped together if you do an alphabetical sort because the prefixes naturally cluster alphabetically.  

But having them exist in bags seems cleaner to me. Imagine writing a parser for this. You could parse bag by bag, look at the schema for each bag, and that feels like a cleaner implementation rather than having to dereference every single property back to a schema.  

I agree.  

Yeah, it’s just a spectrum between very terse, nice, human-readable JSON and something that makes it easy to implement a parser.  

Yeah, maybe here we go more for robust implementations. It’s fine for me.  

Okay.  

But I think, functionally, we’re saying they’re equivalent. You could convert between a flattened JSON-LD style and the property bag style. It’s just about referencing.  

---

**(Shifts to handling schema conflicts and collisions)**

---

The one question we were circling around about the property bags is: What happens when two property bags have the same variable name?  

What do you do in that case?  

I think that can’t happen in the JSON-LD case because every property is prefixed with the schema name.  

Maybe we prefix with the schema name under the hood in our property bag version. Like, we apply a prefix that prevents variables from colliding.  

But in some cases, you want a collision. It’s by design, like inheritance, where a child class overrides a parent.  

I don’t understand why you’d want a collision.  

Let’s say I have a visual node with two property bags, and each of them has a property `A` inside, but they’re different property bags.  

Well, let’s use a specific example: having a generic arrow and a TL draw arrow. Maybe the TL draw arrow has a different type for the same property name, like a `from` and `to` endpoint.  

In 2D, it’s `X` and `Y`. In TL draw 3D, it’s `X`, `Y`, and `Z`. They might want to override the `from` property.  

I see. But if a 3D arrow is so different from a normal arrow and we have a visual node that has both property bags, then what is what?  

Yeah, what’s the reason?  

I thought I had it… Yeah, I thought I had it.  

What’s the reason?  

Semantics. The tool would say this is a 2D arrow and a 3D arrow simultaneously, which doesn’t make sense.  

I think your point is valid. If we have an application not knowing about the 3D extension, it will just ignore it, change the 2D arrow, and write back the 3D arrow as it was, with different coordinates.  

Yes, and the next reader will be slightly confused.  

---

**(Transition to adoption strategies and tooling challenges)**

---

That’s why we’re discussing expected behavior. This aligns with my expectations: if a tool understands 3D, it updates the 3D. If it doesn’t, it ignores it.  

Exactly.  

So, regarding schema extension, we found that we have no realistic way to validate a whole file. But for each extension property bag, we could describe its schema via JSON Schema.  

Yes, that makes sense. We could write tooling that extracts each property bag from the overall file and parses it using JSON Schema tooling. While we can’t parse the whole file at once with JSON Schema, we could write a higher-level tool to process individual sections.  

That might even work with JSON Schema plugins in some editors.  

What about schema inheritance? Is that a concept in JSON Schema?  

I don’t think so. We talked about it early on but haven’t revisited it in a while.  

Michael’s example, though, suggests it might make sense: if we have a 3D arrow and a 2D arrow, the tooling could prioritize one schema over the other.  

Yeah, but I think it’s still up to the implementing canvas to decide.  

Exactly. The container format only recommends behavior. Implementing canvases handle transformation logic, so we just define conventions.  

Right, if we expect 3D to override 2D, we say so. But we can’t enforce it.  

Exactly.  

---

Right, if we expect 3D to override 2D, we say so. But we can’t enforce it.  

Exactly. The role of the interchange format is to define semantics so tools interoperate. If you have a set, use this set mapping. If you have a group, use the group mapping.  

Yep, and that’s what we’re trying to express with the arrow example as well. If you support 3D arrows, update the 3D arrow object. If there’s a 2D arrow, update that too. It’s up to the canvas implementation to handle it appropriately.  

Where would we document this?  

I think we would generalize it when discussing schema extension. We’d say, “In any node, if there’s a collision, prioritize based on...” and describe it abstractly.  

Yeah, that’s about robustness. If you don’t support the feature, don’t delete its property bag—just pass it along unchanged.  

Agreed.  

I think some schemas might even allow for a more primitive representation. Even if a more full-featured version exists, the primitive version could serve as a fallback.  

True. I think we’re saying we won’t fully support schema extension at this point, but maybe we don’t need to.  

Agreed. Plus, it avoids unnecessary complexity, like inheritance-versus-composition debates.  

---

**(Discussion shifts to meta topics: adoption and buy-in)**

---

One thing I’ve been considering: How do we get buy-in from canvas tool developers? We’re starting to narrow down the details, and it might be time to bring in people experienced in spec development to review our progress.  

I’ve been thinking about that too. The whole point of interop is to get tools talking to each other. If there aren’t at least two tools adopting this, then what’s the point? It’s just another way to save files.  

Exactly. I think the strategy should focus on making adoption easy for a few key canvases. We could spend time working directly with TL draw, Scala draw, and Michael’s canvas.  

Yes, Michael’s already doing great work on this.  

Another approach is writing translation tools. For example, converting Obsidian’s JSON Canvas format to OCWG and vice versa.  

That could work well. Obsidian has a strong user base making canvases, and giving them the ability to move their data into other tools would be valuable.  

Right. We could write converters for Obsidian Canvas to OCWG, OCWG to TL draw, and OCWG to Scala draw. That would encourage adoption by both users and tool developers.  

Exactly. The Obsidian community, especially plugin developers, might find this useful. Obsidian doesn’t seem to prioritize canvas interop right now, but users and developers are interested.  

It might also be interesting to target non-visual tools, like using Obsidian as a wiki and exporting its linking structure into an OCWG canvas.  

Good point. That explores structural mapping more than visual aspects.  

Stately is another interesting candidate. It’s built on xstate and heavily used in React development.  

True. You could take an xstate diagram, annotate it visually, and then return it to xstate. That’s a compelling use case.  

Yeah, the recursion piece could be challenging but useful.  

Do we need a layout engine for OCWG files?  

You mean generating layouts for files without predefined positions or sizes?  

Exactly. That would allow tools to display these files without requiring manual layouting.  

That’s an exciting idea, but graph layouting tools are notoriously tricky.  

I know. I’ve worked with Graphviz before, and it’s a challenge. But it could be a worthwhile addition to the ecosystem.  

---

**(Naming conventions and next steps)**

---

We’ve also got some important naming decisions to make. What are we calling this? Is it an “OCWG canvas”? An “Open Canvas”?  

Yeah, and do we use a space—“Open Canvas”—or make it one word?  

OCWG is a nice abbreviation, but it’s tied to the working group. We’re not shipping the group; we’re shipping the canvas.  

Exactly.  

We already have `canvasprotocol.org` for the namespace. Should we use subdomains or subdirectories for these namespaces?  

Subdirectories might be simpler, but either could work.  

Another big question is recursion. If an Open Canvas file references another Open Canvas file, how do we handle that?  

That’ll be interesting, but it feels solvable given our asset handling options.  

I think we’ve covered a lot today. Let’s summarize our key action items.  

---

**(Closing remarks and logistics)**

---

Thanks, everyone, for the notes and discussion.  

Apologies for being late—I had band practice.  

No problem! What do you play?  

Electric and acoustic guitar.  

Nice. It’s great to see us closing in on this. We’ve narrowed down a lot of the details, and now it’s just about execution.  

Agreed. Michael, thanks for staying on top of logistics—it’s a big help.  

No worries. Tools like ChatGPT have been a huge help with my workflow.  

Same here. It’s been a game-changer for reducing busy work.  

Let’s also check out the Fireflies plugin for transcription. It might streamline things further.  

Great idea. I’ll look into it and see if it’s free.  

This call was recorded. I’ll send you all the link afterward.  

Thanks, everyone! See you next time.  

Bye!  

