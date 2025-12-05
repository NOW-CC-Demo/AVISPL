# ServiceNow AI Foundry & AVISPL - Process Walk & Use Case Workshop

**Chris Clancy:** Say logistically,
I was given access to the AI eval instance that you folks had provisioned
and cloned down to. So I have prior to this conversation had
an opportunity to get in there, look at, generally speaking,
how your cases are oriented, look at data models,
look at what I believe to be important pieces of. Information.
So that's super helpful for context. Really appreciate you getting me that
access prior to today. OK. I wanna first make sure you can see my
screen.
**Mike Dennis:** Yep. Got it.
**Chris Clancy:** OK, perfect. OK,
so I kind of covered this in a preamble here,
but the goals for the workshop is obviously to discuss your existing
process. There's a couple of them that we'll
probably pick into review your proposed agetic use cases.
We'll discuss anything that maybe stuck out at me in the course of the
conversation. We'll land on a I build targets. For an upcoming Sprint.
Now I'm not at the techniques part yet, meaning when we go to do builds in the AI
Foundry team, usually we can. Subdivide them into things that are like
kind of classic flow and deterministic techniques.
And then there are techniques that are more a I adjacent,
whether that's using skills that ServiceNow ships out-of-the-box that we
can literally just light up and you can start to see immediate value. Using AI agents that we ship
out-of-the-box, again, things that you can turn on right away
and provide quick value. And we may get to a point here,
let's say specifically around the remote troubleshooter agent that you guys
offered, where we might need to build something
because we might need to touch a number of data points that are unique to you
that we wouldn't necessarily. Deliver out-of-the-box.
So throughout the conversation here, I'm kind of in my head subdividing, oh,
this is something we can tackle with something out-of-the-box right away with
a skill. This is something that we might have an
agent for. This is something that we might need to
build. At the end of the day, we want to bring those techniques
together to kind of deliver an outcome. Does that generally make sense?
Kind of scan with what your understanding has been to this point? OK, so.
**Phil Caiazzo:** Sorry. Yeah, I'm I'm not in my head. Yes,
sorry.
**Mike Dennis:** Yeah, sorry, we're good.
**Chris Clancy:** It's OK. And for me,
I got like multiple monitors.
**Mike Dennis:** Uh.
**Chris Clancy:** So what I hate about teams is that when I
do presenting, I have you folks as little itty bitty
avatars on the right side of my monitor. So I am trying to like, you know,
engage with you, but it's hard with like a little window.
So I do tend to stop every once in a
**Mike Dennis:** Yeah, I got you.
**Chris Clancy:** while and see. What's going on? OK, so with that. I would like to go through some of things
that that stood out at me around your existing process and I'm going to attack
these in little buckets, right? I know there's a lot on the screen here,
so. What I'm going to do here is first focus,
yeah.
**Phil Caiazzo:** So Chris, as you're Chris,
as you're highlighting there, I just want to kind of let the group know
I did invite another guy on my team just cause if we start talking about points
and clicks and specific things that the
**Chris Clancy:** Yeah.
**Phil Caiazzo:** team does, this person will be much more. Presentable than I will about what the
team actually does on a day-to-day basis. So if you see Keith Wachunas chiming in
here, that's that's my guy. So just as as an FYI.
**Chris Clancy:** Yeah, and I appreciate that.
Unless initially I'm less going to talk clicks,
I'm more going to talk about patterns. But if I don't know if some of the folks
that are joined with me on service now can keep an eye on the waiting room.
I don't have immediate access to who might be sitting there and I think I do
need to admit them. So if you see some. and you can admit them, please do. If not,
let me know and I'll do it.
**Mike Buckner:** Got it.
**Chris Clancy:** Cool. OK,
so quick data points that I noticed. I just picked on the month of November
and I'm really just going to less focus on the clicks right now,
but more like understand intake, right? So I looked at the month of November.
It looks like you folks did roughly about 15,000. in cases in the month of November.
Does that sound generally accurate based
**Phil Caiazzo:** Yep, Yep.
**Chris Clancy:** on what you know historically? Okay.
And from what I've seen in your process diagram,
it seems like it's really kind of broken into two buckets, right?
You have an alerting capability, which is firing in alerts that ultimately
materialize in cases. Symphony seemed like something that
jumped out there. Is that your primary vector for kind of
automated alerts inbound?
**Phil Caiazzo:** Yes.
**Chris Clancy:** OK.
So that was roughly 65% of the cases that you get with the other remaining 35 being
some mixture of e-mail, direct inbound e-mail,
which was like I don't know 30% and then things like tap on the shoulder manual. And portal visits,
the AI just want to make sure I had that correct.
But BI did have a quick question on the portal stuff.
So you have portal and unauthenticated users, so the people that. Are not authenticated.
Are they going to an external portal and it's feeding into ServiceNow or are they
going right to your production customer portal for that?
**Aaron Seiden:** They're going to our customer portal,
but they don't have, they're not logging in. So there we have,
yeah, we have an external form,
**Chris Clancy:** OK.
**Aaron Seiden:** but it's still on the ServiceNow portal.
**Chris Clancy:** Got it. Cool. Okay, cool. OK. So I'm done with the intake.
That was just for me to understand how cases are getting there.
So the first thing that kind of stuck out at me,
and I'm not going to focus on the case closure part of this process because that
kind of comes in from southbound, but I'm a case manager. Something just came through,
whether it's an alert or from an e-mail or other channel,
and my initial part here is I need to review the case information.
So how is that case getting to me? Is it advanced work assignment?
Is people plucking from a queue and assigning?
Could you help me understand that a little bit?
**Phil Caiazzo:** Today it's plucking from a queue and
assigning.
**Chris Clancy:** OK.
**Phil Caiazzo:** One of the initiatives that we would
we're taking on now and would like further development on is the AWA.
**Chris Clancy:** Got it. OK.
So I did notice that you had AWA on your production instance and maybe like a
service channel here and there, but it wasn't obvious to me that it was
like fully laid out and that sounds about
**Phil Caiazzo:** Correct.
**Chris Clancy:** right based off of what you're describing.
OK, so I got a I got a list. It's someone. OK, this is Peter Wychunis.
Is that the right name? OK, um, see here.
**Phil Caiazzo:** Yep.
**Chris Clancy:** Mike, are you able to add Peter?
**Mike Dennis:** I got him.
**Chris Clancy:** OK, perfect. OK, so we got a big queue.
Someone is dishing out work. Is this like a supervisor who's kind of
dishing out work or are the case agents?
**Phil Caiazzo:** We we have like a,
we have a bunch of case agents that work specifically in a queue and they take it
in, review the case, update as they need to send quotes out to
customers before we get things assigned to the ultimate case owner.
So they're filtering stuff from a global
**Chris Clancy:** Right.
**Phil Caiazzo:** perspective.
**Chris Clancy:** Got it.
Now before I get to case info complete decision point here,
I noticed a couple of personas across different process diagrams.
I noticed Case Manager which is in your case management process.
And then if I kind of Scroll down to Dispatch Manager, I see the concept of a. TSR or a TSC? Are they different personas?
**Phil Caiazzo:** Same same personas.
**Chris Clancy:** Got it. OK. So these case managers are,
yeah.
**Phil Caiazzo:** Case manager.
Case manager could be a TSR or a TSE.
**Chris Clancy:** Got it. Got it. OK, cool. But they are technical in nature, right?
**Phil Caiazzo:** Yeah, TSES are technical,
TSRS are more administrative.
**Chris Clancy:** OK. OK. So appreciate that. So the kind of the first gate here is
case information complete. How do they know today that it's complete?
Are they just scanning it with their eyeballs or they're going to different
places? Like what gets them to a yes or no in
this case?
**Phil Caiazzo:** So when a case comes in to our queue. A lot of times the contract that the room
is associated to isn't populated. Um. General case information, like, you know,
I'm opening this case on behalf of Steve, who's over in California,
and Steve should be the person that you call,
but they forget to include Steve's information.
So it's more of just kind of cleaning
**Chris Clancy:** OK.
**Phil Caiazzo:** everything up to make sure that. We have correct contacts,
correct contracts associated to the correct room that needs service.
If it's a room that's not in our database,
**Chris Clancy:** Right.
**Phil Caiazzo:** we have to go through an onboarding
process to get all that information in. But we also don't want to stop progress
on servicing our customers. So there's ancillary stuff that we do. So it's it's kind of a holding pattern
until we get to a point where we can move forward.
**Chris Clancy:** Got it.
Now when that case comes in and someone plucks it from a queue and they get to
the point of case information either not complete or complete,
do you have a sense for like with that run to? I know you have response SLAS,
but like do you get? Is there a certain window?
Are we measuring in hours and days, whatever to get to a determination
whether the case is ready for servicing?
**Phil Caiazzo:** I'll throw this out there,
but I'll ask Pete to validate it. I don't think there's any.
It depends on the the level of information that we get,
I'd say on average.
**Chris Clancy:** Yeah.
**Phil Caiazzo:** It's probably about anywhere from four to
six hours.
**Chris Clancy:** OK, cool. Got it. All right.
When it's determined that not enough information is out there,
like you'd mentioned, the contracts are wrong or are not there,
or the contact ultimately should be reaching out to is not defined well
enough. Find well enough and you need additional
info. That additional info. It sounds like some of it could go to the
customer to provide clarification, but maybe if the contract is all
squirrely or not there or unclear, that additional info request could be an
internal request. Does that sound right?
**Phil Caiazzo:** Correct. Yep.
**Chris Clancy:** OK,
so that's just a big bucket of something I need to fulfill. This case isn't here.
Customer's going to answer it, internal's going to answer it,
whatever doesn't matter. But I don't have what I need. Therefore,
we're not moving forward until the case information is complete, right?
**Phil Caiazzo:** Correct. Yep.
**Chris Clancy:** Got it. Cool.
Now the determine initial support required piece.
Let's pretend all my data is good. I'm seeing a description.
I saw things about like Extron podium panels and all this kind of other stuff
that represent pieces of equipment or technology that. May not work or may need help.
So the determined initial support required that case manager.
Are they dynamically doing like is it tribal knowledge? Is it oh,
I've seen this device before? Like how do they get to the determination
of the initial support that's required?
**Phil Caiazzo:** I think and again I'll ask one of the
reasons I've asked Pete to come on here is again he he does this every day and
he's more in tune with this, but I think it has more to do with the
box that's next to it of confirming the
**Chris Clancy:** Yeah.
**Phil Caiazzo:** customer's entitlement.
So depending on the level of contract
**Chris Clancy:** Yeah.
**Phil Caiazzo:** that the customer has with us. Will help dictate what that next step is.
So if they've only subscribed to remote support,
then we need to make sure that that case gets to a TSE who's more technical if the
customer has subscribed to full
**Chris Clancy:** Got it.
**Phil Caiazzo:** entitlement where? When we dispatch somebody,
it's already included in their contract. We'll offer to do remote,
but nine times out of 10, they just want somebody to show up on
site. So we just need to make sure that that's
all squared away. If they don't have that level,
we need to issue them a quote for time
**Chris Clancy:** I got it.
**Phil Caiazzo:** and materials to send somebody out there.
**Chris Clancy:** Got it. So this is not the point of, hey,
I know what's wrong with this thing. It's more like what choices can I give
the customer with respect to support? Meaning if they're only titled for remote,
that's the option I can give them. If they have both on site and remote that
I can give them either, right? But we're just trying to get to a
determination on what we can offer our client, is that right?
**Phil Caiazzo:** Yep.
**Chris Clancy:** Right. OK, cool. All right,
I'm going to skip past the quote needed part for a second because that seems to
be a tall own ball of wax. I will come back to it,
but I want to get to the first point around remote support and because it was
an agent that you folks suggested could be of use, right?
**Phil Caiazzo:** Yep.
**Chris Clancy:** So when and I'm actually going to pull up
the exact language here. So. We got the information we need.
Customer's entitled to remote support. We'll just pretend that's the case.
We give them the option to go, yeah, sure, you know, give it a shot, remote support,
see what we can do. I'm guessing today,
and correct me where I'm wrong. This is the part where a human is looking
at the problem statement, understanding what the device or piece of
technology that's affected is, and trying to get a sense for. Can it be remotely supported?
And what information, whether it's knowledge,
whether it's going out to a website, as you guys have described,
what can be used to build a plan to remotely support?
Does that sound roughly accurate in terms
**Phil Caiazzo:** Yep.
**Chris Clancy:** of how you do it today?
**Phil Caiazzo:** Yep.
**Peter Wychunis:** Yep.
**Chris Clancy:** OK,
I noticed that in your instance you have a rather built out association between
external SharePoint links and the cases themselves. My first question is the acronym SDCS.
Could you let me know what that means?
**Mike Dennis:** That's that's a repository where all of
our as-built documentation is stored. So that would be, you know, CAD drawings,
bill of materials, customer sign off documents.
Those are required to be completed by the installation project manager prior to
hand off to service.
**Chris Clancy:** Mhm. Got it.
So are these in SharePoint exclusively?
**Mike Dennis:** I believe that's a SharePoint site, yes.
**Chris Clancy:** Yeah, I saw, I saw a lot of them, right?
A lot of like really nicely built out. I think 35,
000 different external SharePoint links you have in there today. So. As a as a human agent in here,
I'm going to pick on Extron because it was sticking in my head like a podium
thing. Extron has a number of podium panels or
different models, right? So if the problem is my podium panel
doesn't work, I know it's for this client. Is that agent going to SDCCS to see, OK,
what do they have a model do they have in this particular site?
Is that something that they're doing?
**Peter Wychunis:** Yeah, it's part of the workflow, Chris.
It's sorry, Phil. I was just gonna say,
**Phil Caiazzo:** So. No, go ahead.
**Peter Wychunis:** yeah, it's part of the workflow, right.
So it comes in and they say, hey, we have an issue with our podium panel,
right. And maybe it's intermittent,
**Chris Clancy:** Um.
**Peter Wychunis:** maybe it's not connected. We could go,
we could use that SharePoint site to say, OK, well, what wires go into this podium,
right. And we could potentially say to the
customer, hey, we see that there's. There's an HDMI cable that's supposed to
come in or come out of that panel. Can you verify it's plugged in, right.
So that's how we would use that right to say, oh, we've got 35,
000 installations within our system, right.
We're not going to remember all of those, right. So we have to physically go over,
take a look and say what's this customer
**Chris Clancy:** Yeah.
**Peter Wychunis:** have, right.
**Chris Clancy:** Yep. OK.
And once they understand what they have and are they then going to the
manufacturer's website or other repository to see common troubleshooting
steps or does it depend on like the the
**Peter Wychunis:** 6.
**Chris Clancy:** knowledge of the TSR?
**Peter Wychunis:** All of the above, right? It could be,
you know,
**Chris Clancy:** OK.
**Peter Wychunis:** I know that this is going to be an issue
I have to go to the vendor with or I don't know and I'm going to go Google
this or I'm going to ask a an engineer to
**Chris Clancy:** Yeah.
**Peter Wychunis:** take a look at this or I'm going to ask a
field technician to go out and take a look at this, right? So we could go. It could go all of the above of what you
mentioned, right? It kind of depends on the skill set of
the agent, how they interpret that information.
**Chris Clancy:** Do they go back to um? Incidents within ServiceNow or cases
within ServiceNow prior ones for the same
**Peter Wychunis:** Yeah, we try to,
we try to make that as a checkpoint,
**Chris Clancy:** account, so.
**Peter Wychunis:** right. So if an issue comes in and it,
you know, we look at the location history and we
could see how many work orders were
**Chris Clancy:** Mhm.
**Peter Wychunis:** dispatched on that, right.
Or not only dispatched, a work order could represent a remote
engineer taking a look and working with the customer or a field technician going
out to site, right. So. Podium issue comes in,
maybe the customer says, hey, this happened again, right?
Or maybe they just say, hey, we got this issue in this room again.
We would go hit that location. We could see all the resolution notes
that were provided for that.
**Phil Caiazzo:** So to expand on that a little bit, Chris,
that's done in that queue that we talked Gotcha. about up front.
So stuff comes into that queue. And one of the things that we asked that
team to do is, hey, has there been any tickets open on that
same room for the last six months, three months, whatever it might be? They're going back and doing a quick
history review of, yeah, we have 5 tickets. Oh,
they're saying a podium here. There's a podium here.
Let's see what happened, how did they resolve the issue the last
time and and kind of putting all that information into the new case so that the
new case owner is aware of, hey, this is a recurring issue.
Here's what we did before to resolve it so. That saves on a little bit of
troubleshooting steps up front, gives them an idea of kind of what's
already been done, maybe isn't working, and things that we need to do going
forward.
**Chris Clancy:** But the human in this case is the
interconnected tissue, the research agent in this case to kind
of do that and place that there for like.
**Phil Caiazzo:** Yes. Correct.
**Chris Clancy:** So we're looking at a couple different
ways. Is there a history that someone could
connect some dots on in the case? What do we know about this customer
specific piece of setup relative to the case?
And is there any well-known troubleshooting guides out on the
manufacturer's side? And can we bring that all together to
come up with at least a first pass of a reasonable set of troubleshooting steps
remotely?
**Phil Caiazzo:** You do all that and I call that utopia.
**Chris Clancy:** OK, um. Bye.
**Peter Wychunis:** Agree. You could send me your address.
**Mike Dennis:** OK.
**Chris Clancy:** Well, so here's the good news, right?
This research and investigation pattern, it's in your industry,
it's in financial services, it's everywhere.
Humans are going somewhere to read a bunch of documentations and come up,
make a call in the moment and usually everybody. He's busy.
Sometimes they're more complex than others.
It takes a while to get to a determination.
I'm guessing you're no different, right? Like probably.
Would you measure it in hours or it might take a day or two to get to a point where
you have a sense of what could remotely be done?
**Phil Caiazzo:** It's ours, but again,
some of the more complex ones when if you go back to that STCS,
some of the information isn't there. It might be in a separate folder that you
know these five people know about and there's there's a little bit of
standardization there that hasn't happened,
but we know where all the skeletons are
**Chris Clancy:** Yeah.
**Phil Caiazzo:** are hiding in the closet. So we go look in the closet.
**Chris Clancy:** Gotcha. OK, got it.
Now on the remote support piece, there's going to be.
So I worked in as a managed service provider early in my career,
so I was doing help desk stuff. And So what resonates with me is
sometimes people are like, I don't know, like I don't know what this cable is,
what's an HDMI like that it exists.
**Phil Caiazzo:** Correct. Yep.
**Chris Clancy:** So they may be kind of cattle shoot it
into OK, that's my support agreement, remote support, best effort,
remote support. Would you say that like I'm trying to get
a sense for the volume of your cases that ultimately get to this remote support
triangle? Do you have a sense for that?
**Phil Caiazzo:** Yeah,
we're we're trying to obviously get more to that point.
I think if I look back historically this
**Chris Clancy:** Yeah.
**Phil Caiazzo:** year. We're trending more towards that than we
ever have been. Dispatch is still a huge part of our
business and and Mike's team is the team that we dispatch into the field.
But what we're trying to do is obviously take on more of that remote
troubleshooting on the desk because one, it saves the truck roll,
which ultimately saves us. Two,
it provides a quicker resolution to our customers because I can solve something
in 5 minutes versus A2 business day SLA.
**Chris Clancy:** Right.
**Phil Caiazzo:** So there's a lot of benefits to doing it.
The tools that we have available to us now,
the entry points in the customers environments we have more so than than we
ever have.
**Chris Clancy:** Yeah.
**Phil Caiazzo:** So it's trending more in that way.
I don't think we'll ever be, you know, 100% remote able to resolve stuff.
But if we're trending more towards 50, sixty, 70%,
I mean that's that's a godsend for us.
**Chris Clancy:** Got it. And trend, where are you at now?
Like you're saying trending towards 50, 60, 70%, what would you say now is 20%?
**Phil Caiazzo:** I'd say we're probably. And I'm gonna throw a blind dart at a
dartboard here. We're probably 50%.
**Chris Clancy:** OK. All right, now if.
**Mike Dennis:** And and that considers all cases though,
Phil, right?
**Phil Caiazzo:** Yes.
**Mike Dennis:** The Symphony cases and all and all of
those things that OK, it's an important distinction.
**Phil Caiazzo:** Yeah. So and and that's a good point,
Mike. So the 15, 000 cases that you referenced earlier,
so out of them probably 70% of them are are Symphony alerting tickets or another
monitoring tool that we have that just. An alert that creates a case, right?
So when that happens,
**Chris Clancy:** Yeah.
**Phil Caiazzo:** we absolutely have remote connectivity to
our customer's environment and we try to do everything we can to remotely resolve
those issues. The other 30% I would say. 50% of that 30 is where we're trying to
get to to be successful in being able to remotely resolve those issues.
**Chris Clancy:** I see now on the alert side,
I didn't dig in. I I got access yesterday so I couldn't
dig into everything, but is it every single alert gets a case?
**Phil Caiazzo:** Yes.
**Chris Clancy:** OK,
so I've noticed in some of them like my latency is 292 milliseconds case and then
another alert comes in. My latency is 0. Congratulations. Is that also a case?
**Peter Wychunis:** Yeah, I don't think so, right?
**Aaron Seiden:** If it's on the same device,
it won't open a new case like,
**Chris Clancy:** Yeah.
**Aaron Seiden:** so you'll get an an event within the case
saying it's resolved, right? So yeah.
**Phil Caiazzo:** Right.
**Chris Clancy:** Got it. OK,
but too many of them ought to resolve themselves. Like, hey,
I was slow for a little bit. I'm good now. Like nothing to see here.
**Peter Wychunis:** Yeah.
**Aaron Seiden:** Yep.
**Chris Clancy:** OK.
I want to flip to the data for a second. I'm going to go back to the remote
support side of the house here. So you obviously have a production
repository in SharePoint for SDCS, right? Do you have a developer tenant or a
tenant that we might be able to hit from? Your eval POC instance.
**Aaron Seiden:** We do,
but that just that would involve our IT
**Chris Clancy:** OK.
**Aaron Seiden:** dev team to kind of help you configure
that. That's all Chris, so.
**Chris Clancy:** Yeah, OK. So here's the reason I ask.
Without getting too much into techniques, but I think this is probably the right
point to start introducing it is we see a lot of times,
like I talk to a lot of clients who are like, hey, listen,
my knowledge is not entirely within ServiceNow. We want it to be,
but it's not. So we have it in Confluence and JIRA and
SharePoint. And all this kind of stuff.
And that extends to documents too, right? So if there is a,
we'll call it a dev tenant that has a much smaller amount of data,
just something that I can prove that from ServiceNow I can index that particular,
let's call it just a single folder. Folder and then that index data now
becomes something that an agentic system can query.
So if I can pull that data in or I can access a dot or a picture,
I can start to do some interesting things. About, let's say,
interrogating a picture of a network diagram. I can use AI to say,
tell me what's going on. This is the context of the problem.
This is a schematic or a diagram of the customer's environment.
Extron podium panels in here. What model? OK, it's the 250. All right,
great. Now I know it's the extra on 250. I'm making it up.
Now I can also index external content from website providers and say, hey, look,
I got a 250. You're wide open in the public.
What are common troubleshooting steps for the 250 in the context of the reported
problem? So now you start to see as you're. Catching data points that may not
necessarily live on ServiceNow to come up with a hypothesis.
So these are just like a little glimpse into some of the techniques that can be
done, but the external website stuff, because it's public,
I can go crawl it without needing any interaction from you folks or any help
from IT. But the SharePoint stuff is going to be
something that I'm going to want to work
**Phil Caiazzo:** That that'll be, I'll tell you,
that'll be the most challenging one that
**Chris Clancy:** with you folks on.
**Phil Caiazzo:** we we come across, right?
Because obviously everybody's very data sensitive and secure and it it's
obviously a conversation we want to have with IT. Just bring bring your boxing gloves,
cause it'll be a battle.
**Chris Clancy:** Do you get a sense that the individual
artifacts themselves are the subject of this sensitivity?
**Phil Caiazzo:** So the way I think it's it's probably
more along the lines of the way that we structure that SDCS folder is you know we
have at a from a hierarchy perspective we
**Chris Clancy:** Uh huh.
**Phil Caiazzo:** have a customer, a job number and then. Information within that job folder that
could be could be potentially sensitive, such as customer pricing, customer name,
all those types of things.
**Chris Clancy:** Huh.
**Phil Caiazzo:** When you get down to the, you know, hey,
there's an extra on in the auditorium, nobody's going to really want to care.
But if there's IP addresses and usernames and passwords and that kind of stuff in
the folder.
**Chris Clancy:** Yeah.
**Phil Caiazzo:** That's where it gets a little bit
sensitive.
**Chris Clancy:** So maybe when we cross that bridge,
this is a quick Sprint. It's not going to be a production
deployment. So what we're looking here is to
demonstrate patterns and the pattern is can I talk to a external source and see? We'll pick examples,
just see a network diagram. Maybe it doesn't have usernames and
passwords or something, and then use that data,
interestingly enough,
**Phil Caiazzo:** Oh.
**Chris Clancy:** within the context layout, right?
**Phil Caiazzo:** I'm sure what we could probably do and
and I'll I'll say this and Aaron's
**Peter Wychunis:** It.
**Phil Caiazzo:** probably going to ping me on the side and
say shut your mouth, Phil.
**Chris Clancy:** Yeah.
**Phil Caiazzo:** We could probably pick out, you know,
create a location, pick out a job folder and put some
documents in there that aren't necessarily sensitive but would be
impactful for purposes of this discussion. Drawings, et cetera, et cetera,
and use that kind of as the use case for
**Chris Clancy:** Mhm.
**Phil Caiazzo:** what you're trying to do.
I would assume we could probably do something like that.
**Chris Clancy:** Gotcha. OK.
**Peter Wychunis:** I would also think that our folder
structure within that SharePoint is it's there's a naming convention to it, right?
So it's, you know, folder 0, folder one, folder 95.
Folder 95 is what has the schematic, right? It doesn't have the IP,
it doesn't have the passwords, right? So I'm sure you know AI could do things
like that. to navigate directly to a specific point
and not go to folder two and not go to folder three. Yeah,
it's it's always the same, right?
**Mike Dennis:** That's a good suggestion, Pete.
**Aaron Seiden:** Yeah.
**Peter Wychunis:** Or at least it should always be the same.
If everybody downstream does their does their job correctly,
they put everything where it needs to be. Folder 95 is where, you know,
call it AI needs to hit.
**Chris Clancy:** Yeah,
so there in the what I'm referring to is called like external content connectors.
There is the facility to only crawl certain paths, right? So. That is kind of like a production design
decision for you. We'll figure out what's the right way to
go. The easiest path might be you have a dev
tenant with a site with a folder structure and that only contains the non
sensitive folder structure like it's directionally accurate to what you would
have in production, but it would only contain the folders
that. That have non-sensitive data and that way
we don't. And then when you actually get to the
point where you would actually deploy this,
then there'll be a little bit of effort that you need to go, OK,
when I set this up, I want to crawl this folder,
I want to crawl that. So just trying to kind of I got to,
I got to marry this all with what can realistically be accomplished within a
relatively short build window. Right.
And we don't need to sort out the logistics of this specific topic right
now. I just wanted to, as I was looking at the agent that you
folks proffered earlier on and in talking with you about the time that's spent
trying to hit all these different pieces of data to get an opinion created,
I think it was great that this is probably a good place. To like start with an agentic build. Alright, other thoughts, questions,
comments on that. I I have more but.
**Mike Dennis:** And just to add to that one bit, I mean,
I think the two pieces of information that would be most helpful that live in
SDCS would would be, you know, the as-built CAD drawings for the space
as well as the bill of materials so that the system knows exactly which devices
have been installed because lots of issues. Relate to how those devices are
interconnected, right? So understanding where a failure point
could possibly be. I don't know, Pete, if those are in the same subfolder within
the job folder or in two different places, but maybe maybe that's just something we
can look at because I think that is again
**Chris Clancy:** Yeah.
**Mike Dennis:** those two bits of information. That would be pretty important.
**Chris Clancy:** Are those CAD drawings in actual CAD
format file extensions or are they images? Like.
**Phil Caiazzo:** Yeah, they're they're CAD drawings,
I believe.
**Peter Wychunis:** A PDF file generally.
**Chris Clancy:** Oh, OK, good. Yeah,
that's what I was getting too. Yeah. OK, cool. Perfect. And the Bombs PDF as well.
**Mike Dennis:** I believe so,
because it should be an export.
**Peter Wychunis:** No.
**Mike Dennis:** Is it a spreadsheet, Pete, or is it a PDF?
Because it's an export from from Beaker.
**Peter Wychunis:** I I think it's a I think it's a
spreadsheet. If we need to know, I can go check.
**Chris Clancy:** At some point, yeah, yeah, it doesn't.
It's not like super hot item. OK, so SDCS,
**Peter Wychunis:** OK.
**Aaron Seiden:** Mhm.
**Chris Clancy:** I'm going to veer a little bit off course
for a second because A, you brought it up around knowledge
management and B, it was something that jumped out at me. So um. I saw knowledge bases within your
instance. You have a little, maybe a little more than 1000 articles
that look like here. My first question is, I know we're getting at the end of the
resolved part of this. What is a human doing today to make the
call that knowledge article is needed and are they doing it like routinely?
**Aaron Seiden:** I they there's we're not currently doing
that Chris. The knowledge base is not being updated
proactively through case management activities today.
This is this was kind of where we wanted to get to when this process was created
and there was a point in time right Phil where we were but that was probably in. While we were still in Salesforce,
but yeah, today it's not curated. Chris, we don't.
Those those articles are probably legacy, haven't been updated in a couple of years,
so.
**Phil Caiazzo:** Well, the articles are,
I I think what Chris you're saying is do we create knowledge base articles based
off of specific case resolution and notes for women cases, right.
And the answer to that is no.
**Aaron Seiden:** Mm.
**Phil Caiazzo:** What we do do is we will manually create
a knowledge base article. Um.
**Aaron Seiden:** Right.
**Phil Caiazzo:** It it's just not consistent and it's all
manual. It's all personal, right? So if I if I'm doing something and I
remember to create that article because I think it's something that's worthwhile,
I'll go in, I'll create the article and I'll hit
submit and then it goes into goes into the ether and. People approve it and it goes into the
knowledge base, right?
**Chris Clancy:** Yeah.
**Phil Caiazzo:** So there's no consistency in how we're
doing it today, which is a 2026 initiative for us is to
standardize and get that more cleaned up and more consistent for not only our
internal teams, but for our field techs as well.
**Chris Clancy:** So it's been my experience that like. People want to share knowledge,
but they don't love creating knowledge because they have a day job,
they're super busy like and they'll get to it when they can if they remember.
So a lot of times if you can provide a facility. That is literally like, hey, look,
there's a knowledge gap here. What do you think of this?
Does this look right? Like presenting it for them and then
kicking it off to whomever is in your knowledge management approval pipeline
that tends to get more success. And the reason I say this is that we. For a I in specific,
like knowledge is a real accelerator, right?
Not everybody has knowledge on ServiceNow, not everybody has perfect data.
But if you start to enter this and I'm preaching a little bit,
sounds like you guys already know where I'm going with this,
but there is a little bit of a virtuous loop here if you reduce the friction to
create meaning. Full and relevant knowledge.
That knowledge is making its way into your knowledge base.
You are reducing the reliance on tons of external systems that may be sprinkled
around and maybe siloed. It just it reduces some friction over
time. So one of the goals that we look at here
at ServiceNow is like. How do we reduce that friction?
We have techniques that we use just using out-of-the-box A I skills that we
literally just flip on and it looks at the resolution notes,
it looks at other data points and it will create knowledge and make the human less
of a OK start from the beginning, start typing this out and more like does
this look roughly equivalent. And maybe they need to go in and make a
couple tweaks here and there, but it's not like a net new creation
effort. People tend to like engage with that a
lot better. So if it's a goal for you for 2026,
this might be something that we turn on in the eval.
**Phil Caiazzo:** Absolutely.
One of the things that in in the process of working with us,
you'll you'll quickly understand that change in this place is very, very slow.
It's it's slow to get approval, it's slow to get adoption. People are very set in how they do their
job. You know, they they like these ten keystrokes.
Even if you can reduce it to five, I'm still going to do the 10 because it's
what I know. And you know,
**Chris Clancy:** Sure.
**Phil Caiazzo:** it it takes a lot for the team to kind of
change how they do things, even if it's more efficient. It's the right way to do things.
We're slowly introducing those things into the team to make it more efficient,
productive, et cetera. And these things are going to help us.
So anything that you can do to add efficiency there is obviously something
we're interested in. It's just an adoption standpoint, it's. It it's tough.
**Chris Clancy:** I totally get it.
I've worked with small accounts, smaller account.
I'm not saying you're small. I'm saying I've the spectrum all the way
up to multinational investment banks. Everybody has that same problem as you
might imagine and. What I've noticed is,
and part of the reason, like you may have thought,
and I know you were mentioning in the last call, it's like, wow,
that's a lot of detail to go through for a relatively short effort, right?
Like there's a lot of questions for a lot of different parts of the process.
It's been my experience. That if you if I don't understand how
humans use this and I tried to build them a really nice mousetrap and it's not
relevant in the course of how they actually do their work,
all we have is a nice mousetrap that gets no adoption.
So adoption and ease of use is like kind of paramount here. So I appreciate you giving me the road to
ask these types of questions. I wanted to touch on the this box right
here. Actually, now I lied. So all right, we have an opinion on the steps that
should be taken. The case manager, the slash TSR, slash TSC, whoever's. Owning this case in the moment,
they are the ones doing the basic troubleshooting directly. Is that right?
**Phil Caiazzo:** Yes.
**Chris Clancy:** OK.
And my question here around existing problem known error,
is that something they look for before like somewhere further upstream in this
process or? I guess we're trying to figure out like
one of the patterns we see in support is OK, I'm ready to support something.
Is there something already out there that I should be aware of so I'm not chasing
like or burning a bunch of time troubleshooting something?
And in the graphic here it seems to be after doing the troubleshooting.
Usually I see that happening before. Actively engaging in troubleshooting.
So do you know, like if our humans going in right now and
looking at, oh, there's a PRB or there's a known error?
Is that happening earlier on in the process or is it really happening at this
point?
**Peter Wychunis:** I I think it's fair to say that that box
should be before the one that comes prior, Chris, right? So existing problem, right?
We get a notification from Polly that X firmware is gonna cause, you know,
Y device to do this, right? Issue comes in, we've notified the team,
hey, if you see this issue, you know. Let let it be known there's an existing
issue. This is the fix. This is what we need to do, right?
So that that definitely happens prior to the perform basic triage troubleshooting.
**Phil Caiazzo:** Perform basic troubleshooting is is kind
of like an all-encompassing and then we're just giving a little bit of detail
after it. So you're right,
**Peter Wychunis:** Yeah.
**Phil Caiazzo:** it should come before.
I think the intent here was just kind of we're doing these things here and here's
a couple of the things that we're doing.
**Chris Clancy:** Gotcha. Yeah.
And the purpose was not to poke at the document.
It was more so I understood like realistically where it lands, right?
For sure. Now where are you?
**Phil Caiazzo:** Yeah.
**Chris Clancy:** This might be obvious once I get a little
more time in the instance, but where are you tracking your existing
problems and known errors? Are you literally have like PRB or? Um,
like a node or like I know you're not maintaining knowledge doesn't sound like,
but where would that be landing?
**Peter Wychunis:** If it's a major problem,
we will create a major ticket, right?
**Chris Clancy:** Mhm.
**Peter Wychunis:** That case.
And then we'll tell the team to if you receive a case that relates to this
problem, here's your child case.
**Chris Clancy:** Yeah.
**Peter Wychunis:** Like you'll put this parent case into
this child case field. Or I'm sorry, in your case, there's a. A parent field.
You would put the parent case number into that field and then we could go take a
quick look at all the issues we're having that could potentially be related to that
problem.
**Chris Clancy:** Would there be value in kind of short
circuiting this in that if you have a major case that is descriptive of this
major problem that's known? Like auto assigning or not auto assigning
auto associating as a child of an existing major case like earlier on in
the process.
**Peter Wychunis:** I yeah, I think,
I I think if it the criteria of that case meets, you know,
what we're defining as the problem case, right? Yeah, why not?
And then obviously we could disassociate it if it ends up not being there, right? Right.
**Chris Clancy:** Yeah, once I can hear. All right, cool. OK. Alright, um. OK, so. I really wanted to land in this lane here,
which we've been doing. I did have just like a curiosity question
here around user issue request. What does that mean specifically?
**Aaron Seiden:** We effectively the inbound ingest for all
of our issues for a customer or any of our requests is a case.
So that's just differentiating whether it's actually a break fix or just a
request. We're just not using formal request
records for a lot of the work that. Phil's team uses or does.
**Phil Caiazzo:** So this this it it.
**Aaron Seiden:** Does that make sense? So it's not. Yeah,
go ahead, Phil.
**Phil Caiazzo:** This is kind of one of those things where,
to Aaron's point, everything comes in as a as a case,
which isn't necessarily best ITIL type
**Chris Clancy:** Mhm.
**Phil Caiazzo:** practice. In an ideal world,
a user request would come in as a request. A customer issue would come in as an
incident A. Device like Symphony that monitors our
customers environment and something goes wrong there,
it would come in as an event or an alert and that's how we would differentiate
everything. But today everything comes in as a case
and we move those cases around to the
**Aaron Seiden:** Yep.
**Phil Caiazzo:** appropriate groups.
**Chris Clancy:** Got it. OK. Thank you. That's helpful. Around technical escalation, so. Is that so?
I could interpret that a couple of different ways.
How do you interpret a technical escalation in this context? Meaning for me, let me put some context.
I'm the case manager. I've looked at it. I'm not sure that I can solve it.
I don't know what to do. So then I need the bat phone to a second
line for them to do something. The other way I interpret it is that the
customer is like really hot and they're like, I don't want the first line person. And I haven't had good expert over the
case. Maybe you've heard the story a million
times. Get me to the engineer or the second line.
So that's what I'm trying to understand what this means.
**Phil Caiazzo:** It's it's both.
**Chris Clancy:** OK. OK. And then you got a second line here,
which is gonna kinda, they're gonna do their tier of things and
they have their own troubleshooting management process,
which not really going over in this particular one here, but um, OK, got it. UCC engineer only gets involved when
programming is required, when it's determined programming is
required. Just curious when when you say
programming like have to get in there and
**Phil Caiazzo:** Mm.
**Chris Clancy:** like write code like modify an
application. What do you mean for that? Yep.
**Peter Wychunis:** Yeah,
it's not necessarily always programming. Chris,
just to clarify that about 98% of the time it is,
but there are UCC engineers that might be, you know,
network specialists or specialists on a specific product,
but that's that's a very small
**Chris Clancy:** Yeah.
**Peter Wychunis:** representation.
It's generally programming.
**Chris Clancy:** Got it. Got it. OK, cool. OK. All right.
So this makes sense to me. Let me go through my.
I had a bunch of questions, but I have to stare at another monitor
for a second. Sorry about that. Or I got that. On the knowledge article stuff,
there's a knowledge management process today that is that mean there's like a
group that is handling the authoring, the publishing,
the retirement of knowledge.
**Phil Caiazzo:** Loose and informal, but yes.
**Chris Clancy:** OK.
Do you folks keep knowledge anywhere outside of ServiceNow?
**Phil Caiazzo:** Yes.
**Chris Clancy:** Where are some of the places that you
might keep knowledge there outside of now?
**Phil Caiazzo:** So we would have like an we have internal
SharePoint sites for that might reference
**Chris Clancy:** OK.
**Phil Caiazzo:** customer specific information that would
reference team information. I'm trying to think of examples. Selling some of our get Pete if you have.
**Peter Wychunis:** Pet. I was gonna say a lot of how to Chris is
what I'll say right? And it might be applicable to ServiceNow,
but it also might be how do you submit PTO? What's the PTO process?
So just a lot of how to documents that
**Chris Clancy:** Yep.
**Peter Wychunis:** just don't necessarily fit into
ServiceNow. But we put them on our SharePoint because
we know, hey, this is a collective space that we know
everybody knows they have access to and they could share helpful information
should anything come up.
**Chris Clancy:** The how tos that would be relevant to
this process, are they kind of broken out into their
own little place on SharePoint?
**Peter Wychunis:** Uh, yeah, I I believe so.
And if they're not,
**Chris Clancy:** Really.
**Peter Wychunis:** they could quickly be broken out.
**Chris Clancy:** Got it. OK, cool. Cuz I see you. I mean,
I'm sure you see it too. Like if there's like a bucket that has
how to's that is that could meaningfully impact this,
if we could tie that in as another source of reference, that would be amazing,
right?
**Peter Wychunis:** Yeah, I'm a I'm a big how to fan, right?
So I'll have some how to one as simple as how to create a ServiceNow case,
how to create a ServiceNow quote, how to like how to just do everything
right? Like rather than just repetitively train
somebody, you're training me,
**Chris Clancy:** Yeah.
**Peter Wychunis:** giving the documents what I believe in.
**Chris Clancy:** Yeah, absolutely.
And where I'm extending my in my head, this too is within ServiceNow we have for
we'll call it case manager or agent personas.
We have a panel effectively an assistant, AI assistant. That if they just had any question, hey,
I'm new, I see that the customer entitlement,
they need a quote. How do I create create a quote?
Like it's a much better experience to not have them go off and just have it. Oh,
you create a quote by doing 12345, here's my citation. You know, after the races, right?
But it is predicated on having access to those altos.
That's why I was kind of unpacking this a little bit. OK, cool. I wanted to talk about. I want to make sure I'm kind of plucking
off parts of what you've brought up. So we've kind of already talked about
opportunity for external connector integration in a variety of senses here.
We talked about knowledge management. I want to talk about before I get to
dispatch. This will actually segue nicely. There's a desire to use a dance work a
song that it sounds like. But there is also a desire to potentially
augment with AI the assignment. So could I just get AI for a second?
Can I just get your take on do you see any gaps in your preliminary evaluation
of AWA that would necessitate AI or like I'm just trying to get a sense for where
you? Where you think this might play in your
minds?
**Phil Caiazzo:** I'll maybe I'll describe to you kind of
my vision of utopia as it pertains to a WA. Maybe that'll help.
So when a case comes in today,
**Chris Clancy:** Sure. Yeah, it'd be great.
**Phil Caiazzo:** it comes into that queue management group,
the queue management group does. 20 manual tasks to get the case to a
point where it can then be assigned to a technician.
Out of those 20 tasks that they do,
**Chris Clancy:** Mhm.
**Phil Caiazzo:** there's probably 10 that, in my opinion,
are could be systematically driven to help. Narrow that field of who that case could
ultimately be assigned to. So for example, we'll have customer. Polycom.
So Polycom's our customer and we have five specific agents that are dedicated
to that Polycom account. Now they're not solely dedicated.
Those five agents also service 1000 other
**Chris Clancy:** OK.
**Phil Caiazzo:** accounts.
But anytime a ticket comes in for Polycom, it has to be one of these five agents. So from an AWA perspective,
case would come in, it hits the assignment group,
AWA looks and says OK, is there what room? What room is the case being opened on?
Let me pull that information into the case. Who are the five agents that are part of
the Polycom group? OK, I see these five. Which one was the last one to get a case?
OK, this one has 20. This one has 20. This one has 10.
Let me give it to the person with 10 because they have less cases. It goes,
it signals them.
**Chris Clancy:** Sure.
**Phil Caiazzo:** Hey,
you got to do case to sell for Polycom. It sits there and the clock ticks for two
minutes, 5 minutes, whatever it is, they accept it,
goes into their queue and they run with it.
**Chris Clancy:** That sounds exactly what AWA was built to
do. Now we do look at and sounds like you're
very knowledgeable about AWA. We look at availability,
capacity and skills.
**Phil Caiazzo:** Yep.
**Chris Clancy:** The skills side of the house here,
you've defined like the account team kind of structure,
even though it's a support team. These skills are skills captured for
agents today.
**Phil Caiazzo:** Always P to answer that one.
**Peter Wychunis:** Are are not within ServiceNow.
We don't we have. So there's two answers to this Chris.
Mike Dennis and Mike,
**Chris Clancy:** Yeah.
**Peter Wychunis:** I'll speak on your behalf here.
So tell me to shut up if I'm wrong. Your team is currently putting skills
under agents for the field service. Side of the house right now.
We have not done that on the remote help
**Mike Dennis:** OK.
**Peter Wychunis:** desk side of the house yet.
We have all those, but we have skills captured in SharePoint.
It'll say, Chris, you know, Polycom, check, right?
This person check on this technology, but we have not populated that into
ServiceNow yet.
**Chris Clancy:** Gotcha.
So but there is a you are going towards the direction of capturing skills for
your personnel, what they're good at,
**Peter Wychunis:** Yes.
**Chris Clancy:** what they might need help on, etcetera.
It's just where are you storing that and
**Mike Dennis:** Yes.
**Chris Clancy:** field service is getting there a little
bit faster as it relates to ServiceNow than help desk, remote support help desk.
**Peter Wychunis:** Yeah, I think field service it was.
I think we all would agree or maybe we'll agree that we saw more impact in in the
sense of hey, let's get them filled out first because
now we can route a work order to them directly.
Whereas a case manager it's not as it's important that the right. The right issue goes to the right guy,
but it I'll weigh it less than a a field tech having the work go to them directly.
That makes sense.
**Phil Caiazzo:** Yeah, that's fair. Because with, with,
with, with it, within the field, you know,
**Mike Dennis:** Yeah, we agree.
**Chris Clancy:** Like there's less. Yeah, go. Sorry.
**Phil Caiazzo:** I'll, I'll,
I'll pick on our New York region. You're going to have 10 technicians in
New York and only one of them might have a specific skill set that this particular
case is required for. So it was much more important for the
field. To identify their skill sets,
then the 200 agents over here on the help desk that operate in a global fashion
that I might have 30 people over here that have that skill set,
but there's only one in New York from a field.
So this case can get routed to 30 people over here versus the one person over here
that should have it.
**Chris Clancy:** And the risk rolling a truck is
considerably more expensive than.
**Mike Dennis:** 100% showing up at a customer location,
being presented with the issue and saying Yeah, yeah.
**Phil Caiazzo:** Alright, alright.
**Mike Dennis:** I have 0 training or experience on this,
I'm going to have to go back and send someone else worst possible customer
outcome.
**Chris Clancy:** Yeah,
and I'm sure it reflects that way in some of your surveys and assessments that you
sent out. If that when that happens,
**Mike Dennis:** 100% Yep. Verbatim. Yep.
**Phil Caiazzo:** Yep.
**Chris Clancy:** right? Got it. OK,
so you answered my second question because we haven't quite gotten to the
dispatch portion of this, which was another one which was. Source engineer by skill set and location.
So you are capturing skills for the text, right?
I didn't get that far in the instance those skills matrix is being populated in
ServiceNow right now.
**Phil Caiazzo:** Yep,
I I think that I think we just started
**Chris Clancy:** Perfect.
**Phil Caiazzo:** building that out.
We're probably and how far through Mike's.
**Mike Dennis:** We should be pretty close to done,
if not completed already.
**Phil Caiazzo:** OK.
**Chris Clancy:** Yeah,
what's good is cause I've seen the work order tasks with the individuals that are
getting assigned. So we know we got their location and if
you have the skills and now you want to do it by skills and location,
the question becomes is that. What technique do we use for that?
That's that's on me, right? To kind of sort out like do I use AI for
that? Do I use something else within the
platform or would you use something else
**Phil Caiazzo:** OK.
**Chris Clancy:** within the platform for that?
So I'm not quite there yet. It was more like do we have the data
pieces to do what they need to do? Um, OK, so. I'm gonna go up to dispatch management
for a second. So on the I'm going to jump around a
little bit, but I promise I'll pie this together.
So when we've talked about the remote troubleshooting agent,
there was the idea that you would come up with a plan for the purpose of remote
troubleshooting. But it seems that has cross utility
because if you need to roll a truck that tech. Still needs to have a sense for what
needs to be done, right? Or at least an idea.
So they don't roll up and they're trying to fix a podium, you know,
box and it really is like it's the projector. You get the idea.
So I think that was called out in your dispatch coordinator agent, which is. Hey, look, take a look at the case.
You know who the account is. You know where they are.
You know what our SLA is. Come to a determination on the skill sets
that are necessary. Ideally, have an idea of what needs to be done
when you're on site. And then find the field tech who is in
that geography that possesses that skill. And in the work order task,
make sure whatever hypothesis or plan you come up with is in that work order task
so that they have eyeballs on a. So the first,
they don't get the task and go, wait a minute,
I'm in Florida and this is Georgia. I'm not going there. Secondly, it's like,
oh, this actually looks pretty solid. Like, OK, I need to go in here and do XYZ.
It's about kind of like reducing the friction,
not only in the dispatch identification part,
but also making sure that the field techs themselves have. A cohesive and descriptive set of work
they need to perform. Um, that sound fair?
**Mike Dennis:** You nailed it, yeah.
**Peter Wychunis:** Yeah, a clear,
clear and concise description is the way I view it, Chris.
**Chris Clancy:** Got it.
Why would field tech reject the work order task? We're assuming.
**Mike Dennis:** If they've got PTO that's not represented
on the calendar,
**Peter Wychunis:** But.
**Chris Clancy:** OK.
**Mike Dennis:** if they recognize that the technology is
above their station in terms of qualifications, training experience,
they might reject a work order for that reason. They might reject it if we didn't account
for enough travel between one dispatch
**Chris Clancy:** Mhm.
**Mike Dennis:** and another. For example,
if we have a work order scheduled for 1:00 PM,
their previous work order is scheduled to end at 12 and they know that it's a two
hour commute when we've we've scheduled a one hour commute. I mean,
those are just off the top of my head.
**Peter Wychunis:** Yeah, yeah, I, you know, I'm a field tech.
I've been out here 10 times and you guys
**Mike Dennis:** Pete sees a lot more than. I do but.
**Peter Wychunis:** aren't recognizing that downstream and
you're sending me back.
**Mike Dennis:** Yeah.
**Peter Wychunis:** There's nothing I can do based on the
last 10 times I was here.
**Phil Caiazzo:** We're not providing enough information on
the work order.
**Peter Wychunis:** Yeah, yeah,
not not clear and concise information. Or this work order you gave me.
It's everywhere. I have no idea what you're asking me to
do.
**Mike Dennis:** Yeah.
**Chris Clancy:** When that's really helpful.
Now when they reject, you're going back up to a tree of things
that take time in and of themselves, right? So meaning if they reject,
you're going back to the to the well to try to find someone else, right? I noticed there's some churn around
partner dispatch. I don't know if that's. Necessarily,
I'm sure it's applicable to you. I just don't know how much it's going to
be applicable to this particular effort. But to me it sounds like I need to
dispatch someone. Am I OK to use a partner if I don't have
an internal available tech? Is that the right way to look at it?
**Peter Wychunis:** Yeah.
**Chris Clancy:** OK. But when they actually reject,
how much like does that happen often? Like can you approximate like a
percentage of time?
**Peter Wychunis:** Yeah. Like, I'll say less than 1%, right?
Because I think what we try to encourage is communication, right? To say, hey,
I'm the tech you gave me this work order. I'm not just going to say no to it.
I'm going to come to you and I'm going to say, hey, I need AB and C.
**Phil Caiazzo:** Yep.
**Chris Clancy:** Mhm.
**Peter Wychunis:** And that percentage there, Chris,
probably less than 1%.
**Chris Clancy:** Yeah. OK,
so I'm going to bring this full circle. While this it is better for the overall
efficiency of the organization to provide clear and concise notes and try to reduce
sending the wrong person to the wrong site, just to pick an example. The value impact,
if I snap my fingers and solve this tomorrow and said nobody will ever reject
again because we've always had line of sight to PTO and we make sure we use
Google Maps APIs to ensure they have the right travel time.
Like the value payoff for that is going to be relatively small in like volume,
right in dollars. Sense. Is that a fairway to say?
**Phil Caiazzo:** It's going to be from a dollars and cents
perspective, yes, but the impact is bigger than the dollar
value will represent.
**Chris Clancy:** Sure. Like, yeah.
**Peter Wychunis:** I think what we also want to accomplish
within this, right, is, you know, you're getting the right information up
front. You're the tech has everything to go out
one time, Chris. Like ideally we want these guys.
If they're going to go out, we want them there one time. And now sure,
they're going to be situations where hardware's broke and they have to go back,
right? Yes, but if we can get them. All of the applicable information we're
going to reduce return visits.
**Chris Clancy:** Yep. So that's the.
**Peter Wychunis:** We're going to tell, you know,
if we're able to say, hey, you know, based on the description that was
provided, here's a hypothetical, you know, solution here,
you're going to need to come with two HDMI cables.
You're going to need to come with, you know, this, this size ladder, right.
And you know, just throw in 10 other things, right.
We get those guys that they're going to be more successful in the first time.
**Mike Dennis:** And you're also going to reduce the
troubleshooting time, right?
**Peter Wychunis:** Yeah.
**Mike Dennis:** Because right now,
according to our statistics in ServiceNow, our average dispatch is just under 4
hours. That's a long time, right? So the better the quality of the
information, the more of a head start we can give our
technician when they get there. The less they have to literally start
from scratch and start troubleshooting every single device in the chain of
devices. If we can narrow that down a little bit,
the pay off I think would be massive.
**Chris Clancy:** You said 4 hours on average to dispatch
today.
**Mike Dennis:** Just just under correct.
**Phil Caiazzo:** Yeah. So if you extrapolate that out,
obviously simple math, our techs average about two dispatches
per day, per tech, right. If we can get that to three or four like
that, again, the payoff on that is enormous.
**Mike Dennis:** I just like to get to two because you
know if you look again if you if you go back to some of the ServiceNow data,
I think we're averaging somewhere between 1:00 and 2:00.
You have some markets like our new
**Chris Clancy:** Mhm.
**Mike Dennis:** Arizona market where they are averaging
closer to three because they have their smaller markets. They're a recent acquisition.
They have a much more just to prove out this concept.
They have a much more in-depth troubleshooting process than what we have
in the rest of the business. So that shows you that the advanced
preparation can result. And being able to increase capacity in
the field. So that's what we're all trying,
trying to work toward, I think.
**Chris Clancy:** Got it. So in my. Initial statement was very specifically
focused on removing the document rejection reason.
That's a byproduct of providing clear and concise information that allows the field
service tech to not only be able to digest exactly what they need to do,
but ideally reduce repeat visits if you reduce repeat visit. You are making room for additional visits
to other customers and if you are finding
**Mike Dennis:** Yep.
**Chris Clancy:** the right engineer by skill set and
location quickly, you are reducing the time to dispatch
from approximately 4 hours to some metric. Is there a? I know you're saying like,
what would be utopia, to use your terms over and over again?
Like what is your target for dispatch?
**Mike Dennis:** In terms of duration.
**Chris Clancy:** In turn,
I took the approximate 4 hours to dispatch for everything that needs to
happen before a truck is rolling towards a client. Is that right?
**Peter Wychunis:** I'm sorry, Chris,
I need that one more time.
**Chris Clancy:** Yeah, yeah, 4 hours to dispatch today.
I interpreted that as four hours from the
**Mike Dennis:** And me too.
**Chris Clancy:** time a problem is stated to the time a
truck is rolling. Is that the right way to look at it?
**Peter Wychunis:** Yeah, yeah.
**Mike Dennis:** No 4 hours is the time our technicians
are spending on site on average from the moment they click start work until the
moment they closeout their work order task.
**Chris Clancy:** and they start work. Okay, to finish work.
Okay,
**Peter Wychunis:** So the so the help desk has already made
that determination. They're gonna send a technician and this
is now part of the dispatch process,
**Chris Clancy:** Mhm.
**Peter Wychunis:** right? The tech we've said, hey,
we need to send Chris out to site. Chris starts his work on site and he ends
his work on site.
**Chris Clancy:** Got it. OK,
so I was looking at it totally wrong. This was not the preceding the truck
rolling. This was I had site. I'm there for approximately 4 hours on
average today.
**Peter Wychunis:** Yeah.
**Chris Clancy:** Got it. OK. And that was OK.
So now that I have that framed correctly, um. Is there a target that you're going
towards? Like we want our texts to only be out
there for two hours maximum. We get all the perfect information,
understanding that stuff happened and whatever, but like generally speaking,
do you have a target?
**Mike Dennis:** I I I don't,
but anything less than that is appropriate. Zero is perfect. You know,
one to two hours is probably more
**Chris Clancy:** Yeah.
**Mike Dennis:** realistic and I think that would be a
fair target cut in half.
**Chris Clancy:** Got it. OK. Got it.
And would you say some of that time of the four hours is due to the lack of
solid information in the work order task?
**Mike Dennis:** I think that's a that's a fair statement.
I mean, I think that if you look at a day in the
life of a field technician, most of of what the technicians receive
today in a work order task, not every time,
but in a high percentage of time is the customer's description of the issue,
right? What is, what is the customer's symptom, right?
What are they seeing?
**Chris Clancy:** Sure.
**Mike Dennis:** So they're taking that,
getting on site and then trying to recreate the issue so that they can
determine which device or devices might be causing that issue.
**Chris Clancy:** Got it. OK. All right, that is super helpful.
Just taking some notes here. Bear with me one second. I guess I'm in stakeholders. Real quick here,
to communicate assignment to stakeholders, are we really just talking about like,
hey look, here's your work order task notifications
to the field tech or to all interested
**Mike Dennis:** Yeah, I'm, I'm thinking, you know,
a little bit bigger than that.
**Chris Clancy:** parties like?
**Mike Dennis:** I'm thinking, you know,
make sure that the field tech is aware of the assignment.
So they have the opportunity to review it, accept it, reject it once it's accepted,
making the customer aware. That the dispatch has been scheduled date
and time approximate,
**Chris Clancy:** Right.
**Mike Dennis:** making the help desk agent aware that the
dispatch has been accepted and it's sort of locked in for this date and time.
I think that's that's it.
**Chris Clancy:** How does it? How does it?
**Mike Dennis:** The stakeholders would be case manager,
customer and technician.
**Chris Clancy:** Does that happen in any fashion today?
**Mike Dennis:** Manual today. So yeah,
it's team sending an e-mail out to the
**Peter Wychunis:** Today it's all all manual, Chris. So Kate.
**Mike Dennis:** customer to say this technician's going
to be there at this date and time.
**Chris Clancy:** The case manager doing it.
**Peter Wychunis:** Yeah.
**Chris Clancy:** Got it. And the the desire, yeah,
go ahead.
**Peter Wychunis:** Right. And and all that information is,
is that that we're providing to the customer,
they're all fields within ServiceNow, right. You know this is your technician,
this is the his start time, right. It's all there. We we take that over.
We I,
**Chris Clancy:** Yeah.
**Peter Wychunis:** I I'm a big fan of the quick messages in
snow, right. And we kind of script them to fill out
the information.
**Chris Clancy:** Yeah.
**Peter Wychunis:** But you know,
I don't see there's no reason why, you know, once that thing scheduled. Communication goes out to the customer.
Hey, this is your technician. This is what to expect.
**Chris Clancy:** Totally agree. Very deterministic. Yeah,
the data's there. It shouldn't be a big deal.
So kind of making a profile here like it's under the context of an agent.
Agents use tools, deterministic tools and LLM so. It's not a big deal. I just need to know,
like, you know, to what extent is it happening today and
what what is desired in state, OK. Just making sure I'm not leaving anything
out here. Could you talk to me just for a second
about asset managed? Like I looked on your instance,
I can see the customer, I can see assets, basically name and serial number when you
do a project. And you have a new customer,
are you capturing every single piece of equipment and the related serial numbers
as assets manager now?
**Phil Caiazzo:** So Asset Management today is something
that has been new to the company. In what you're describing over the last
year and a half, two years today, it's kept in a separate database 2026,
we are moving that into ServiceNow.
**Chris Clancy:** Oh.
**Phil Caiazzo:** So there will be a migration effort of
the information that we do have from our customers into ServiceNow. On top of that,
there's an initiative company-wide that will take a number of years to kind of
fulfill. But the vision is that regardless of what
downstream systems are used by our operations and our install teams,
that information from equipment, make, model, serial, lumber,
etcetera will make its way into ServiceNow as. As part of our systematic handoff
processes. So today very little information that we
would have from our customers perspective
**Chris Clancy:** Got it.
**Phil Caiazzo:** from asset gathering. What you're probably seeing is we do
collect when we are responsible for our video conferencing codecs from a
manufacturer perspective. That information we do capture and do
publish in ServiceNow today.
**Chris Clancy:** OK, got it. That's helpful.
I just wanted to make sure I wasn't missing like a big, big rock here.
**Phil Caiazzo:** No, not yet.
**Chris Clancy:** Yeah, it's coming, right? Cool. Right on.
Um.
**Phil Caiazzo:** We're we're getting there.
**Chris Clancy:** OK, hold on one second.
I think these were the two. Is there any? I I know I didn't get like the there's
123. There was a number of processes that I
didn't see documents on. I I want to be mindful of not blowing. Up the scope crazy to touch every single
process that might touch case management, but is there anything in the quoting side
or the logistics side that you think are opportunities for improvement as it
relates to ServiceNow?
**Phil Caiazzo:** Quoting side is is tough only because I
think we we AVISPL should have an initiative to tie into our normal quoting
procedures like today the quoting process is completely custom within ServiceNow we
had a built. And it works for service,
but I think bigger initiative from us internally is once we have a consistent
global ERP system, which again is coming in the next couple
of years, then we can tie that quoting into how we
quote the service now and this way everybody in the company is quoting the.
**Chris Clancy:** Hmm.
**Phil Caiazzo:** Same way using the same tools,
same processes, etcetera. So quoting. I I don't.
I don't think it's a worthwhile exercise to go through for this just yet.
If they tell me it's 10 years away,
**Chris Clancy:** OK.
**Phil Caiazzo:** I might come back to you and say, hey,
let's add this to the scope.
**Chris Clancy:** OK, good to know and just for. Sake of uh,
I did notice you mentioned custom. I did notice that you folks have. A number of custom field tables that are
hung off a case. So you guys created your own quote like I
noticed it was your case structure was really nicely done in my opinion like
stayed relatively out-of-the-box. There were a few customizations sounds
like around quoting logistics. And you tied your MPS into that as well
and maybe TNM billing. So like it seemed like it was very
thoughtful in sometimes I see these and like it's like a spaghetti nest.
I don't know what's going on. So this was very nicely done. It helps me.
**Phil Caiazzo:** That's what we that's what we came from.
And the the notion when we got into ServiceNow was to make it as
out-of-the-box as as humanly possible. So we untangled the big rat's nest when
we were in Salesforce.
**Chris Clancy:** Yeah.
**Phil Caiazzo:** When we got to ServiceNow,
it was change of process, change of habits,
whatever it takes to stay as out-of-the-box generic. As possible.
**Chris Clancy:** Yeah, I chose right.
It it it makes this a lot easier. It makes the build time a lot shorter
because you're sticking out-of-the-box for the most part. All right, so quoting,
no. We'll kind of stay away from that. The logistics,
I know there was a ton of stuff here. Like it seemed to me anytime you needed a
part or an RMA or anything like that like. There's a whole chain of logistics that
need to occur to request replacement parts.
There's probably a million things I I don't even know about,
but that encompasses the logistics process.
**Phil Caiazzo:** Yeah,
but I I think there's some opportunities there,
maybe some low hanging fruit if if I'm being honest,
that could help with all that.
**Chris Clancy:** Let's hear about it. What do you think?
**Phil Caiazzo:** So very simple things and some of them go
on to the, you know, customer satisfaction type scale.
So today I I have a person on my team who's almost sole existence is to get
tracking numbers. From FedEx, from UPS, et cetera.
Put that information into the case and then provide updates on when packages and
stuff are going to arrive. I would have to think that there's some
type of a I simplicity that could be applied that says. Hey, here's the FedEx tracking number.
Go out, find this information for me, populate these fields,
and when this information gets populated, send an automated message out to our
customers that says here's when your package is expected to arrive kind of
thing, as well as notify the case owner in the
case notes.
**Chris Clancy:** Yeah,
this is just a bread and butter REST calls and workflow. Could a I be in there?
Cool. Yeah, maybe. But like,
**Phil Caiazzo:** Yeah. Yep.
**Chris Clancy:** I've seen other customers do exactly what
you're talking about and you have a person who's dedicated for that.
**Phil Caiazzo:** Yep.
**Chris Clancy:** And I'm sure they love looking at
tracking numbers all day long.
**Phil Caiazzo:** I I I love Ida to death.
I think there's better ways that we could
**Peter Wychunis:** It.
**Phil Caiazzo:** utilize Ida's time.
**Peter Wychunis:** Chris,
once those tracking numbers numbers are plugged in by Ida,
now it's reliant on the case owner to get
**Chris Clancy:** Yeah.
**Peter Wychunis:** to that notification in time to send an
e-mail to the customer that a part's on the way. Generally, not generally.
Sometimes what happens is, hey, if that's an overnight delivery,
by the time that case owner gets to that notification. Art is already delivered, right?
And the customer says,
**Phil Caiazzo:** Yeah.
**Peter Wychunis:** was anybody going to tell me that this
was here?
**Chris Clancy:** I see. OK, so yeah, it looks out of step.
Like, why didn't you tell me? Yeah,
**Phil Caiazzo:** Yep.
**Chris Clancy:** I totally get it. So is there a? Can I talk to Ida at some point?
**Phil Caiazzo:** I I I don't think you.
I don't think you want to talk to Ida.
**Chris Clancy:** Or or you if you know exactly what she
does. No, she's too busy doing tracking numbers.
I get it. OK,
**Phil Caiazzo:** I wouldn't. I wouldn't do that to you.
**Chris Clancy:** well maybe just cause that's like that's
it is low hanging fruit. Is there any other stuff that you can
think about in the logistics side of the house that is low hanging fruit?
**Peter Wychunis:** Um.
**Chris Clancy:** And if not, it's no big deal.
**Phil Caiazzo:** Maybe we get back to you on that.
**Peter Wychunis:** Yeah,
I was gonna say maybe I could sit with
**Chris Clancy:** Yeah.
**Peter Wychunis:** them, Phil,
and have them show me their workflow.
**Phil Caiazzo:** I ironically, Chris,
this is something that we're actually
**Peter Wychunis:** Just show me.
**Phil Caiazzo:** transitioning from one manager over to
Pete's team.
**Chris Clancy:** Yeah.
**Phil Caiazzo:** So Pete's going to have a first-hand
experience with this team coming up here in the new year.
So let us get back to you on that.
**Peter Wychunis:** I'll say this,
I I think a lot of what they do is plugging in fields, right?
Take data from here, plug it in there.
**Phil Caiazzo:** OK.
**Chris Clancy:** Yeah,
I'm kind of thinking like I'm not going to do it on a live tracking number,
but like what you described is not like I could show you the pattern of how it's
done and like build it out and like have like mock tracking number and show how
flow like updates records and stuff like that.
Like I just need to know exactly what they're kind of doing and then I'll just. Like stitch it together.
It shouldn't be the deal. And if it saves you some time or I do
some time more specifically, it might not be a bad thing to kind of
throw in here.
**Phil Caiazzo:** OK.
**Chris Clancy:** We talked knowledge.
We talked dispatch management. Oh, major case. This is major incident case.
You use a major case construct today. You described it before, right? Well,
do you get a lot of them?
**Peter Wychunis:** Yeah. Yeah.
**Chris Clancy:** Yeah,
what would be the normal circumstance that a major case would come in?
**Peter Wychunis:** So I I would categorize that. And Phil,
you you might correct me here. Kind of like the example I gave earlier,
right, where there's a Poly Polycom sends out an
e-mail and it says, hey, anybody that's on this firmware is going
to have issues, right? So then we would create a case for that. Polly communication and we would tie all
the child cases to that parent. So that way if I if if I'm the owner of
that major case, I'm working directly with Polly and
Polly's feeding me updates. I'm putting those updates into my ticket,
which is now feeding all the child tickets,
so that everybody who has a ticket is aware of what the updates are and they
can then share it with their customer.
**Chris Clancy:** Got it. OK.
**Phil Caiazzo:** Yep, that's one example.
There's another example I'll use of our Symphony monitoring platform if an entire
building goes out or an entire, you know, geography goes out, so to speak, and. We'll get 1000 alerts that pop up on our
dashboard. We'll create one major incident ticket
and tie all of those alerts into that incident ticket so that we don't have
1000 tickets, we have one that's managing the entire
event.
**Chris Clancy:** Got it. OK,
so it could be a a site issue or a vendor specific issue.
Are there other circumstances or are those generally just like 2 good examples?
**Phil Caiazzo:** I would think that's that encapsulates
probably the the majority.
**Chris Clancy:** OK. Yeah. I mean, look, you folks are,
it's not like you're developing software that could affect multiple customers.
Like what are the, what is the the premise of a major case
that something's affecting many people and what would be those cases,
the vendor specific equipment that you use? Or a site location that might spawn a
bunch of case sprawl that you don't want to be chasing your tail if you know that
the site is down itself because Symphony told you. OK, that makes sense. Is there? Is there opportunities in there that you
think you think you pretty much have it down given that that you don't get many
of them or?
**Peter Wychunis:** I can't think of any opportunities, Phil,
to be honest, right? It happened. So it doesn't happen often.
And I think what happens today works and maybe that's, yeah,
I can't think of any need for it.
**Phil Caiazzo:** Top of my head.
I can't think of anything other.
**Chris Clancy:** Bam. A major case existence before remote
troubleshooting starts. That's the one that I thought that we
talked about earlier.
**Peter Wychunis:** Yeah.
**Chris Clancy:** Maybe one slipped through the cracks,
you know what I mean? And now you're starting to do this whole
remote troubleshooting effort and it's like, oh,
actually this is already known about, so no need to bother. OK. So here is oh, I missed one thing.
Proactive maintenance visits. So it seemed to me that I'm going to be
oversimplifying this. There are customers that if they need
help, you can quote on time materials and
you'll help them. And it sounds like there's customers that
have contracts. For support, does that sound right?
**Peter Wychunis:** Yep. M.
**Chris Clancy:** PMV falls into the customers that have
support like an ongoing support contract.
**Phil Caiazzo:** A preventive maintenance visit is. So a customer can subscribe to have a a
room check X number of points per year. So most customers subscribe to once a
year. I want a BISPL to come in and do a health
check on my room, right? So we call them preventive maintenance
business.
**Chris Clancy:** Mhm.
**Phil Caiazzo:** That room could be 100% operational. But what we're going to do is we're we're
going to come in, we're going to make sure that the cables
are are neatly addressed and you know the monitor is square on the wall.
And if your light bulb in your projector needs to be changed,
we're going to denote what that is. So it's it's really just a health check
for particular rooms. In the course of that we may find issues,
in which case we will open up a a case, an incident to resolve that issue that we
found during the preventive maintenance visit.
So today the reason that this specific point is on here today on when a customer
signs a contract, they subscribe yes or no to preventive
maintenance. And what's the frequency that they want
that preventive maintenance? Is it yearly, biannually, quarterly, etcetera?
So numbers put in there, the contract is processed through
ServiceNow and today the system reads it and goes OK, this customer. For these ten rooms has one preventive
maintenance visit per year. So it goes in and it opens up work orders
for those 10 rooms for one time a year. And let's say the contract starts January
1 and ends December 31st. So in May,
approximately 5 to six months into the contract,
those work orders will pop onto my team's dashboard that says, hey,
in the next two months you want to be able to do these preventive maintenance
visits for this customer and their work
**Chris Clancy:** Right.
**Phil Caiazzo:** orders. What we would like to get to is instead
of having them come in as work orders, we have them come in as cases because it
it provides a lot more functionality for us to work out of. And we can add notes,
we can add commentary, we can, you know, send tasks off to do specific things
where you can't do that in a work orders. Order.
So the notion here is can we get it from going creating work orders to creating
cases?
**Chris Clancy:** Got it. OK,
so this is more like a a data model reengineer than it is like it's not like
you got the.
**Phil Caiazzo:** It's a re-engineering of,
it's a Frankenstein that we created because we we were, we were kind of,
we were guided that way by our our
**Chris Clancy:** OK.
**Phil Caiazzo:** initial vendor when we went down the path
of migrating from ServiceNow or from Salesforce to ServiceNow.
**Chris Clancy:** Yeah.
**Phil Caiazzo:** They encouraged us to do it this way,
and we found that it's not as efficient as we would have hoped or thought.
The case route is where you get a lot more benefits.
So unraveling and de Frankensteining what has been built to make it much more
simpler into a case.
**Chris Clancy:** Got it so. Truly as a process and data model
opportunity, probably not something in this Sprint
like for a I like your main problem here is and not that you don't do them or you
don't track them, it's just where you're tracking them.
At least that's your initial problem right now, right?
**Phil Caiazzo:** Yes.
**Chris Clancy:** OK, OK. WhatsApp and chat integrations today,
do you have, well, let me ask you teams company wide,
is that right?
**Phil Caiazzo:** Uh, Microsoft Teams, yes.
**Chris Clancy:** Yeah. Do you, um,
do any integrations with ServiceNow with our with teams?
**Peter Wychunis:** No.
**Phil Caiazzo:** Can't think of any. I can't think of.
**Peter Wychunis:** No.
**Phil Caiazzo:** I don't think we do.
**Chris Clancy:** Is there is that like a?
The reason I ask is and maybe we don't do it during this build because it'll take
longer than like a week or two, but. ServiceNow Virtual Agent Now Assist
Virtual Agent has out-of-the-box integrations with Microsoft Teams in so
far that remember that scenario we said how to create a quote.
You could literally just go to Teams. Type how to create a quote,
get the same response. Just the difference is where you're
landing and where you're living. Same thing for updates on incidents,
same things for making requests and things like that.
So just kind of keep it in your back pocket if you're standardized on teams
and you see utility in engaging with ServiceNow and now Assist on ServiceNow. Teams can be an entry point,
so put it in your back pocket. Take it for what it's worth.
If people are used to living in ServiceNow on the agent side of the house,
that's fine. I work with other customers that they're
like, look, we have, you know, financial advisors and they never want to
leave teams and e-mail, so. You know, your mileage will vary. Um. Do you have a requirement for more chat
integrations in general? Because I noticed it when it was in here
on your list.
**Phil Caiazzo:** Yep.
**Chris Clancy:** What do you see that as being?
**Phil Caiazzo:** So kind of a couple step process here.
If if you were a if you're a customer of AVISPLS,
I'd be embarrassed to direct you to our customer portal at the moment because
it's it's it's a terrible experience it
**Chris Clancy:** OK.
**Phil Caiazzo:** it's. It's from like 1985.
So the vision is that we redo our customer facing portal to the point where
it gives the customer a holistic entry point into a BISPL.
You can do searches for existing cases. It gives you a list of phone numbers,
it gives you an e-mail capability, it gives you a portal capability to open
a ticket and it also gives you a chat
**Chris Clancy:** Mhm.
**Phil Caiazzo:** function.
That chat function will be driven by ServiceNow,
but will the entry point would reside on our customer facing portal. So that's kind of step one is let's get
our customer facing portal a little bit more presentable and useful for our
customers. Step 2 on our side is how do we start
introducing chat into our existing environment from a skill set standpoint
and availability standpoint. We also have a language. I won't call it an issue,
but we have a language barrier, so to speak,
where we're starting to have more and more of our level one resources in India
and Mexico where English isn't their first language.
So how does that information make its way
**Chris Clancy:** Easy.
**Phil Caiazzo:** over to somebody in India and present
itself into something that's going to be digestible for them to be able? To respond to somebody in the US,
that actually makes sense.
**Chris Clancy:** Sure.
**Phil Caiazzo:** So how can the person over here in India
interpret this in a way that makes sense? How can their response make its way
through, present it to the person in Philadelphia?
That makes sense.
**Chris Clancy:** Sure. Got it.
The customer portal today is external to ServiceNow, right?
**Phil Caiazzo:** Yes.
**Chris Clancy:** You have your own website, not ServiceNow.
Customers are going there. You're looking to reimagine that,
make it more contemporary,
**Phil Caiazzo:** Correct.
**Chris Clancy:** have shims or hooks into a chat delivered
experience back to ServiceNow, the people behind the curtain on the chat
side with an AVI SPL. Would actually be international.
So they have their own language localization efforts that need to occur,
right? And that's kind of like the broader end
state here as as it relates to chat integrations. Is that right?
**Phil Caiazzo:** Correct.
**Chris Clancy:** OK. And the WhatsApp side,
could you describe that for me? OK.
**Phil Caiazzo:** And a lot of their customers,
and we're finding it not only South
**Chris Clancy:** OK.
**Phil Caiazzo:** America,
but a lot across the APAC as well. A lot of them use WhatsApp as a form of
communication. They don't use e-mail,
**Chris Clancy:** Mhm.
**Phil Caiazzo:** they don't use text, they don't use phone. They they they use the WhatsApp and
WhatsApp goes into. Our South Americans ticketing system and
that's how they would communicate. So a question was asked of us when we did
the acquisition of can we incorporate WhatsApp into our ability to intake
customer information and get it into a case and manage that out of ServiceNow. So I think that there's a hook for
WhatsApp that ServiceNow offers,
**Chris Clancy:** Yeah.
**Phil Caiazzo:** or there's a middleware that has to kind
of come into play to enable that connection because we we did look into it,
but this was more of a hey, if there's an easier way for WhatsApp to
get into ServiceNow, we're all. Years.
**Chris Clancy:** Got it. OK, that's going to. Kind of segue into something that I we
mentioned in the first call, I know because I got a sticky for it,
which was for me at deflection. So 15, 000 cases,
65% of them roughly are automated, meaning driven by alerts or monitoring. The remainder, there's a potential for,
I'm sure there's a potential for deflection in the learning and monitoring
side of the house, but I'm talking more of the the human
aspect here. So I'm a customer, I have a problem.
What resources are available to me as a customer of a BISPL? To self-service or figure out what's
going on. Forget if they're even interested in
going down that path. Let's pretend I was like, you know what?
I don't want to talk to anybody. Let me see if I can figure this out. What?
What's available to me as a customer?
**Phil Caiazzo:** Nothing. Today, nothing.
**Chris Clancy:** OK. Got it.
I'm sure the desire because we want to do self-service deflection is to present
them some kind of structured content that can guide them in some way,
shape or form towards self-service before the point of case creation.
**Phil Caiazzo:** 100%.
**Chris Clancy:** Got it. Have you folks? Yeah, go ahead.
Sorry.
**Phil Caiazzo:** And we and we and we recognize that like
that requires a knowledge base, it requires hooks into, you know,
external things. It requires an A I chat agent to be able
to do all those kinds of things in the back. So we recognize all that,
which is why we're we're not there yet.
**Chris Clancy:** Yeah. Sure. And it's good.
It's good to know like where you're at and where you're trying to go.
I and you already recognized it. Like deflection visa V delivery of
knowledge, delivery of catalog items to request
things and then the backstop of a live agent chat or just a direct case creation
completely available is like a bread and butter use case for us. But to your point,
it just really kind of revolves around what knowledge do I want to present to
them that I think will be effective in achieving case deflection.
But I'm glad I picked on that in terms of like a I representations of this. I could certainly show what it could look
like if someone were to engage through a chatbot and be shown knowledge and things
like that. I don't know how much, how much use that's gonna have to.
I don't know if you've seen it before with other people you've engaged with at
ServiceNow. Is that like a a secondary thing that
would be cool? Have you seen it before?
**Phil Caiazzo:** If if we have,
it's been a long time since we've seen it. Um.
**Chris Clancy:** OK.
**Phil Caiazzo:** So Aaron Seiden might have been,
who I know he had a drop from the call, but he might have seen something more
recent than Mike, Peter, myself.
**Chris Clancy:** Kind of cool. Sorry if I could type. So here is what I'd like to do.
I I feel like, and I apologize, I feel like this was a deposition from me
to you, but this is like a lot.
**Phil Caiazzo:** It's been great.
**Chris Clancy:** It's it's a lot of great information.
It helps me a lot. I think that well, I know exactly what the next step here is. So I have the recording.
I need to go back and digest some things. I try to not like peck away at notes
while I'm talking with you so I can listen to you and not spend half my brain
writing things. So I'd like to go through some of the
notes, but I think I have a sense for some of
the things that would potentially be shown. And they land pretty closely to what you
folks had originally asked for, which is around remote troubleshooter
agent. But what I want to do here is put some
slideware together that kind of describe each unique build item. And kind of where my head's at in terms
of the things I I want to build and the outcome I want to achieve and then
quickly get that to you and then hopefully you either go, hey,
looks great or hey, I'd like to make some tweaks here and
then now we're boom right into build world where it's basically me. Maybe one or two others,
but I have access to the instance. I already have the analysis bits staged
on there and as far as I'm concerned it's ready to go.
But I want to kind of collect my thoughts after this meeting and come up with the
build cases. But for that right now I'm looking at
remote troubleshooter agent. Probably going to.
I'm definitely going to turn on the knowledge generation A I skill and kind
of paint a bit of a story here of you have a lot of good case data in there,
like what it would look like at the end of a case closure for an agent to
actually be presented with realistic knowledge based off of the details. Based off of the details of the case,
that won't be a big deal. That's literally a turn the switch on and
maybe futz with a couple of settings to make sure I'm capturing all the data
points you want. I called out knowledge hygiene agent
because I wasn't sure how much right now you wanted knowledge or you plan on
having knowledge in ServiceNow. A lot of times people burn time. Retroactively going back into knowledge
and making sure it conforms to certain standards, right,
that are based off of what you as an organization want your knowledge to look
like. So a lot of humans go in there and they
go, oh, it's referenced in this structure, it's this, that and 3rd. I think I'm probably going to skip that
one.
**Phil Caiazzo:** That's fine.
That's actually going to be a starting February one initiative for I I actually
have a guy that's going to kind of take some of that stuff over and work with
Aaron to get knowledge hygiene kind of more ingrained into how we do our
day-to-day so. So specific templates,
specific formatting, specific approval process,
like all that kind of stuff is going to be much more streamlined and efficient
hopefully by the end of Q2Q3 next year.
**Chris Clancy:** OK, cool. We can park this one.
I'll keep it noted for and I'll give you folks access to Miro if you want to see
it, but I'll keep it kind of off to the side
as a stretch goal for down the road. I have this in AI use cases, but you know,
major case child association. I'm really just trying to get a sense
that. If there is already a major case,
we're not burning time trying to remotely troubleshoot. I think I might have put that in there
twice and then the dispatch coordinator agent.
I'll need to take a look at the skills that you have built out for the field
text, but it really is a twofer right? Which is. Where are my texts? Uh. Relative to the site that needs to be
visited, do they possess the correct skills?
And am I providing a clear and concise explanation of the upstream case data to
the work order task so that a field tech can look at this and go, OK, cool,
it's in my area. Yes, I'll take it. Oh, this,
that and the third looks like it's problematic. Like, oh,
this customer's maybe had a history of this. You know what I mean?
You start to kind of aggregate data
**Phil Caiazzo:** Yep.
**Chris Clancy:** points into a digest that a field tech
can look at and have a good sense of what they need to do and also the historical
context.
**Mike Dennis:** Perfect.
**Chris Clancy:** Um, but yeah, so I'm a. I think I'm probably good right now.
I want to leave time. I know we've been having free flowing
discussion, but I want to leave time for you to ask
any questions about either the next steps if I haven't explained them or just
anything in general. Kind of floor is yours and otherwise I
can give you time back your call as well.
**Phil Caiazzo:** I I think from my standpoint,
I I think you've done a really good job of understanding our how we operate from
a business workflow perspective. The things I think you're focused on are
the right things to help us again. Small wins, but impactful wins.
And I think that's what this exercise is all about, right?
**Chris Clancy:** Agreed. Yeah, 100%.
I appreciate the feedback. I appreciate you giving me the time to
ask these questions. I know, as Mike mentioned before,
sometimes it feels a little slow to go faster. I'm a firm believer that as well.
So I do appreciate you bringing the folks on the line as well as yourself to answer
these. Questions Mike, I see Mike Buckner's back,
but Mike Dennis, did you have anything you wanted to add
or any questions you wanted to?
**Mike Dennis:** No, I I think Phil,
Phil summarized it well. I mean I appreciate that you need to ask
these questions to really truly understand the pain points and you know,
I hope we've articulated to you, you know the benefits that we see from
you know from specifically my point, you know my my agenda is to. Make my field technicians more efficient
on site and as Phil mentioned or Pete mentioned earlier to increase first visit
resolution. You know when we when we know we need to
go out there right now to give you some context,
we measure this at the case level, right so. We have a metric that looks at any cases
that required at least one dispatch, but only one dispatch and we look at how
often that happens, right? And right now we're teetering around 70%
and we can't seem to get that much higher than that. Now we do appreciate. That when we look at our and we built out
these return visit causes, right? So we ask our technicians if they can't
solve a problem and they have to close the work order task as closed incomplete,
we've created a drop down list. Of reasons why and what we found is that
the the highest number of instances do revolve around RMA right equipment that
has failed. We don't carry this equipment in our
service vehicles or in our local offices. We're going to have to order it,
come back and reinstall it or send it in for repair. So we know those are unavoidable
instances, but most other categories are avoidable
and that's what I'm trying to attack, right?
So one of the most other prevalent reasons that that our techs indicate
they're having to come back is they ran out of time. And if we can get the better information,
better preparation upfront, I hope that that diminishes over time and
that we can reduce again that average four hour dispatch down to two hours or
even less than that better preparation. So I hope that that's really clear.
That's the one. One thing that's really driving, you know,
my involvement here is trying to get there and using the technology that we
have available to us to get there and take more of this out of Phil's hands and
just let the tools do their work, right. So that creates capacity in Phil's team,
it creates capacity in my team and it's an overall. Huge win.
**Mike Buckner:** I'm curious,
you said you said something interesting
**Chris Clancy:** Super good.
**Mike Buckner:** there. When when techs run out of time,
do they document on the case or the the field dispatch like what took so long so
that you can kind of get into that, you know,
reinforcement aspect and figure out what
**Mike Dennis:** 3.
**Mike Buckner:** we could have done better next time?
**Mike Dennis:** Yeah,
I I don't think we do a great job of that. I think, you know,
technicians are supposed to list any troubleshooting steps that they took.
But like I mentioned earlier, a lot of times they're getting to site
and you know this, this is no slam on the help desk because
they're they do a great job. I mean, they really do. But in many cases,
the field technicians just looking at the symptoms that the customers reported and
they're they're basically starting from scratch, right?
They're looking at every device in the room. What could possibly be wrong?
Is this a signal flow issue? Is it a hardware issue?
If a hardware issue, where in the chain is that happening? If it's a complicated room like a
multi-purpose room, it's got a lot of technology in it and
it's got combine and divide capabilities where it functions one way and in combine
mode it functions different way and divide mode where it's like 4 different
spaces. It can take a lot of time to try to
narrow that stuff down. So the more again, I I think that's a that's part of the
issue. I think the other part of the issue is
technicians are mismatched from a skill set perspective and they're not going to
admit that a lot of times, right.
**Mike Buckner:** Yeah.
**Mike Dennis:** They're not going to admit I just. I just don't have the training and
experience to deal with this because they think there might be repercussions for
them personally by admitting that.
**Mike Buckner:** Yep. Yeah.
**Mike Dennis:** So they just,
they're just going around in circles trying and failing, trial and error,
trying to identify a problem, solve a problem.
They just run out of time. And so now we've got to come back and
continue that maybe with the same technician, maybe with. A higher skilled technician. It's uh,
it's a bit of a of a mixed bag.
**Mike Buckner:** Yeah, that makes sense.
**Phil Caiazzo:** On top, on top of that,
I think there's a little bit of and again this is. We have technicians that are very
methodical in what they do, so they will approach an issue and say,
OK, here's the first thing I'm going to do,
second thing, third thing, fourth thing. And from a remote side,
we might have done those first four or five things,
but unless the technician who's on site physically does. Those things like that,
there's a trust factor there, and there's a OK,
I know I need to do these five things to eliminate that from the potential cause,
and then I can proceed with the rest of my troubleshooting.
So there's just a little bit of nuance
**Mike Buckner:** Mhm.
**Phil Caiazzo:** into how everybody does that piece of the
job, and it's not right or wrong,
**Mike Dennis:** Yeah.
**Phil Caiazzo:** and it's probably a behavior that you're
never going to be able to. Standardize on because there is no right
or wrong way to do one piece of troubleshooting,
but everybody just does it a little bit different.
**Mike Buckner:** Yeah, it makes sense.
One thing I have seen that's really advantageous about these types of A I
systems is going back to like we said before that you're not really capturing
what took too long or why it took longer and you had to kind of go back a second
time is that when people start to, it's kind of that carrot versus a stick
approach. We can either say please document this
stuff. Is your job to document,
is the process to document, and people will do a middling job of it.
But when they start to see the benefits in doing it in that AI is using that
information to be more proactive in the future,
to provide better context in the future, people are more apt to do those extra
things when they get personal benefit from it.
So I'm always a big fan of these types of things that. Talk about variety of things,
the updating knowledge articles, keeping that up to date like everyone
knows they should be doing it. But when they see the personal benefit of
doing it, it's a lot more effective than just
saying this is the process, go do it.
**Phil Caiazzo:** Yeah,
that's and that ties into something that Pete and I have been talking about,
which is like you're probably seeing Chris when you're scouring through our
info. A lot of our resolution notes are very. Unfiltered, right?
It's it's very open keystroke. Like there's no formatting to it.
There's no specific questions that are asked. It's just, hey,
here's what we did to resolve the issue. What we would like to introduce and what
we're considering is like, OK, when you are going to resolve the case
and you know exactly what it was, put up some type of structured
information thing that cut that our team has to fill out specific data points that
we're looking for and then that can help feed into our knowledge management that. From your point, Mike, you know,
makes it a lot easier for when I when I do have a question,
I can ask this and now there's specific reference points that can just pull it
out.
**Mike Buckner:** One of the things that's so interesting
about knowledge design in kind of 20252026 is we spent so many years in the
past building these like beautiful HTML table formatted knowledge articles so
that humans could read them more better. But AI agents don't care, right? Actually,
it's not advantageous. You're just bloating the context window
with stuff, right? So like,
**Phil Caiazzo:** That's a good point.
**Mike Buckner:** we actually have a white paper I can. Send you on best practices for knowledge,
but it's not around formatting, so it does actually reduce the burden a
little bit, like a bullet list of what you did.
Even if it's long and messy, like the AI agent does not care,
you know the LM does not mind one bit how
**Phil Caiazzo:** That's a great point.
**Mike Buckner:** you format that stuff.
So just the fascinating change of
**Peter Wychunis:** I think.
**Phil Caiazzo:** Yeah, I'd love that that white paper.
If you don't mind sending it,
**Mike Buckner:** behavior. Mhm, Yep.
**Phil Caiazzo:** that'd be great.
**Peter Wychunis:** I think everybody on this call knows this,
right? But the historical resolution information
that we have in ServiceNow today, it's gold, right?
And they're like Mike's team and my team, when we fix an issue,
there is a field that information has to go into what the fix was that should
match up to the description of what the issue was, right? I use AI, right?
I think everybody probably uses AI, but if I have a complex issue, I'll go.
Now I have to create reports to do this and go in and I got to say, OK,
give me all the resolution information that matches a Polly E70, right?
And then I'll go, I'll scour through all that stuff.
But now I'll kind of plug that resolution information into AI and be like, hey,
here's the issue I have, like what matches? Is up here and like 9 times out of 10,
like, you know, the fix has already been done by somebody
on the global services team, right? It's just happened in an area, you know,
another country, another city that we're just not seeing,
right? So I think that's where it's going to be
gold, right? Where? We know this issue happens with this
product. It happened in San Francisco. Now we're having that issue in London.
Just feed it to us.
**Mike Buckner:** Yeah, great opportunity.
Appreciate the partnership here.
**Chris Clancy:** So for next steps,
look out from a for an e-mail from me. I'll send some initial collateral over
like soon that describes kind of things I I would like to build and maybe some asks
that I might have following this, particularly around the SharePoint stuff.
We might need to tie off a little bit more. I'll leave it up to you whether or not
you want to have another meeting to recap what is to be built or if we want to take
it in e-mail. I want to be respectful of your time so,
but I have a little bit of work to do and I'll be back to the folks here as soon as
I have that done.
**Mike Dennis:** Fantastic, yeah.
**Phil Caiazzo:** Sounds great.
**Mike Buckner:** Thanks, Tim.
**Phil Caiazzo:** Thanks everyone.
**Mike Dennis:** Thanks, Chris and Dave. Awesome stuff.
**Michael Runger:** Thanks, Chris.
