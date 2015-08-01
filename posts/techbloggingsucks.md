---
title: Why Technical Blogging Sucks
tags: technical blog, blog, git, github, hosting
published: true
---

Technical blogs (like this one!) are one of those groaner things we new engineers are expected to produce, along with resumes and websites that work in IE6. The whole process kind of sucks, though! Some of the problems I've experienced include:

- **Tech blogs are hard to set up**, in a *technical* sense. Setting up hosting, thinking of quirky-but-not-too-quirky domain names and then buying said names, etc. It's not pleasant.

- **Tech blogs require knowledge of traditionally-non-engineery subjects** like *design*. I don't care what my content looks like, I just want it out there.

- **Your content isn't easily discoverable.** Unless you're engaged in and good at another distinctly unpleasant and un-engineery act--marketing--there's no way of knowing if anyone will actually read your material. It can feel like you're yelling into the void. 

- **Your content isn't automatically connected to other, similar content.** Producing material on javascript, for instance, should optimally connect you to a network of other people in the same or similar boats.

- **It's discouraging to write on a nearly-empty blog.** You have to write a certain amount of posts before you feel like your website isn't sparsely populated.

- **Embedding code -- especially back-end -- is difficult, if not impossible.** Code blocks are ugly and lack line numbers or nicely formatted comments, and there's often no way to actually run your code in the browser so it can be seen in action.

- **The process of writing a technical blog is divorced from the process of writing code.** Jekyll + GitHub Pages is a nice example of using the same workflow for both programming and blog writing. 

- **Blog posts go out of date as tech changes**, requiring some combination of a) readers carefully vetting the material they read to make sure it's still relevant, and b) authors exerting an enormous amount of effort updating their back catalogs.

There have been attempts to solve some of these problems. [Medium](https://medium.com/) is one of the bigger players in the "easy to setup, content-only blog" space. And they're a lovely site--for writers. However, no support for embedded runnables, lackluster code block support (embedding Gists doesn't work, for instance), and a tagging system not optimized for technology-related queries makes Medium not the best platform for technical blogging.

My thesis team at Hack Reactor and I are working on a solution: a blog platform combining the workflow of Jekyll, the ease of hosting of GitHub Pages, the community editing of GitHub Pull (via Pull Requests to blog posts), the discoverability, tagging, and community of posts of Medium, and (if we can pull it off!) embedded runnables and Gists!

If it works out, maybe I'll move myself on over there. 
