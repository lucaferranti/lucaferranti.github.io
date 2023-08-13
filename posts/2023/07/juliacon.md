@def title = "Open source around the world stop 2: JuliaCon"
@def pubdate = Date("2023-07-31")
@def img = "https://juliacon.org/assets/2023/img/boston_2800.png"

My open source trip around the world continues, 3 trips in 3 continents in 30 days.
It is time for the second one, a very special one.

## JuliaCon, Boston, US.

The second continent is America and the second stop of my tour is nothing less than [JuliaCon 2023](https://juliacon.org) itself, this year hosted at MIT, in Boston, US.

Pretty much everyone who knows me knows that I love programming in Julia.
I started getting involved in Julia in late 2019 and gradually became more and more active in the julia community.
I started with Julia season of docs, writing documentation about interval arithmetic.
Next, I was twice in the Google summer of code program, coding interval arithmetic stuff in Julia.
Now, I work as Julia software developer, use Julia in my research, have given [a tutorial](https://www.youtube.com/watch?v=oHsLmaHSHd8) about developing libraries in Julia, created a [julia community in Helsinki](https://julia-users-helsinki.github.io/) and even organized a [small conference](https://juliareach.github.io/juliareach-days-3/) about interval arithmetic and reachabiltiy analysis in Julia!

So, summa summarum, I consider myself pretty enthusiast. Now, you probably noticed the date when I started, late 2019.
Unfortunately, we all know what that means, COVID! So yeah, so far my Julia involvement has been remote, which is why I was very excited about finally meeting people at JuliaCon!

### Arriving to Boston

The flight was surprisingly short and painless. Arrived to Boston, I took a cab to MIT, had a look around and prepared to go to my airbnb.
Accoring to google maps, the distance was 4.5 km, it was hot and humid, nevertheless I spoke my famous last words *I can walk that far*. And make no mistake, I did it!
After getting to the airbnb and taking a shower I decided to make some sightseeing and went to Harvard (I wonder why people say it is hard to get it, the doors are always open).


### JuliaCon

JuliaCon was in the very funny-looking computing science building of MIT. Arrived there, I registered and got some swag (t-shirt and stickers).


![](/posts/2023/07/mit_building.jpeg)

The event was 3 days long and there were a lot of interested talks, indeed a lot of times I felt like the Buridan's ass, stuck between lecture rooms.

Some highlights:

- The workshop about [Genie.jl](https://genieframework.com/) was very interesting. Coming myself from a compuational background, I find refreshing to see the Julia community going beyond scientific computing and being used also in web development. I found Genie very intriguing and I hope to use it myself soon too.
- Stephen Wolfram was a keynote speaker.
- The status of Julia was very interesting! A lot of very cool features coming in the upcoming julia release (1.10), a completely new compiler-fronted ([JuliaSyntax.jl](https://github.com/JuliaLang/JuliaSyntax.jl)) with better parsing error messages, shorter and more friendly stacktraces. Huge improvements in latency and precompilation. Indeed, I think people complaining about "Julia being slow at the beginning" heard that a few years ago and haven't updated their belief. If you are one of those people, give julia another try, you'll be amazed!
- In parallel to JuliaCon, there was a [special conference](https://math.mit.edu/events/ase60celebration/), celebrating Alan Edelman 60th birthday. This had a lot of talks related to numerical linear algebra, which was very cool. I also got to meet some "rock stars" like Gilbert Strang and Nick Trefethen!
- One JuliaCon was not enough, this year we have 2!! Yes, there is a second one in December in Eindhoven, check it out [here](https://juliacon.org/local/eindhoven2023/). I will probably be there too.

Overall, there was a very cool atmosphere, with a lot of interesting chats. Everyone was very humble and friendly.
This is a very cool aspect of open-source, everyone is so enthusiast and dedicated!

### My talk: FuzzyLogic.jl

I also had my talk, where I presented [FuzzyLogic.jl](https://github.com/lucaferranti/FuzzyLogic.jl).
If you don't know what that is, it is a library for automated reasoning using fuzzy logic.
In a nutshell, while traditional logic is binary (true or false, zero or one), in fuzzy logic the truth value is an number from the interval ``[0, 1]``.
This allows to model uncertainty, particularly vagueness. In a way, fuzzy logic resembles the way humans think.
If we think of an imprecise concept, such as *being tall*, it cannot be defined exactly. When is someone tall? Someone 2m is definetely tall, what if someone is 1.8? or 1.7? or 1.6?
Even if I choose an arbitrary threshold for "being tall", does it make sense to say someone is "not tall" if they are 1mm shorter?
Instead, with fuzzy logic, the truth value of the proposition "being tall" smoothly goes from 0 to 1 as the height increases.

Surprisingly, I prepared my slides as early as 2h before my talk, however, before walking into the room, I saw a demo of a controller keeping a [furuta pendulum](https://en.wikipedia.org/wiki/Furuta_pendulum) in equilibrium.
I thought, I can do that with my library, and 1h before my talk I updated the slides with a small demo of a fuzzy controller for an inverted pendulum.
The very cool thing is that I could almost effortlessly plug my fuzzy controller into [DifferentialEquations.jl](https://github.com/SciML/DifferentialEquations.jl) and it just worked. Julia composability is so cool!

Here is my talk if you want to watch it (Note my bright yellow belt, apparently that is now "my thing" in the Julia community). You can also find the slides [here](https://github.com/lucaferranti/talks/juliacon2023).


~~~
<iframe width="560" height="315" src="https://www.youtube.com/embed/CrIAsPmG2a0?start=18217" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
~~~

I am pretty happy with how the talk went, I had good time management, ok pace and managed to fit perfectly the given time slot.
There were some nice questions from the audience and I chatted with some people before and after about the library. FuzzyLogic.jl even got its first citation! Shout out to [Copulas.jl](https://github.com/lrnv/Copulas.jl).

![](/posts/2023/07/fuzzy_logic_citation.jpeg)


### Hackathon

The last day was the hackathon! A very cool event where cool people sit together and code cool stuff!
It was very fun to see the atmosphere and enthusiasm.

Personally, I kept working with a friend from the Pluto dev on the [computational thinking template](https://github.com/juliapluto/computational-thinking-template) (see also my [previous blog post](/posts/2023/07/graz)).
We went through the process of setting up a server and deploying the website, identified pain points and made some progress in making the process smoother. Overall pretty productive!

### Acknowledgements

I want to thank my PhD supervisors, Jani Boutellier and Heidi Kuusniemi at University of Vaasa, for being supportive with my open-source scientific computing "hobbies", and especially for paying my trip to JuliaCon.