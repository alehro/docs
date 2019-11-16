# Feature oriented structure of solution

## Table of contents

+ [Programming is all about sort and search. Or can you trust your collegue to sort socks?](part1.md) 

    More to read: Algorithms to live by - The Computer Science of Human Decisions - Brian Christian

+ [And nobody found that out before you? You cannot be so genius. No way.](part2.md) 

    Reference: Microsoft article, https://msdn.microsoft.com/en-us/magazine/mt763233.aspx?f=255&MSPPError=-2147217396

+ [Coupling, cohesion, DRY...](part3.md)

+ [Do not tell me about your experience. I am experienced too! Oh, I am offended!](part5.md)

    More to read: How to Measure Anything - Finding the Value of Intangibles in Business, 3rd Edition
                My life and work, Henry Ford 

+ [Oh, now you dare to make estimations! Unbelievable!]()

    Minimum 20%. Maximum 100%, 200%? Difference between success or failure.

+ [The happy end or just beginning. Reward for patient reader.](part6.md)


## Introduction

 Usually real life projects are big and cluttered. What is even worse they often structured not according to business requirements. They often structured as hello world projects where files are grouped by technical aspects (you know: Controllers, Views,...). The problem is that when the project grows this structure starts working against you. The bigger the project the bigger the part of time you spend on navigation in a mess. These all is very well described in MSDN article: https://msdn.microsoft.com/en-us/magazine/mt763233.aspx?f=255&MSPPError=-2147217396

Note regarding the article. 
The article is absolutely correct in the theory. The analogy about organizing computer files is perfect.
"To see what I mean, imagine if you organized your computer files in this same structure. Instead of having separate folders for different projects or kinds of work, you had only directories organized solely by what kinds of files. There might be folders for Text Documents, PDFs, Images and Spreadsheets. When working on a particular task that involves multiple document types, you would need to keep bouncing between the different folders and scrolling or searching through the many files in each folder that are unrelated to the task at hand. This is exactly how you work on features within an MVC app organized in the default fashion."
And then
"The reason this is an issue is that groups of files organized by type, rather than purpose, tend to lack cohesion. Cohesion refers to the degree to which elements of one module belong together..."

The reference to "cohesion" term is absolutaly brilliant. Why it is? Because in traditional project organization 


The article still has quite a lot clutter in the implementation part. I have never tried the Areas feature because I work usually with Angular + Web API projects. So, I do not have .cshtml files and do not need related routing setup. Let us describe perfect case. The case when I have full freedom and which results in Feature Oriented Structure (FOS) of project folders. In the past years this happened quite often, so perfect doesn't mean purely theoretical and not tested. In fact the approach is very well tested on several successful projects. What I do in perfect case. I make single file hierarchy. This implies that essentially I put everything into single Visual Studio ASP.Net project. This is of cource not possible if you split domain into separate project. Such splitting leads to duplicating of many folders. Unfortunately collegues usually don't end up with two projects. They do have separate project for POCOs and for Services. These already amounts to 3 projects. The folder structure gets tripled. Actually the structure gets quadrupled because collugues usually keep controllers in separate Controllers hierarchy and views in another one (JS/TS and html files. Thanks gods they learned to not separate those files too ). At this point as project grows happen two bad things. 
1. People stop making folders when it is needed. Dev thinks: "Why bother if the structure is already a mess. To be correct I will need to make 4 copies of that folder. And well, this is quite a lot of clatter. The tree will grow a lot. (Author: Seeng such trees I usually imagine bush. Yeah, and what you prefer finding something in bushes or on tree. I prefer tree.) I put it to that pile. Every professional dev knows how to open files fast, right? The amazing "Ctrl+.". So, if somebody doesn't know then it is his problems. Actually I hope most doesn't know - they will work slower than me. Hah!! This is of course exagragation. Usually having the quadrupled structure devs just abandon any its maintanance because it is just a pain.
2. Navigation becames more and more painful. When new dev comes to the project (And this happens in our company more and more often. I average I see new projects once in about 3 monthes) the first thing he needs is for get familiar with basic notions of domain. Would we have FOS on the project he could do that just by looking at the single root folders structure. But we don't have it. So, trying to understand something from folders structure is very unproductive. Features are reflected in folder name quite occasionally. E.g. often they are not reflected. Often they are intermingled with uselless technical clutter like: Controller, View, Modules, Domain... TODO: continue here

Being unable to restructure the projects in most cases, I have created this extension. It has proven itself as indispensable tool to stay focused only on things I need. There is actually quite a lot of other reasoning and I could go on and on about it for quite a long time (this was really a pain for many years). In particular reasons from the modern neuropsychology and a book "Algorythms we live by" but I keep it for next time.

## Usability notes

The extension is developed to solve most critical productivity problems. So, if you don't find UI for something, it is okay to edit config file by hands. It is json file with simple structure. It is located in root of solution: parallelFolders.json.

