@def title = "JSoD"
@def pubdate = Date("2021-03-27")
@def img = "/assets/posts/jsod/juliaintervals-logoTest.svg"

## Introduction
During last fall I participated to the \elink{JSoD}{https://discourse.julialang.org/t/the-julia-language-x-gsod-x-jsod-2020/45216}, a program aimed at developing the documentation of packages within the Julialang community.

My mentor was \elink{dpsanders}{https://github.com/dpsanders} and I worked for JuliaIntervals, an organisation developing packages related to interval arithmetic, which is a mathematical framework for rigorous computations.

## Final deliverable

The final deliverable of the project is a webpage for the JuliaIntervals organisation containing documentation and learning materials The webpage is available at \elink{juliaintervals.github.io}{juliaintervals.github.io}, here is a screenshot.

\fig{/assets/posts/jsod/homepage.PNG}

The webpage is divided into $4$ sections
- **Tutorials:** The articles in this section (one for each package) target new users and aim at teaching the basic functionalities of each package.
- **Applications:** The articles in this section are "advanced tutorials" targeting users who have used the packages before and want to learn how to apply those to solve real-life problems.
- **Explanations:** This section contains background explanations, such as the theory behind the algorithms used by the packages.
- **API DOCS:** This section contains the documentation (docstrings) of the functions in the packages. The content of the section resembles the documentation automatically generated with Documenter.jl, the logic to generate these API DOCS automatically in Franklin was written by myself (with a lot of help from @tlienart)

During the project particular emphasis was given to the workflow set up, to minimise the amount of manual work. Franklin.jl already offers a great integration with Literate.jl, which allowed me to write each tutorial only once as a Julia script and automatically generate all html and notebooks at once. I also wrote a couple of functions to automate the workflow even more, mainly one to automatically generate all navigation bars and tables of contents from a single json file and one function to automatically export the docstrings of the functions in the packages and format them à la Documenter. The seamless workflow allowed me to focus on the most important part: writing!

## Future work
	While the webpage has already the basic material and documentation for the JuliaIntervals packages, it will need to be maintained up-to-date as the packages evolve. Furthermore, there is always room for improvement and more content, for example more articles about theoretical background and applications can always be added. Also, while the webpage is already a good resource for end users who wish to use the packages for their research, it could have more technical details about the internals of the packages for people who wish to contribute. From now on I will continue as a maintainer of the webpage, keeping improving the quality and quantity of its content.

## Acknowledgement

I want to express my gratitude to David P. Sanders for the guidance during the project and the constructive feedback during the development of the webpage.  I want to thank also \elink{@tlienart}{https://github.com/tlienart}, the author and maintainer of Franklin, for his amazing availability in helping in slack with the several Franklin and web development issues I faced during the project and  \elink{@cormullion}{https://github.com/cormullion} for creating the original idea of the JuliaIntervals logo and  helping me with Luxor.jl for the graphics design. Finally, a broader thank to the Julia community and the JuliaIntervals community in particular for the welcoming and friendly environment.