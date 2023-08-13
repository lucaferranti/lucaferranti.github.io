@def title = "Open-source around the world stop 1: Graz"
@def pubdate = Date("2023-07-20")
@def img = "https://avatars.githubusercontent.com/u/74617459?s=200&v=4"

Summer 2023 has been very exciting, I namely had an **open-source tour around the world**, 3 trips in 3 continents in 30 days, all related to open source!


## Step 1: Pluto dev meetup in Graz

The first trip was in Europe, particularly in Graz, Austria for the Pluto dev meetup. Funnily, this was pretty much ex tempore.

So, I have been developing [FuzzyLogic.jl](https://github.com/lucaferranti/FuzzyLogic.jl) and I am planning to use it in my teaching next year.
Particularly, I was determined for my teaching to setup a website like the [Computational thinking in Julia](https://computationalthinking.mit.edu/) taught at MIT.

I started reverse-engineering the website to adapt it to my teaching, while working on it I thought *I have to do this anyway for my teaching, probably more than once, why not making a generic template for everyone?*.
So I started working on a template, with a simple goal, make for every teacher as simple as possible to build a website like that, automating all "web stuff" as much as possible, so that teachers could focus on the most important thing: material development and pedagogical aspects.

While working on the template, I ended up commenting on [an pull request](https://github.com/mitmath/computational-thinking/pull/124#issuecomment-1600836056). In my comment, I mentioned the template I was developing. A few minutes later, I got a reply from the Pluto main developer inviting me to have a short chat. Apparently, they liked my idea and mentioned there was going to be a developers meetup in Graz.

So all of sudden I am on a plane, heading to Austria to discuss about how to make teaching (with) Julia more engaging and successful.
The meetup in Graz was very productive, I met the Pluto.jl core devs, we had a lot of very interesting discussions about higher-education pedagogy, courses planning, and how Pluto.jl can help to make teaching (and teaching preparation) more productive and engaging, both for teachers and students.
I also got a much better understanding of Pluto.jl internals, "server stuff" and how to deploy and host a dynamic website.

Before going further, if you are wondering *What the heck is this Pluto?*.
[Pluto.jl](https://plutojl.org) is a notebook format, similar to jupyter, with the goal to make programming reactive and interactive.
Particularly, it strives to have pedagogically sound design principles and it is hence very well suited for education.
If you were not familiar, you should really check it out (see e.g. some sample notebooks [here](https://featured.plutojl.org/)).
After that, you might be more interesting in reading my 2c contribution in enhancing teaching with Pluto.

### Concrete stuff: Computational thinking template

As mentioned, I got sucked into the Pluto dev community via this template.
My motivation and goal for this template are simple -- I think the *Computational thinking with Julia* is a masterpiece showcase of using Julia for teaching and everyone using Julia in their teaching should be able to do something like that.
With this template, I want to make building courses like that more accessible, automating all the "webpage bulidng" parts so that teachers can simply write their teaching material as Pluto notebooks and let the magic happen.

So, what does this template do in practice? It has a built-in small static site generator called PlutoPages written by Fons (should be moved to its own package soon), which takes the teaching material (Pluto notebooks or markdown) and constructs the html of the website.
Here is a sneak preview of what the tempate looks like. Find the repository [here](https://github.com/juliapluto/computational-thinking-template) and the template website [here](https://juliapluto.github.io/computational-thinking-template/). 

At the time of writing this blog post, the template is usable, some features highlights:

- You simply need to fill your class metadata in a given file, after that the homepage, table of content and tracks are automatically built.
- The template is self-documented, in the sense that the sample material in the template are the documentation on how to use it.
- Automatic preview on pull request (and friendly bot telling you where to find the preview).

Currently, it can build static websites, but I still have two goals:

- *Supporting precomputation*. There is a [pull request](https://github.com/JuliaPluto/PlutoSliderServer.jl/pull/29) in PlutoSliderServer.jl about supporting precomputation. The idea is pretty simple, for all possible interactive elements in the notebok (sliders, buttons, etc.), precompute all possible states.
  This will give an illusion of the website being dynamic while it is actually static. While it is not the best solution for big animations or in cases of "real-time animations", such as interacting with webcams, this would make developing small interactive websites seamless for teachers.
-  *Better hosting support* It is in principle possible to set-up one's own server and host the website there. However, this is not necessarily trivial for every teacher, a next step is to better document this, so that server noobies like myself can do it, as well as making the process as easy as possible with more autoamtion.

### Concrete stuff: PlutoGrader.jl

You may have heard of [nbgrader](https://nbgrader.readthedocs.io/), a cool piece of software that allows to write exams as Jupyter notebooks, hide the model solutions, automatically grade students' solutions, give feedback and export the file results.
Well, you probably guess where I'm heading. While being on the plane to Graz I thought, why not having PlutoGrader.jl, so I started prototyping it.

At the time of writing, this is very very (very) early WIP prototype, but it is starting to take a nice shape and I am fairly confident I will be able to use it next year in my teaching.
[Here](https://github.com/lucaferranti/PlutoGrader.jl) is the link to the repository, feedback welcome.

The workflow is currently roughly the following

1. The teacher writes the exercise sheet with model solutions, these delimited by special comments. They also add tests to check students' solutions.
2. PlutoGrader.jl removes the model solutions, giving the assignment to be distributed to students.
3. Students start workin on the assignment, since it is Pluto.jl they get immediate feedback on their work by seeing what tests are passing and what not. If some tests fail or error, they can inspect the stacktrace.
4. Once students have returned their assignments, teachers start grading. This adds a special form to each exercise. By default, coding tests are autograded based on the number of passing tests. However, teachers can overwrite the default score and add textual feedback to each exercise.
   A cool thing I learned, is that Pluto.jl supports cell-level metadata! Thanks to this, the teachers' feedback is persistent in the notebook and it is not lost whenever the notebook is refreshed.

Here is a sneek preview of what it looks like

![](/posts/2023/07/pluto_grader.png)

This is looking good, but a lot of things are coming, namely

1. export grades in csv and/or xml format
2. Automatically add a form on top of the notebook for students to fill their basic information (name, student number).
3. your feature request?

Overall, I am pretty happy with this and hopefully it will help others too, making teaching with Julia and Pluto easier and funnier.