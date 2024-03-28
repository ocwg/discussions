# Meeting 1 Transcript  
date: 26 march 2024  
  
this working group is about enabling interop across canvases so hopefully you're all here for that reason and we  
can all travel on this airplane together um today will be a little more unstructured maybe than some of the  
meetings in the future because we didn't know exactly who would be involved from like which projects and what their  
specific interests are so this will be a little bit more exploratory Discovery style that being said um Orion and I did  
spend some time putting together like somewhat of a structure um to go through and kind of we have our thinking of what  
would be kind of next steps for enabling interop but if other people have thoughts this is not a uh like plan set  
in concrete um or anything um Orion do you have anything to add before I kind of go through the  
agenda and we just get started I think you can uh you can go  
for it cool well I first off massive thanks to Orion for even proposing this  
uh on in a tweet and then uh I foolishly responded and said I'll help uh and so  
here we are um so thanks thanks for being the initiating energy um Orion all  
right so uh interop across canvases um as I as I mentioned we're all kind of here for that same goal um I wanted to  
start by sharing my screen real quick and  
share uh let's see yeah so open canvas working group what we're we're we're  
hoping to do is today be a little bit more unstructured I already mentioned that in terms of an agenda I'd like to  
talk about maybe uh some near-term goals and then break those goals into projects  
that we can work on like small time bound things that we could go do maybe over the course of a few days or weeks  
that would drive towards those goals um and then the last part we'll actually like talk about next steps how we could break up and work on things together but  
it wouldn't be a conversation about standards without this famous XK CD comic um one thing that we'll need to  
talk about is you know Jason canvas exists it is this very obsidian specific  
format that um that we could build on and as Orion and I were talking more  
about this yes there's a lot that would need to be done to extend it to support many of the use cases of things like TL  
draw and zwier and some of the other folks that I've seen in the room um but  
we should let's I think our goal right now is let's see if we can start from the standard even though the standard is  
only a few weeks old and see if we can evolve from there rather than creating a whole new one um and so that kind of  
leads us to like our first question uh which is to fork or not to Fork um and  
um as uh Orion and I have been working with this Jason canvas uh format and  
looking at a variety of different uh canvas types and thinking about their feature set and that kind of thing uh we  
think it makes sense to actually try to um stay with Jason canvas and evolve it  
from there we've had a few conversations with um capano from obsidian who will be  
like uh I guess following up asynchronously um on this meeting and there is some interest in seeing Jason  
canvas extended uh so we'll see like kind of how that works because right now it is a uh sort of an  
obsidian um shephered thing the governance falls under  
that um Orion anything to add here talking about  
Jason canvas Fork not Fork do you want to talk about your experiences using it  
for the TL draw um export I I think I won't for now I will  
uh I'll keep accumulating my pile of thoughts and then uh dump all those on your ones cool that works I'm going to  
bring up the chat real quick make sure that I'm not missing things there all right yes I see the chat nothing there  
yet yeah so the in terms of next steps like maybe we can go around the room  
real quick and people could talk about like just mention the name of the project that you're working on um that  
way we know kind of who's in the room um I see a few people have made their um  
have put it in their the title of their um their username or whatever and  
display name in Zoom but maybe we could just just um I'm just going to start calling people's names and if you want  
to unmute and tell us or drop into chat and tell us what project you're working on just because we have sort of have like a roster um Steve it looks like  
you're with zwier just real quick before we do that I think it'd be good if we try and keep these like 15 30 seconds  
super brief um just so that as we have this large number of people we won't take up too much time you would have to  
have a very long name of a product in order to take more than 15 or 30 seconds to say we we'll have a good amount of  
time to uh to get know each other I'm sure exactly this is just your project tell me which project you're working on Steve wibbler thumbs up that's right  
yeah dragan notebook. thanks for putting that in your Zoom Max we've got graphin  
out and CC do you want to expand on what cc is real quick what whatever that acronym  
stands for yeah so it's two things graphin out is for graphs in out so it's a graph format converter it's open  
source and CC is calano connected still in stealth mode that's a graph visualiz  
perfect great Lou has TL draw in her Zoom display name looks like Christopher  
has excal draw great to have both of those in the room Luke has UIC um which  
is a university I believe yeah right so I'm an academic I'm University of inoa  
Chicago and so we've been working on collaboration software for a long time for science basically and it's a series  
of software called sage and we are at the ser iteration Sage three got it Sage  
okay cool and then alarin I maybe misspelling your name  
but I'm not lurking project I'm just  
here to I can great um kako we've got get  
perhaps yeah uh we are working in an infinite canas where you can collaborate  
with others and also with AI so every brings its own AI to the canvas and you  
can interact with elements and the AI can also create or modify elements that's the idea awesome that's awesome  
Moritz react flow seen that project um  
Phillip you're on I don't see a name there do you want to unmute and tell us what you're working on yeah hi so I'm uh  
just um product designer from Berlin very much into the topic not working on  
a spefic specific project but just very interested cool very cool and then we've  
got Chris CAD CAD uh which uh I think CAD CAD might be the project name  
certainly a whole category of prod of products uh uh so catat stands for  
complex adaptive dynamical systems computer AED design um it's a python library for doing uh complex systems uh  
engineering simulation modeling um combining systems dynamic modeling with agent Behavior  
modeling that's super cool that's definitely pushes it in it pushes things in an interesting Direction um John  
ganella I'm trying to remember I'm trying to remember which project you were from yeah Christopher Shank and I  
are working on um basically bir directional visualization and structural editing of some little languages uh  
specifically in state charts U so a little overlap with David's work there with xate but also with high graphs yes  
that's right the high graph stuff I remember and I was looking at Chris's slides from this weekend where he uh  
described High graphs um and that kind of stuff so Chris I I assume you're working with John you have anything to  
add uh not at the moment okay cool um and then Brad mentions in chat that he's  
an independent file format enjoyer which is a great title um and yeah I think  
Elon from block science so I think that might be a CO worker of uh Orion do you  
all work together or yep he's uh he's actually right over  
here across the room great cool well that's a great set of represent or  
representation from a bunch of different projects um I think the nice thing I uh Orion and I have kind of done a a survey  
of different projects we'll have to add a couple of columns based on the some of the folks who are here today but I think  
the nice thing is I I think we're in sort of a sweet spot where Jason canvas  
can work for most of these scenarios obviously you guys are smart enough probably to opt in to something that  
would work for your tool um or could be made to work for your tool um I think  
one of the one of the ways that we've been realizing where Jason canvas and  
where we think the format could go would be is there's  
a a type of canvas where the relationship between the objects in the  
canvas and sort of their conceptual what they conceptually represent is the most  
important thing about the canvas right and that that is true of obsidian and  
that kind of stuff layout obviously does exist on a 2d canvas you have to lay things out and you want them to not  
overlap each other and you'd like them to remain relatively stationary and all that kind of stuff but there's another  
type of canvas that's more like working in figma which is is the thing that you're making in the canvas that is you  
know whether it's a a picture of some that is the important part it's not actually about the nodes or the  
relationships between the nodes or the the sort of the the information that's encoded in the relationships between all  
the nodes um it's something else and I think we are intending to support the former and I think just about everyone  
here is working on a project where the former is true um is sort of I wish I had made a tree of this I need to make a  
a graph of or a diagram of this but basically it's like is the most important thing the nodes and edges and  
relationships or is the most important thing the visualization um if the most important thing is the nodes edges then you're  
probably in the right place the next thing that we're going to have to figure out is um does your  
canvas like have an x and y coordinate or do you do auto layout that feels like  
the next Fork down the road so um in many cases something like graph viz or  
mermaid or and I'm I'm maybe some of your projects as well possibly state chart generators possibly react flow um  
the X and Y position isn't manually specified by the user of the canvas or and so you you end up having some sort  
of Auto layout um and I'm I'm the question is are we going to be able to  
support both of those in a really elegant way because right now obsidian is it is the case where you manually  
drag things around you the user puts things where they want them want them and you get an XY coordinate and so um  
that's kind of what I'm but for all of you who who've gotten here does that make sense as sort of a taxonomy like  
we're nose and edges are the most important thing and then there's a further taxonomy  
break I'm going to pause for a second I think it like the T does make  
sense uh for the use case of excal draw like I think the first one where you  
mentioned like no and edges I don't think it's actually like the main use use case of excal draw I think the main  
use case is actually like drawing like putting stuff in the canvas and sometimes you're going to use like edges  
and arrows but I don't think this is like the like biggest and overwhelming use case and so if this like the goal of  
the uh like spec is on the first one uh I don't think uh like it's going to be  
like super valuable for XK draw but at this this is what I'm getting from just  
like hearing your pitch yep that makes sense ory go ahead yeah so I I I think  
we can probably um kind of shift that border out slightly where I think figman  
might be in a in a gray area there but I think a better illustration of where that something out outside of this would  
be um the tool everyone draw right which is this big multiplayer canvas but  
you're actually basically doing like pixel art where the the the outcome is something much closer to something like  
like Photoshop it's it's entirely Visual and and there isn't any way to to even represent um relationships between  
between objects and that  
canvas yeah um if I'm understanding right um uh I guess one thing one reaction  
Viewpoint that that we had is is is like in some ways the Json canvas  
specification was was quite minimal um that would allow for like building on  
top of and but we did also sort of find that there were some things that were  
actually quite opinionated already um that would would make certain things  
like makes it hard to always be additive I think so um for example you know like  
the edges having specific um information about like their positioning um which is just not how our  
Canvas Works at teal draw really um so I mean I I don't know what we would do if  
we were to try to make it work really well with it what we would do to make it compatible it would feel slightly  
strange to I don't know maybe ignore some of those or like override them or you know there's what so  
basically um I think a big question for me is whether to do additive changes or  
whether to like go back and just sort of review what we've got so far um because  
perhaps if we from what I understand from what you said like M um we might be  
deciding what the next first chunk of work is um yeah so is that adding on or  
is that reviewing um and I don't know sorry so I I think a a common piece of  
input from the tools that I've I've seen talking about um uh the Json canvas is is like largely  
in line with that right that there are actually already some things that are too um that are too specific to obsidian  
and even though it's not the kind of change that is like preferred for spec  
it does seem like most of the good paths forward would actually involve loosening some of the con some of those  
constraints um moving them out of out of you know required fields and and making  
them optional and so on which would almost assuredly be a kind of  
breaking change um but that might be the the kind of the only path uh forward  
there if to to avoid having a a really kind of gnly additive mess where like  
the additions end up undo doing stuff that you did before yeah I think you know like this  
the spec is is great for a certain type of canvas um but now that we're we're thinking about we you know and and it's  
also great because it's brought us all together right now you know which is which is pretty incredible um but if we  
if we're TR if we're going to try to make it um something more something that  
every kind of canvas can get involved in um it's it feels like a slightly different uh design problem um so yeah I  
I completely agree completely  
agree oh I think you're muted Jess if you're talking yeah sorry about that the um yeah I think that is the big question  
for like do we are it's pretty clear that if we and and  
like Ryan said from reviewing the use cases of different canvases and talking to folks it's pretty clear that whatever  
change that we're if Jason canvas is going to make it it's going to be a breaking change um I don't think we're  
going to we can do like a um an additive change and I think the biggest one from  
my perspective is the um there's things that should we basically need like a  
properties bag on nodes and on edges that has a couple of properties to it um  
one that um everything in it is optional and two that an implementing  
canvas that doesn't uh doesn't know what an optional node is like um item in that  
property bag is should not touch or edit it or mess with it so that basically  
allows um uh each canvas to treat the properties bag is sort of like an annotation layer on this base node um  
object um and then the uh and then I think from there we can kind of start  
extending the types if you're not familiar with if you don't have the like Jason canvas memorized I do I I did make  
this spreadsheet for myself to start thinking about like what support I started with kopio for a very specific  
reason I don't know if you guys saw that kopio already integrated or uh Jason canvas export and import um that being  
said I did try it this morning and it didn't work um so I'm not sure why I was I I wasn't able to debug why it was  
visually inspecting the Jason canvas uh export I couldn't see anything that would cause obsidian to not render it  
but um yeah so another problem is going to be like how do we sort of do  
continuous integration testing over these Integrations to make sure that they continue working um but anyway the  
reason I picked kopio as well they've already they've already implemented it and two kopio is very similar to obsidian um it it doesn't support shapes  
it only supports text objects links um groups um interestingly and um and edges  
between like text objects um so very similar to the uh feature set maybe the  
most similar of any of the like the tools that I've seen um but even then there's sort of differences there and so  
I think the the big question is would the obsidian if we could release a version of Json canvas like 2.0 that  
allows us that's like signals that this is a breaking change that allows us to move some of these attributes into an  
optional properties bag um and then we have that sort of guarantee around properties that they won't get clobbered  
by other tools when they open them up I think that enables a uh a lot of  
experimentation at least to where you can start seeing whether some of these different tools can communicate with  
each other um since excal draw and te draw are both representatives from both are in the room those feel like another  
two canvases that are very similar in terms of their feature set um they have  
a very different vibe but they it feels like people the people that I talk to are kind of they either use one or the  
other um and and there's in fact on the the DXL  
team we actually have te draw people and we have Escala draw people we even have like one guy that uses draw.io um but  
the they pick these things because they have a specific feeling to them but it it feels like if we could figure out a  
format that allows canvases that are at least very near to each other in feature set to interrupt first that feels like  
the easy first step of like that's like baby steps and then we can figure out on  
how to map between canvases that have like slightly you know more and more differences between them so I was going  
to suggest as a first project basically hacking the Json canvas uh specification  
well is it possible here was my question would it be possible to use the existing Jason canvas 1.0 to have TLD draw and  
excal draw communicate something doesn't have to be the rich full feature set of either one of those  
tools and then it might be interesting to think about like okay well how would we add one more feature and then where  
would where would that what would that look like to extend Jason canvas to add that one more feature and that's kind of  
where I started with this particular spreadsheet is I was thinking okay what is in Jason canvas 1.0 and then what  
would it mean to add one more field or to make one structural change and we can sort of evolve from there anyway I said  
a lot of things there um yeah thoughts on go ahead or yeah  
just one thing kind of on this question of um how to take what already exists  
with Jason canvas which I just want to mention we're definitely not going to figure it out right now um but I think  
it makes sense that for any kind of open standard especially around interrup um  
we really need a a kind of a process of of moving forward with these changes um  
and importantly a process that is not like any one of us individually and and also ultimately long term can't really  
be obsidian I I I like to think that they'll uh that they'll come to agree with that right um so I just wanted to  
to plant that in in this conversation that uh that kind of how we longer term  
govern the evolution of any spec that we have is is also I think an important part of of success  
here yeah I think one One Step I'd like to see is like a low hanging fot is like  
can we exchange sticky notes between all those all those tools for like I make sticky note FES I export it sign it to  
the dra and it works and or the opposite even if it doesn't render the same way is fine but is that I think to me that's  
a minimore it's a rectangle with a piece of text a position XYZ and and then uh  
te drawers arrows and and and and so on I would ignore them for instance and  
like that so very low hanging forood just to try  
and yeah that that seems Luke that seems like a great thing that is in line with  
kind of what I was thinking of like uh Jason canvas right now supports text uh  
node types and so if we if uh TLD draw and  
excal draw and our Sage three or whatever are reading these exchanging  
information via canvas basically text types um are the things that they have  
to exchange um or like that that would be one of the simplest things that we could start with would be these text  
blocks um and yeah you could make those the yeah yeah you immediately get into  
the problem of um npio for example doesn't  
require uh X and Y um or no width and height I mean this should be  
optional um yeah it doesn't require a width and a height it just requires an XY position and then it auto renders the width and  
height um so yeah you get into some of those sticky things I think that's where  
I I think what you're mentioning as a project is so this is kind of moving from goals to projects goals is our goal  
is to see inter op across all these different canvases the projects the the what I'm thinking of in terms of how we  
get there is sort of taking these baby steps for in out between the two and so now would be the time where people could  
say I would be volunteering to take on X Project to try something out over the  
next few weeks and then kind of let people know how that goes and we learn from it um  
so does anybody have anything that they've wanted to try and or already trying that would kind of take a step in  
the direction of interop using the Json canvas format to begin with OR using something  
different I mean um I know or has already done like a a mini experiment  
but I I don't know if that was actually using Jason canas or if that was using um I don't know just hand hand done  
thing so I'm curious to hear about how that went from Orion  
um in the past we have done a tiny amount of excal Draw 2 TL draw um  
conversion partly for for just experimenting with is this a feasible idea  
um and that that obviously didn't  
involve a standard or anything that just involved looking at excal draw format um  
and allowing allowing people to paste it into teal draw um I I think I think the  
motivation for that was to try to you know be be an example of of  
interrup um but I don't know if that still works or not um yeah I'm curious  
from Orion uh how your inter experiment went yeah so that that was a a very  
brief experiment um mostly just to have a good video for for Twitter um that was  
using basically a subset of the the Jason canvas spec um and at least at the  
time of the video it was really only one way from ta draw to obsidian so I I just set up a a small server teal draw so you  
go from the the teal draw page to the server and then that does some um very  
very basic translation luckily um there is some amount of kind  
of shared design choices there already um um I I put together a a a spreadsheet  
of of a kind of comparison table between tools and one of the things I was looking at was um thing yeah this one  
here so if you look at the the stuff around coordinates near the the top um  
basically all of them have have made the same choice to follow what the web does with um positive X going to the right  
positive y going down um and so the fact that there were that kind of shared set  
of of choices around coordinates as well as um um both using like compatible ID  
schemes of just basically unique strings um that made it pretty trivial um and and looking at the table it seems like  
some of those Basics are are going to be shared between a lot of these tools  
already related to that um like a project that I'm going to be working on over the next couple of weeks um is we  
have a tool at DX called composer composer has a plugin for TL draw um and  
so you can draw TL draws inside composer and we also have local file uh export so  
composer is a local first notion a table mashup basically that's like completely extensible so drop like creating a new  
um plugin like a TL draw plugin is like very simple to do and so one of the things that we need to do is save those  
TLD draw files to the file system system we were currently doing that by Saving out the Json snapshot of um of te draw  
and we'd love to do that by writing it to a canvas file we know that right now that would be super lossy but um we  
could write both we could write like the Json file and the and the canvas file and just have them sitting right next to  
each other and that would allow people who are using thing using composer with say obsidian could open that canvas in  
obsidian immediately um so um if Ryan or  
someone or Lou or someone from TL draw or someone in the community wanted to add that sort of TL draw to Canvas  
export um we would be happy to like pick that up and put it in our software today  
um and then we would get to like actually experiment with that um I'm an obsidian user as well so I would find  
Value in that immediately and would be able to kind of make that part of my normal daily work and be able to say hey  
this is continuing to work right I would be the human integration test on that um  
feature um yeah I mean let me uh let me speak to the rest of the team and um and  
say that that's something that Jess Martin wants as a human and um I I don't  
I don't know um yeah let me speak to the team and I don't know what the outcome  
of that would be um but you know like that it would be great if that existed I  
think that's like you um I think the the hard part might be how much like hacky  
work is involved I think with the current Jason canvas spec like you said it would be quite lossy I think um from  
my gut reaction um from looking at it is that a lot of the the sort of constructs  
in it um I I if I was building to Target  
that I might not use I might do it in a slightly different way like maybe like  
baking in some data into names and text and I don't know some sort of  
weird weird I don't know um I think it would be uh quite hacky um but could be  
a worthwhile experiment to KCK things off I'll speak I'll speak with the  
team one um note on these kinds of next  
steps is that I think it's both a really useful outcome of this first meeting to have some specific things to SN our  
teeth into um I think it's also maybe worth mentioning um longer term  
timelines and there there's two things I I want to mention one is that it's probably going to be more productive if  
we don't treat this working group as a kind of as an interest group I mean it  
might be that as well right like we all probably love canvas stuff and and we'll happily talk about it um but having some  
kind of bounded long-term goal emerge over these next few meetings would be  
would be great maybe that's you know six months maybe that's a year depending on what what the the concrete goals are  
that we end up with um there's one more thing I want want to mention in there which is that there is  
a a more uh aspirational potential outcome  
um specifically for the tools that currently or in the future support um multiplayer especially  
real-time multiplayer which is taking the work on the file format and basically extending that to to realtime  
collaboration um I I personally would find it incredibly magical if my friends  
who who uh prefer excal draw and and and use that all the time could um  
interoperate with M draw friends um and be able to doodle on each other's  
stuff um from from different clients I think that would be that'd be great but that doesn't apply to to all of these  
tools  
here sense yeah um okay oh t uh Lou I had one more question if someone from  
the community wanted to contribute the code that does the TL draw to Jason canvas export is that possible based on  
the way things are currently set up with your project like could someone open a PR and and add that  
functionality uh let me yeah I mean like I If if um if  
someone from the community wanted to give it a give it a crack um that would  
I think that would be very valuable um uh and and the the the I think the value would be  
in in testing out and finding out where the  
uh where any limitations are and and where their scope to improve I I  
don't I don't see it being like a I think it would be quite hard is what I'm  
saying but I think it would be very V so whether it whether it's so your  
reticence isn't like this is not allowed your reticence is like could anyone outside the team even pull this off no  
no I I I um I don't know if anyone inside the team can pull it off that's why like I don't know if anyone um not  
because it's it's like um yeah not because it's you know canvases are hard  
but because you know the Json canvas spec is quite young um and so on that's  
why um but I think it would be valuable um for us to as a learning exercise if  
that makes sense at this point yeah I think that's the main thing I was thinking of is like having a version  
that works with Jason canvas 1.0 will be extremely lossy probably not even that  
useful um but it would be really interesting to say well we had here's how we mapped between the internal data  
model in this canvas and the current specification for Jason canvas and  
that's kind of where I was starting with the spreadsheet of like mapping between like actual Fields wanting to get down  
to the level of nodes in this in this program have these specific fields like  
it does this does this concept even exist in this canvas yeah yeah exactly  
and and and I just I guess I'm just trying to manage expectations a little bit with anyone who like wants to go out  
and spend like you know 72 hours straight with no sleep and uh make make this um there would it would be very  
valuable and personally I'd love to see it and um uh but the yeah the value  
would be in the learning you know the value wouldn't be in necessarily yeah we're GNA we're going to all use this  
all of a sudden yeah great and yeah you you put that really well as well I think  
cool um similar question for other folks projects was like does anybody um two  
questions really would you would it be would you be interested in or like  
having ajacent canvas 1.0 like existing version of the spec and or a here's how I would modify the spec  
if I could um like Jason C 2.0 export and doing that from the tool that you're  
working on now is like question one the question two would be is it possible for  
someone on the commun from the community that's not you or not on your team to actually do that because we can we can  
definitely put these there are other people who are going to be following along with these meetings and if we can say here's a way to get involved we  
wrote an issue on the excal draw GitHub repo here it describes the problem it  
points to the Jason canvas spec and it says good luck um and then you know PR welcome um and and kind of bounds it  
like Lou said appropriately um this is for learning it may not be a particularly useful feature to have yet  
but it will help us develop the interop that we're it's a step towards the interop that we're hoping to have um I  
guess thumbs up from other projects or feel free to unmute if you want to add additional context around that because  
that feels like a really obvious first project that will help us build towards the right  
spec I saw a thumbs up from Chris from excal draw um one question I had is that  
so you talked about optional field but is there a way to dump data into other  
field or create a a field where we can store our app specific data for now or  
something like that or yeah so I would be interested in both honestly that's why I was saying like Jason canvas 1.0  
or you could just say like there's no point at all in doing my tool without these changes to the spec and so I'm  
going to imagine a fictional Jason canvas 2.0 that has some changes and I'm just going to write an export to this  
Jason canvas it's you know Loosely based on Jason canvas but maybe it adds this properties bag like we were talking  
about um but I think the the most interesting thing that would come out of that would you be you describing why you  
chose those specific changes like I moved this in I moved width and height into the property  
bag because fill in re fill in rationalization I added these additional properties into the properties for these  
specific purposes I think this will help us like get a layer deeper because honestly I was surprised at Lou's  
response that she was thinking this would be hard um for TL draw um I I  
assumed because Orion seemed to like magically produce it in several hours from the point that we started talking  
um that it would be an easier thing but I think the why is it hard would be the  
the the thing that we need to know that we don't yet know yeah I mean yeah um is it me is it  
me yeah please go please go yeah oh sure sure um just very quickly I think part  
of the reason I think it's hard is because there's a lot of decisions involved um around like these there are  
Concepts which are in like incompatible uh mostly with te draw um  
in in various ways like uh width and height being required and you know edges  
um needing a position um on their attachment I believe I might be wrong um  
and I think the the difficulty will become will come from H how are you going to deal with that and yeah maybe  
it's just ignore it all at this point um that that's why I think it's  
hard yeah I think the the file Express relationship from the nodes and it doesn't tell you how to draw them I  
think that's probably the it's still up to the app to decide how to draw those link because I could see the yeah the  
arrows in t draw are probably very different from how it's specified but you know that the link exists between  
those two Ed those two nodes so then yeah you have to interpret a little bit  
yeah I guess I feel like the elephant in the room is what is the value of The  
Interchange and what are the products you're incentivized to produce um if you're looking at it know  
it's really difficult is that a is that a function of trying to maintain the same level of visual Fidelity so that  
someone gets exactly the same outcome at another product and is that a long-term value that's going to be likely to be  
possible to maintain so what are we trying to capture and transport between  
these different tools and what things are going to you know just by the nature of these evolving tools always be  
something that the spec would be chasing we were going to try to encode that so I'm curious is there is there  
information we want to share across these tools and I think that got to that earlier conversation about like are we  
trying to maintain the visual Fidelity or you trying to maintain some sort of information that is could be you know  
presented in new and novel and useful ways by a myriad  
tools let me call on a couple people uh dragon had his uh hand up and then Chris  
uh from a scal draw mentioned something and then I'll get to or go ahead  
all right thanks uh so I wanted to step back um and see how we approach like the  
general decision making and prioritization of different works and it seem there's a lot of ideas and uh we  
can't say necessarily that one idea is U kind of more important at the current  
time than any other uh and I was wondering if we should come up with some sort of a document where we can maintain  
different ideas that we have and then have other people uh be able to express their desire which exact project they  
want to join and then just have people kind of naturally match and go from there uh and then take some time to kind  
of see where all the different uh projects end up and then come up with some something more concrete because it  
seems to me that trying to figure out the one thing that we should all be focusing now uh might be like not so  
productive good point Dragon yeah I apologize if that's why I would it sounded like that what's what I was  
trying to communicate what I'm thinking for the projects is and then I'll I'll respond to dragon and then Orion I'll  
call in you as well um is uh this should be something that you opt in for um not  
something that you get signed up for that kind of stuff it's totally fine for us to say and I I do think it'd be helpful to have like a list of uh things  
that PE ways that you can contribute um that we can keep in a list and that I think that's something Orion and I can  
add to the existing um GitHub repository the GitHub um organization we can add a  
list of like ways you can contribute that that has a similar effect to what you were saying Dragon of like here's  
some projects that people can pick up if they want to help out um and that way we  
don't have to decide what the one thing is that we're doing but what I'm most interested in for this first call is  
people saying here's the thing that I'm going to do between now and next you know two three weeks from now like here's the here's the next step that I'm  
going to work on right now um and that's the way that I was positioning projects as not uh something we're signing  
everyone up for but individuals might say I will do this um and and report  
back basically um so yes to both of your  
things uh like we'll we'll we'll make a list and also on for the purposes of this call what would you like to  
contribute and do um Orion you Wen um you're up buddy yeah so um quickly on  
that on that last point um I want to mention that we're planning  
on having most discussion over on on GitHub discussions so that they are out in public and so that they work for  
people doing async work um and so we we absolutely intend to kind of organize a  
lot of the uh a lot of like the mess that will inevitably come out of these calls into like well structured um  
discussions over there and that will also be a place to organize around around specific initiatives and and so  
on um the thing I wanted to mention is just as a kind of point of comparison  
looking at like other specs and protocols um when we look at something  
like email part of what allowed it to evolve was the way that it was constructed to  
basically have this very very tiny set of required uh information that made that  
made the spec that that made the protocol actually work um the email does actually allow for arbitrary other  
fields to be added and a bunch of the features that we now take for granted came out of this kind of more ad hoc  
coordination on top of this very minimal underlying protocol um that's like how  
we got things like you know like Rich uh hypertext and and so on um then the  
other one is something like XML which has um support for explicit schemas and  
also ways to compose them together so we could for imag we could imagine for  
example a a future spec for canvas tools having some Bas versioned spec that has  
a very minimal set of of absolutely mandatory stuff um but then on top of  
that you can have more kind of optin specs for for example if there is some  
subset of tools that have that share a a kind of a typed input output system I'm  
I'm thinking specifically of things like um like react flow and stately and so on  
and and these uh these tools that can be used to author like executable uh node and wire diagrams and  
and and that kind of stuff um maybe there is a a schema for those kinds of nodes that allows um allows more kind of  
localized coordination um and and still gives you that interrupt where it applies without bringing all of that  
into the you know to to not end up with a kind of a spec that just tries to do  
everything and and but to still have um coordination around around interrupt for  
these for these more Niche specific  
things I see there's a lot of stuff in the chat  
here  
you're muted just sorry  
muted um yeah so I was uh I was saying that yes there's things in the chat uh  
Chris mentions that he would um be interested in or that he'll do the work for mapping between excal draw and Jason  
canvas 1.0 the what is equivalent of the Jason canvas spec based on the excal draw sort of data model um you had you  
want to speak to that Chris oh yeah I'm not I'm not planning to do a mapping so what I'm planning to do is uh take the  
xcal draw like file format and write something like the Json SC text uh  
conver spec that use the Exel one and then for each field then explain like  
what was the rational uh that was in excal draw and see if it can be generalized or change all those kind of  
things and uh then we can see if it's going to apply to like other uh like  
project and everything so the I have like strong feeling that like the current spec right now is like way  
specific in some places and like way too lose in some so uh I don't actually like  
I'm not a big fan of like the current spec as is and so I like to like I know you wanted to like figure out if we can  
interrupt with this one but I don't think it's going to be a good base for like this group of people and I think it would be better for like like actually  
coming up with like together like hey what would the spec be and then use this as more like a guidance or so this is my  
personal point of view I don't know if other people agrees no I think that's great and I think you should you should  
absolutely take that on and be very curious to look at that and then I think the other the other The Next Step from  
there once you have that is also like I mentioned looking at other canvases that have very similar feature sets to excal  
draw so TL draw I'm sure that there's a couple of others as we go through the comparison table that Orion put together  
that it would be very natural to say okay well how would this spec work for that particular canvas that's not excal  
draw so love it I think the the reality is we're headed towards some new spec  
which will either be Jason canvas 2.to or it will be a different thing um  
and that really more of that probably depends on obsidian's perspective on how to evolve the spe the spec um and how  
much change they want to make um and so we'll we'll see but I I think we're all  
kind of in agreement that some pretty major structural things need to happen um to change Lou mentions agreement on  
that one as well um yeah I was John you spoke and no one  
responded to what you said so I apologize for that I had I was looking I was managing the queue of people with  
hands up and I was I I was out of turn so I'm sorry yeah I didn't it's totally  
fine I think what we we're trying to figure out an answer to your question and I kind of posed it at the beginning  
of like what is the valuable thing that we're going to exchange between canvases  
is it something closer to visual Fidelity or is it something closer to the information about the relationship  
between the objects and the canvas and it may end up that this sort of bifurcates into two different specs  
specs that are more about the the relationship between objects and specs that are more about visual canvases that  
are more about visual visual Fidelity that's part of the the work that we're doing and trying to actually uh  
attempting interrupt in some minimal way across these tools because I think we'll find the the big gaps and we'll find the  
places where there's a lot of value there so yeah there's probably Great Value in  
how those two could project between each other even yeah this is and I'll get to you in  
a sec Max like one of my Visions for this is thinking of the visual Fidelity  
tools as almost like a layer on top of a a tool that's more about um Auto layout  
so um yeah I was thinking about like there are tools that support hand freehand drawing in fact like there's  
the best freehand tool in you know TL draw or whatever I think the library is called like freehand or something like  
that um but the you you might want that on top of another canvas that doesn't have either any freehand support or has  
less robust freehand support so thinking about a TL draw canvas layered on top of another canvas um is a really like  
annotation layers is the way that I'm thinking about this the same way you can add comments to a text file um and so  
that would be a that's sort of a dream of mine of the way that these things might interupt is that you're not actually interacting with the same  
object you're interacting with a layer on top of and each of these canvases but  
they but they're mapping anyway we'll see Max I'll let you to speak okay nice so for example what you  
just propose is exactly what happening in the graph exchange world there's the quite popular tool called y add from  
Yorks which is an auto layout editor and it actually stores all the stuff in graphml a very old convoluted XML based  
can do everything exchange form it and then it does some proprietory data extensions to stuff their specific  
styling and coloring and even SVG shapes all into that XML  
so you can drive it really far that direction and I would say about the goals for The Interchange format if we  
just can exchange let's say text and the structure between we achieved already a  
lot so you can already hard migrate from one tool to another one and lose not  
everything or send some structured stuff to a colleague and reort it and reuse it that's a big thing and taking to the  
total extreme you would have a migration format where you can completely change tools and I think to create a migration  
form it should not be the first goal because that's just too much but just  
being able to export structure and then more and more visual Fidelity on top of it is more  
achievable yeah seems one one point on that is is going back to the the email  
protocol example is that part of what made that work is that if someone introduces some new field and you send  
someone an email with a client that doesn't support it and then they forward it on to someone else else um the  
explicit design there is to not touch the stuff that you don't know anything about and I think we could actually get  
a lot out of just kind of having having that principle of you know if there is a a property own some object that you  
don't know anything about by default don't affect it at all and that and that gives you a lot of that that kind of  
ability to to bounce stuff around without worrying about your your your data being um  
butchered there's um another Point here that I want to make I I also I really  
loved Chris's suggestion of kind of writing down something resembling a spec  
for your own project um like as as if you were basically doing what what  
obsidian did I I think those would be really valuable artifacts to to  
coordinate around and we we can see where we overlap I tried to do some of that with this uh this table that's up  
on screen um but it's not really the right way to do that right cuz I was really looking at the specific data  
model which is not not exactly the same thing um but what I'm wondering is is really  
two things as as kind of potential well really one thing as as a  
potential near-term question which is are there changes that we can make to Jason canvas right now that don't just  
help us uh migrate uh into some backwards compatible spec in the future but help  
uh people building canvas systems specifically I'm thinking about people that are not in this group right that  
don't that are not up to date in any of these discussions um can we make some future where there is a a a non-b  
backwards compatible breaking future spec can can we make it can we make that  
future easier to to to handle with actions that we can take kind  
of in the in the very near future around Jason canas um that's my kind of near-term question um the the last thing  
I'll say is I'm I'm wondering if there would be value and maybe this happens after we have a kind of  
speculative uh spec design around some of these tools for the ones that that want to engage with that um well we  
could kind of uh very informally speculate around a  
future spec and actually build uh build interrupt and and build  
things around that some you know imagined Json canvas 2.0 but we don't treat it as something that we're really  
trying to specify but more as um let's imagine what if the spec worked this way  
um which would be a bunch of breaking changes it would not be useful for actual users  
um yeah those are that's all I got awesome thanks over um I'm just noticing  
that we have about one minute left I want to respect people's time for showing up today um so I I heard a couple of things I'll we'll go and  
transcribe this and talk about in next steps um it sounds like there's some work that Chris is going to do for the  
Escala draw sort of theoretical spec um I'm going to be doing some like I think  
there's looking into how TL draw might export to Jason canvas there's probably also that same work of like how would  
what would be the theoretical spec for TL draw um but we'll we'll look at that that might be something Orion and I work  
on um something that I'm already working on is the spreadsheet that's on the scen right now um I'll uh if any of you do  
what Chris is doing for your tool right a theoretical like Jason cannabis open spec um Orion and I will commit to doing  
the work of like taking those specs and trying to jam them together like like  
like putting them into a shared artifact that we can look at together and have a  
start of a discussion um start a discussion around um so that's kind of a  
couple of next steps in projects um if you have other stuff you want to volunteer um given that we're like  
running over a few been on time if people need to head out um thank you for coming we appreciate you um feel free to  
if you would like to use the Discord as a way of chatting with people who are working on projects feel free to but we're going to try to keep everything um  
any like uh we'll try to put things into GitHub discussions and keep some of this  
stuff async where people can have more of a threaded um public discussion and not have to hang out and chat all the  
time so thank you all for being here um we'll  
uh be in touch about the next time we get  
together thanks very mentioning that that we do have that mailing list as well and things like this recording any  
transcripts Associated discussion a copy of the chat um we'll bundle all of that  
together and and put it there and I'm sure we'll we'll put a link on on the website to that information as well yep  
you'll get an email all right thanks y'all by  
thanks  
