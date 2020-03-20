<!--
.. title: Starting my Sabbatical
.. slug: starting-my-sabbatical
.. date: 2020-03-20 20:07:49 UTC
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

Super exciting news: I'm starting my sabbatical. Through a combination of luck, timing, and hard work on the setup, I'll be spending the time working on computational oncology. Specifically, I'll be joining an existing collaboration between two fantastic labs at Johns Hopkins. It turns out that my statistical physics, computer science/programming, mathematics, and biophysics backgrounds are an excellent fit.

So now it's time to catch up on the science from a different field. I'm starting with a few Coursera courses.

<!-- TEASER_END -->

The computational side involves learning some modern data science. Excellent. I've been meaning to update my formal knowledge here for a while. The Johns Hopkins Data Science courses on Coursera came highly recommended by several people, especially the courses by Brian Caffo and Jeff Leek. So, which ones to check out?

Given the instructors and my goals, there are two specializations (groups of courses)

[Genomic Data Science Specialization](https://www.coursera.org/specializations/genomic-data-science)

* Has Jeff Leek
* Is mostly based in Python

[Data Science Specialization](https://www.coursera.org/specializations/jhu-data-science)

* Has Jeff Leek
* Has Brian Caffo
* Is mostly based in R

So, it looks like the right thing to do is to do the Genomic Data Science Specialization, and then pick and choose courses from the Data Science Specialization to supplement. I thought about trying to get the certificate, but I don't see any real benefit to doing that for either of these ... I think I'm at the point in my career where knowledge and skills trump official certifications. Just to make some notes for myself for later, here are courses that sound particularly interesting from the Data Science Specialization

* [Practical Machine Learning](https://www.coursera.org/learn/practical-machine-learning) ... an alternative to this might be [fast.ai](https://www.fast.ai/)'s ML courses. I've heard that their stuff is quite good.
* [Exploratory Data Analysis](https://www.coursera.org/learn/exploratory-data-analysis) has got to be worth a quick look through. Interesting stuff can be done in Python, I'm sure.
* [Statistical Inference](https://www.coursera.org/learn/statistical-inference)

I started with Course 3, Python for Genomic Data Science. I did the whole thing in about a day. The final project was interesting, and reminded me of a few things

* **It's important to have a good set of test data.** In this case, I wrote some buggy code that got cleared up much more easily when I just started writing sample FASTA files.
* **You need to become comfortable with the data formats.** Similar to the above, I spent a few tens of minutes trying to use pre-written data files because there was some weird mental hurdle keeping me from just playing with the files directly. As I know from lots of previous research experience, being afraid to play with data directly is just going to hurt.
* **Writing lots of small functions that you tie together makes it easier to play with data.** In the final project, they described the types of questions you'd be expected to answer. I wrote some not-so-well-factored code that answered their example questions for their example data set. Then their actual questions were a bit different ... and my answers weren't quite right. Refactoring everything into small, reusable pieces made it easier to poke at the actual buggy parts. This is likely going to be an extremely important lesson as I move into bigger data sets.
* **I hate "gotcha" questions.** I skimmed the first few lectures, took the first quiz, and then quickly moved on to the final. That was fun. I'm vaguely tempted to get the certification, but it looks like I have to answer all of the quizzes to do so. One of the quizzes was (I think) just trying to get you to debug code, but a lot of the time, that comes across as "gotcha" style questions, which are less fun when you're already competent at the language.

My original plan was to have enough self respect that I got 100% on everything. I'm happy with my 100% on the final. I'm going to be fine with missing a couple of gotcha questions on the way to the certification :). It's possible that I missed something by skipping the lectures, but I like the flexibility here. I can just get what I want/need, and go back for more if necessary.

Anyway, I hope everyone is very impressed that I now have a super official Coursera Certification!
