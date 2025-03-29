Cloud: All right, this is OCWG meeting number 21 for those who are following along on the recording.
All right, we were just talking about getting things set up in CloudFlare,
mostly DNS and redirect logistics, not that interesting. Shall we dive into something more
interesting? What do you guys want to talk about today?

: Yeah, maybe how we handle the spec on
GitHub, because you already have some plan, I believe, in handling updates for new versions,
but I wonder if we can do it differently.

: Sure.

: Yeah, so we've rolled out two versions in the last
few months, 0.3, and we're looking at rolling out 0.4 right now. Technically, this would be 0.4,
at least. Maybe the name of this PR. This, the 0.4 release doesn't make a ton of changes,
mainly changes the namespace, and then I think there was like maybe one other change.
Max, when you did the 0.3, I commented that it was really hard to tell
what change between 0.3 and 1.

: Yeah.

: And then the idea was for the next time we would just copy
the 0.3 to a folder called 0.4, and from there on do all the changes so that we can track them in
Git.

: Oh yeah, that's probably, I was thinking we would create like a candidate branch for 0.4,
and then do exactly what you just said. Copy all the files from 0.3 into the 0.4
thing, and then we would do PRs against the candidate branch, and that way each pull requests
changes would be specific to, you could see exactly what changed versus 0.3,
or versus the previous version, whatever we branch from, and then when we've done all the
changes that we want, and maybe it's only one PR, one giant PR against that branch,
doesn't matter how many there are, once it are all done, then we merge that to main,
and that way we can use the full pull request flow. However, we don't have to do that, like
you just mentioned, if we create a branch, copy everything over from 0.3, we can use Git Hubs
manual compare feature to compare between two commits, and we can just compare to like
the commit before, we just don't get all the nice PR tools.

: Well, we can, we can copy 0.3 to 0.4, maybe just change the numbers, because they really don't
imply much, and then do individual PRs against that candidate branch to see what changes really,
I mean, that the number will change as sort of trivial, and, but we could also do it in a PR.

: Oh yeah, no, that makes sense. Now that's an even simpler process, probably, so we would,
basically we would end up with on main, like in this case, for example, we do end up with on main,
we'd have a 0.4 folder here already, even though that is not at 0.4.

: Okay, cool. Yeah, then so then we might need to just, like whatever it is that defines the current
version of the spec, we just keep that at 0 at the previous version until the new directory
is kind of fully ready to go, and then we, and that might be one or more PRs to get there,
and then we just kind of like advance the pointer to point to this new spec.

: Yeah, okay.

: Yeah, I had a different idea, but all right, but that would mean a lot of changes that
the versions that you see here are only old versions, so the spec, the files that are
under 0.3 are also in the root of this repo, and right, so when you make a new version,
you copy that the current version to, to here, so you have like on that file and the root.
Because yeah, we have spec that in my MD core extensions, all that kind of stuff,
you're saying all those would exist here at the root.

: Yeah,
then you have, I think less issues with changing version almost, so I still should do that,
have to do that, but on a lot of places, but maybe less than currently, also with pointing to the
latest version of the spec, you can always point to the main branch to the spec dot and the file,
that's always the latest version.

: It does have the advantage of, yeah, when people come into the
repo, they're always looking at, if they go into spec, spec.md always has the most reason,
it's easy to kind of find that you don't have to know what the current version is,
you just go, you can go to spec.md. Walking through that in my mind though, it seems like that would,
like how would you advance the version? Then you copy everything that you have in
the root directory, to the new directory under the spec folder, we probably need to rename the
spec folder to do something, but then you know that that's an old version and then the new version
gets created on top of the files that we already have in a separate branch, of course.

: This would make some relative links harder to maintain because then the archive versions
have a deeper nested directory structure than the main schema, if they refer to the same
cookbook which is outside of the schema.

: Yeah, that's true, I think.

: So having a directory called current without the version number and then the spec in there
would make things already slightly easier. Would you put current at the root max or
interval to 0.3 and so on?

: But actually... Here I think, yeah.

: I like the current way things work.

: Yeah, and you still have core and some other things underneath here.
But maybe the cookbook should also be part of the spec folder, it's now in the root.
That's of course also the catalog.

: I don't think I have a strong opinion on either one of these. I think either one will work for me.
I think my only request is that whichever direction we go we consider what the... I would
really like to use GitHub's PR tools for reviewing a spec change. So as long as I can see the
difference between this was the spec and these are the proposed changes, how we do it from a
directory structure is fine with me. And I can figure out how to... I'll make sure that these redirects
actually point to the right places.

: Well, given we have the technology of redirecting
to the current version, then you just type spec, open canvas org and you go to the current version
and always you see clearly in the directory in which version you are. So this is even more
explicit than just having a current or head. That was my only... My only
hesitation with your suggestion, Max, about going ahead and creating a 0.4 before we moved to 0.4
is it might be somewhat confusing unless we like make the... unless we call it like 0.4 draft or
something like that, which we could do. Like it could be 0.4 draft is on main and until we're ready
ready to ship it. And then we rename it to 0.4 as the final step kind of thing could be.

: Yeah. Because even if they came to 0.3 via the canvas spec, that came as protocol.org and they went
back to the spec directory and they said, "Wait, there's already a 0.4? Which one's current?" And we
probably do need to flag it in at the top level as well. To give a disclaimer, this is a draft.

: Yeah, and also like a current version of the spec, 0.3, which we do have here.
But maybe a little bit more explicitly.

: And is there some tooling or some other...
Very good. I do make it more easy to deal with all the changes to the version number.

: Yeah, Max, you got any suggestions on that of like dynamic variables and markdown. You've done
some stuff with things that are not marked down. Yeah, I ask you, Doc, this would be easy. But in
markdown, by one thing that is quite pragmatic is to say, we don't call it 0.3. We call it
the 0.3. And then we can easily use certain replays.

: There you go, easier than 3. That does make it easier to find, for sure.

: That could also just be some instructions that we need to follow.
For me, it was the first time that I did this with our spec.

: Right. Yeah. But if we just call, yeah, instructions is a good idea. And also calling it
the 0.3 everywhere, even in the path, and everywhere, so that it won't be confused if we have a stroke
width of 0.3 in an example file. We don't want to upgrade that with every version.

: So this might be a pragmatic way. I have a short section, a note to the editor at the end of the
spec. And maybe there we should mention how to do the next version. I basically wrote these
for myself so that I would stay consistent. And there we could also say, yeah.

: Did we arrive at a conclusion on the directory structure? Or have we just presented several
options and then we're going to choose one in terms of current 0.3, 0.4, that kind of stuff?

: So we agreed that we want to have full requests. We agreed that we want archive and current version.
We agreed that the current version should not be called 0.4 already, but 0.4 draft or
some other name. We have the option to call the current version 0.3 or current.

: Yeah, I would vote to keep the number in the directory to make it even more explicit,
given that we have the redirect technology to make things work.

: I think I agree.

: Yeah, okay, great. Cool. Then I think some real quick notes that I'm going to
take that we can add this. So when creating a new version,
copy the existing, sorry, the current spec to the next version number with draft
appended.

: And if we add the V, then we even get these in the JSON schema names and everywhere.
The V in the JSON schema. Do we have the version number?

: I don't know that the version number is in these files.
What's the file? No, it's just the directory directory. That's good.

: Yeah, that's good. One last thing to change.
That's the better. Same in the extensions. Yeah, great.

: Okay, so that's a separate proposal is preface.
All version numbers in the files with V in order to enable quick find and replace
with zero ambiguity.
Does that change anything about a directory structure? I don't think it does.
It'll just be spec 0.3. Oh, yeah, it does. It absolutely does because
yeah, this would need to be this, for example, will need to be V 0.3, which means that all of the
version numbers, these need to all be moved to V.

: And do we need to make additional changes in this file that we already have?
If we go for the V ID, we also need to retroactively change the old files to fix the links.

: Yeah, and I already had like a card for this normalizing file names for older spec versions.
So now we would need to make this into V 0, V 0.

: And that's this card. I guess I should go ahead and card a new card for what we're just talking about.
Document how to create a new version.
Create pull requests against the new V
draft bolder and still satisfied with release and then
and rename from blah blah draft to not trust. Yes, yeah, you're right.
For this part of the release, right?

: Yeah, I'll try to fill this or this issue out and get you guys to take a look at it and make
sure I didn't miss something. I just did a bunch of this other. There's like a couple of read means.
There's the canvas protocol.org website. There's like advancing a version number does trigger
a couple of different things. And I'll try to document all of them here. And that might mean
that we actually get rid of some of them and say, wait, let's not put a version there. So we don't
have to change it. I'll take this one on assignee.js. Create. Yeah, I'm gonna assign myself to this one too.

: Great. So we have the existing 0.4 PR. Anything else we want to discuss about 0.4 that we'd
want to include in the release?

: I think clarifying changes are not breaking. I mean, we just make
more precisely was always the case that doesn't require releasing a new version. Maybe just a note
and the changes. Then why are we bumping a 0.4 because of the spec changes?

: Yeah, that does change
a lot to change the name space because now what was yesterday valid implementation today isn't.

: Good point.

: Yeah, cool. That was what I was thinking of why we were bumping a 0.4.

: Okay. Yeah, so then I guess, let's see. Yeah, we'll want to change that.

: Oh, yeah. I think there's a changes section in the 0.4 one.
Here we go. So you're saying in this section, make sure that we specify that
that changes are not breaking or no enhancements or no changes to existing.
There can be changes. I was saying more or less the opposite.

: If we have the 0.4 released
and later we had a little section. By the way, the note positions are intended as global positions.
Then this would not force us to do get another release. We could just update the 0.4 in place to
make it slightly more precise. And if we do that, we could add a little note in the changes. By the
way, in 0.4, we also made note positions more precise. But we do have to make a real release
number when the changes are breaking as is right now. And we have to invest it.

: So disagree on what you just said, basically?

: Yeah.

: Okay. Yeah. So then in that case, let's see. I've already mentioned it. Yeah, a couple of changes
too. I guess prefacing version numbers with the change that we'll make. Are there any other changes
that we've discussed around the actual spec that we would want to group in with 0.4, because we
haven't officially released this yet. Or do we want to just go ahead and get this out the next day or two?

: I would cut it out quickly, because I expect very few changes to most parts. But this is a huge
change. Technically, it changes everything. Cool. So if people start building on it,
there should be a few disruptions.

: Yeah. I like the idea of getting it out quickly as well.

: Yeah.
See, update these, the aspect, no, that's right. And then it's going to be
soft update those URLs. All right. Well, we're going to get 0.4 out quickly here. And
did you have any other question? Anything you wanted to discuss, Michael, about the 0.4 PR,
you and I went back and forth on a couple of things.

: Yeah, no, it's very good to make a new version
for me to come across these issues. Cool. All right. Anything else to discuss, you guys?

: Next week is the future of coding meetup. I'm not sure yet if I already want to present something
there. It also has to do with the time that I have available on my site. I could still do it,
but keep it probably will not be as deep as I want to. But still, I don't have a lot of time
for the presentation anyway there. It's only seven minutes. So
I can't talk about all spec anyway.

: Yeah, I think you have seven minutes worth of worthwhile
content, for sure, in terms of covering the spec and showing your integration, I think will be
pretty great.

: Yeah, I don't know if I built anything more than I already have shown you guys.
Yeah, I mean, I think this is awesome for seven minute demo. Look, we have a new spec for a new
topic. We have a cool tool and even half integrated the stack already. Wow, what a blast for seven
minutes.

: Yeah, you're bored of it, but you have to remember none of the folks have not even heard
of this much less demo of it actually working. So I think yeah, definitely worth it.

: I don't know, we'll just do it.
Prepare it a little bit.

: Yeah, yep, agreed. I think it will be very interesting.
I also spoke with Lou Wilson from the other one last week.

: No, that's great. We raised a bit of awareness for the spec and also asked for some documentation
about the tldraw format, which is not yet available, but hopefully in the future.
And I will probably show something about our spec on the tldraw discord.
I have something to share because I can export to the other for my tools. So that's at least
something.

: Yeah, yeah, it's interesting. So you're and you can import from tldraw as well, correct?

: Yeah, well, I have built something. Yes, but that's not it's far from already.

: Yeah, don't worry about it. I thought you still had an import that was working with tldraw.
Because then it's funny because then your tool would be this weird shelling point for or like
intermediate. You could like create something in ocwg4. You could import something in ocwg format
and then export it in tldraw format from your tool, which is funny.

: Yeah, I think the main things that we've talked about in terms of next steps for
actually writing code were an obsidian two way to two and from obsidian to ocif.
And then the other one was some sort of ocif validation tool, allowing people to
put in a file and find out whether it's valid or not and get back sensible results.
Or in terms of error messages and things like that.

: Yeah, also last time we discussed, sorry, am I interrupting?
Last time we had this idea of an universal ocif merge. So the idea was, we have an ocif file.
This is imported to a GLTF tool, which discards everything that's not GLTF standard,
changes it, re-exports that part to another smaller ocif file. And now we need to merge
the original ocif to preserve what we had with the changes and somehow add it as a unified
okay file. And I have not thought through this. Like if a node disappeared, it was deleted.
If it's still there, are we augmented with the data we kept?
Or we merge the data, but the precedence is on the new file.

: You could have, I mean, you could do it two ways, right? You could actually say,
you could have it a flag on that command line tool of like delete on, you know, delete on delete
or replace on delete or whatever could be like the flag. So then you could basically customize
the behavior of if the node is deleted, then yes, we want to assume that that was purposeful.
And we want to allow it to be deleted from the merged file. Or we can assume that that was an
oversight, in which case we merge it back in with the original.

: Yeah, either way.
It's interesting. Is the more we need to be aware of? I mean,
superficially, it seems to be simple.

: It seems very simple.
Yeah. And then you're basically like hydrating the file with the ocif.
It seems like a really interesting first step for
round tripping into tools that don't yet support storing the property bag.

: We have this referential consistency. So the merge then no longer has a node because it has
been deleted, but another node still refers to it. So what do we do with that one? Just delete
that one extension or propagate the delete.

: So that's interesting. You're right. Do
how to deal with dangling pointers effectively? Is that a question?

: Yeah, yeah. If a node is deleted, if a tool doesn't support relations, but a node is in a relation.
We will probably need to decide on a case-by-case basis for each extension.

: Yeah. Yeah, that's interesting. You could make that an actually, that's the part that I guess
makes it more complicated. Max is like, if we wanted to support a per extension flag effectively
of like, do you propagate the delete or not? And even like a per node type flag,
do you merge it in on delete or do you allow it to delete? Do you cascade the delete?
There's a lot of interesting questions there. But I think superficially we're talking about
JSON files. And so this is two JSON data structures. Doing basically a deep merge
should be a pretty simple tool. And getting something that handles like 20% of the use cases and 80%
of the usefulness is probably pretty quick. So this is like, consider the following use case.
Someone creates an okif file from a tool, whatever, import the okif file into
a tool that doesn't preserve property bags.
Export, make some changes in the tool.
Export from the tool.
So they import the okif file into the tool and export from the tool to okif. Those two steps
is going to involve us writing a converter, right, that we don't have. But export from the
tool to okif, which will not populate.
For extension is that the tool doesn't understand.
Merge the original okif file with the modified okif file.
I guess, populating solutions that match.
Am I describing that properly?

: I think it's understandable. There's even a related case, let's say we have a tool
that keeps the property bags intact. But one of the nodes is saying I'm using ports and I'm
referring to ABC. Then C is deleted. It's no longer there, but the property bag is still intact,
it's preserved, it's still pointing to ABC. So now it would be to ask for the built-in
properties to say we can actually fix consistencies. Check them and fix them.
But for extensions it's up to extension authors to do that.

: Interesting. So what you just described though isn't really a merge, right? That's just a
validation of the file. Does it have to be funners, which I think you're right is
independently useful. This is a more complicated case like you mentioned, but the simpler case
that's also useful is look at the file and make sure that it's valid/there aren't, and then also
have what you were just saying to clean up a fixed step.

: Yeah, that's really interesting.
I did have a, but shouldn't you need to know which properties are pointers to nodes?

: Yeah, this only works. It only works if you have deep understanding into the property bag.

: Right. If you really know, yeah, this is a port extension, it's part of core, we know
exactly what's happening. It's referring to these three nodes, but one of them doesn't exist, so we
auto fix it to not point to it. Maybe. I'm not even sure that ports is in core, but it's just an
example. Or option B auto create the missing nodes. It depends.

: Yeah.
Okay.

: And now nodes here really also refers to resources, for example, so it's entities.
Yes. Yes. I was starting to say nodes in relations, and I'm like, wait, it's not just those,
it's also resources. Any entity. Yeah, probably this validation auto fix tool is even more
basic than the merge.

: I think it is. That's why I flipped over to this issue instead of the
other one. It's like, wait, we actually need this first, and then we can do the merge potentially.
But this is definitely more basic. And again, we should have,
before we even start with fix, valid or not, is a great place to start.
And the way that we've written the spec, we should be able to use JSON schema tooling
for validity, plus following the pointers, basically. Is there anything other than valid
schemas, pointers, resolve?

: I'm not sure how fine current large AC schema can constrain the value space of objects,
or if literals. But probably it has regular expressions, so should constrain everything.

: Gotcha. So there's an open question about, can the JSON schema tooling fully support
the schema? Probably it can. Most likely.

: We think so. What about consistency? Things like, we have an arrow that points to a relation,
and the relation points back to the same arrow. Not just to an arrow, it's the same arrow.
That's more than just following pointers and saying they do resolve, but they resolve to the
correct thing.

: Yeah, it's true. Do we describe that as must in the spec, or should, or?
I think we use the should language in most places.
I think we should be able to, like, we should. I think we can grep for should in the spec,
and potentially encode each one of those things in the validator.
If we have should in the spec, we should include that in the validation.
Even if we don't say it's straight up invalid, we might issue a warning.
You have an arrow that doesn't, you're not following this part of the spec.
It's valid technically, but it doesn't follow the full.

: Yeah, just a warning.
Okay, so this gives us two major action points. More outreach, more adoption, and a validator.
Yeah, and I do like that as kind of a, you know, moving that kind of to the top of the stack is,
and we should probably split this into two. This isn't, this is two issues, not one.
I was just kind of drafting in the same one here, update comment, and yeah.
Only one of you already did something with cursor and our spec to create
proof of concept validator.
I haven't, but I haven't either.

: Yeah, it's a great idea.
Technically won't be in the spec repo. I mean, it can't be. It's fine.
Motivation.
Oh,
mementation notes. There we go. All right.
So, but I do think this is the big one here, in order to issue spec repo.
And then.
Yeah, the obsidian canvas one is the other one that I want to.
Work on the generic merge is super interesting.
There is something that's several tools for JSON to JSON transformations.
I think that's this JQ, there's JSON transforms, there's JSON it, which is quite popular or was.
And maybe one of these is enough to go from obsidian canvas to okay.
It might be more or less a syntax transform.

: That's a really great question. I'm going to note that here.
JQ or similar JSON transformation.
Cool. To go from dot canvas.
And this would then be maybe highly portable.

: Yeah, that would be.
It's a great way to start. Maybe it's.
Maybe it's.
Maybe it's.
No, it's a really interesting one. So yeah, my vote would be, since we don't have anything coming
up for the next meeting two weeks from now, I vote for when we get together two weeks from
now that we kind of do a hack session and pick one of these things and actually work on it together.
And see if we can, I think, yeah, this is the main time that I have to make progress on.
And this day, usually, it's usually the Tuesdays every other, every other Tuesday,
like I spent an hour, you know, screwing around with CloudFlare this morning.
But now that we're close to getting zero dot four out the door, CloudFlare set up,
like there's some like DNS, there's like, menial stuff that's done.
It'd be cool if two Tuesdays from now, we're actually hacking on one of these things.
And I might do some hacking, like, prior to the meeting, and then we can kind of carry that into
the meeting. Here's what I've learned so far. Investigating JQ is a transformation,
or something like that as a transformation for visiting. Canvas would be a great place to start.
And or for OKF validation, like, can we use the JSON schema tooling to validate our schemas?

: Yeah. Cool. Yeah, really great idea. We should do that. Thank you.
All right. Great. Nice.
Well, folks, fun times.

: Yeah, sure. Talk again in a couple of weeks.
Yeah. I'll see you later. Have a nice day. Bye. Have a good time. Bye-bye.
