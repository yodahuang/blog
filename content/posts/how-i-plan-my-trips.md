---
title: "How I Plan My Trips"
date: 2024-08-04T13:16:47-07:00
draft: false
math: true
---

## Solving a global optimization problem greedily.

Planning trip is, fundamentally, a global optimization problem.

You want to maximize your experience with constraints, e.g. with limited time and money. There's also the regularization factor: if you spend too much effort on planning the trip and make sure you've got a plan for everything, you become more stressful and the trip itself lost its charm since there would be no surprise. Since it's such a good time to prove that my blog setup can render equations, here we goes:

$$
\begin{aligned}
& \underset{x}{\text{maximize}} & & \int^T_0{\text{Exp}(t, \pounds) + \alpha \mathbb{S}}\newline
& \text{subject to}
& & T \leq \text{Your free time} \newline
&&& \pounds \leq \text{The money you're willing to pay}
\end{aligned}
$$
$$
\mathbb{S} \propto \text{Time you spend on optimizing the problem}
$$

Beautiful.

Global optimization is hard (real world problem is never as simple as [linear programming](https://en.wikipedia.org/wiki/Linear_programming)). A reasonable alternative is to use [Greedy algorithm](https://en.wikipedia.org/wiki/Greedy_algorithm). So what I do is I make "bag of places / events" approach, by having an unordered set of stuff, each with their own constraints. Just like playing a Sudoku, I start with the one with the hardest constraint and start from there, greedily plan my next event.

Well, this doesn't necessarily applies only to traveling. That's basically the "start from something and focus on getting your left foot down and then right foot" kind of stuff from self-help book, but that's a topic for a different day.

## What do I care about?

Before I continue I have to confess that I'm always longing for city life (something I cannot get from my lodging in Silicon valley). I don't like beaches / mountains / great waterfall / national park. I don't understand the enjoyment of hiking. It's probably too late, but if you enjoy these stuff, you can skip the rest of the post. Things I do enjoy: kids running around in a park / public library / non-chain-store coffee shops / public transit that sparks joy.

### Whole day Events

This may be the reason I book for a trip: day long events that happens to be in a city.

Open house weekends are great: you go to 10+ places in a day, go inside buildings you don't have access to during normal hours, and meet friendly volunteers! For example, there's [Open House Chicago](https://openhousechicago.org/) and [Open House New York](https://ohny.org/).

Film fests: where you pay exorbitant prices for film ticket, just to feel the vibe. Again, every major city would have one. I plan to go to [TIFF](https://www.tiff.net/) someday but haven't yet...

Art fests: E.g. [FRIEZE](https://www.frieze.com/fairs/frieze-london-frieze-masters)

I'm also into games, so there's [PAX](https://www.pax.com/), and maybe someday I'll go to [GEN CON](https://www.gencon.com/) or [Comic-Con](https://www.comic-con.org/cc/)

### Short events

My preferable way of discovering them is via official government website. 

[Meet Boston](https://www.comic-con.org/cc/), [I Amsterdam](https://www.visitpittsburgh.com/) or [Visit Pittsburgh], again, every city has its own version of it. Go to the calendar page and look for what you're interested in. These are the events that would not be mentioned on TripAdvisor (since they are not regular event), or RED (the Chinese social media), since the users on the platform does not have good taste.

Some examples of the events I found this way:
- In Boston, there's the [duck parade](https://friendsofthepublicgarden.org/events/ducklingday/) on Mother's day, where parents dress their kiddos in yellow clothes and gather in Boston commons part for fun, and then go on a parade. 
- Or on the first Friday of every month Boston SoWa Art + Design District's artist studios are [open to public](https://www.sowaboston.com/first-fridays/)
- Maybe just some small scale [magic shows](https://trustarts.org/) in Pittsburgh?

### Tours

There're two types: that can be and that cannot be found on TripAdvisor.

The one that are not in TripAdvisor: just type in what you are thinking about in search engine, and you'll find it. I want to try donuts: [Underground Donut Tour](https://www.undergrounddonuttour.com/). New York is famous for its Bagels: [Bagel Tour](https://www.nycbageltours.com/). Chicago architecture: [Chicago Architecture Center](https://www.architecture.org/tours/).

Trip Advisor sometimes offers interesting tours, especially short excursion around the city. For example, this [hot ballon flight](https://www.tripadvisor.com/AttractionProductReview-g499421-d24962104-Balloon_flight_with_pick_up_in_CDMX_Breakfast_in_a_natural_cave-San_Juan_Teotihuac.html) in Teotihuacan. Before booking, check the reviews on other platforms that have more trustable user comments, and you can avoid places that doesn't seem good at all, e.g. the famous Stonehenge near London.

### Shows

When you see a "theater" in TripAdvisor's "top attractions", that means it's good time to also get some shows / orchestra / opera lining up, since a good theater indicates good performance.

Examples includes [Metropolitan Opera](https://www.metopera.org/) in New York (I watched Mozart's Magic Flute there), or [Bellas Artes](https://balletfolkloricodemexico.com.mx/) in Mexico city (Ballet Folklórico de México).

### Big city only

Sometimes there's so much unique activities in a big city. E.g. NYC. See this [reddit post](https://www.reddit.com/r/AskNYC/comments/93usax/another_unique_nyc_experiences_post/).

### The usual sightseeing places.

I like museums. I go to all of them. I like walking around districts with quaint little shops.

## Adjust accordingly

### What about night time

So museums closes at 5 or 6 p.m. There's still quite some time left before ending the day. I don't like bars or DJs. What I found is that I can:
- Go to local art house movie theatre. Well, that's because I love motion pictures, and a movie watched on a trip is different from the one watch at home.
- Go to improv, comedy or other late shows. I went to [The Second City](https://www.secondcity.com/) in Chicago two times and it's great.

You can simply get the tickets for these just an hour before it starts. For example, look for places to go when you are waiting for your dish at dinner.

### I got too much free time

Sometimes I finish what I want to do early and I got some free times in the day. 

To prepare for these situation (am I doing too much preparation?), I search "city + coffee shop" in reddit, and I marked all the recommended one. Then I go on good coffee hunt.

Or, open Google Map, look for places that's yellow, which means it's dense area. Head there and see what's there.

### I don't have enough time for X / I missed Y

Maybe the place I want to go is closed. Maybe I failed to get a reservation for an event. Maybe the line is too long for some particular restaurant and I cannot afford to wait in line. That's almost always guarantee to happen. I argue that "always not complete", or "there's something left" is the best state. Without completing all you ever want to do, there's always a veil of mystery in the whole experience. The best kind of travel is the one you can't wait to come back, not the one that prompts "I've covered every inches of ground here. Guess that's it".