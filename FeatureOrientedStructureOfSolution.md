# Feature oriented structure of solution (FOS)

*I apologize in advance for the messy article structure and amount of brackets. Though I have tried to apply some principles of structuring knowledge I advocate for: using trees and tree flattening*

## Why, or just to start from something

 Usually real life projects are big and cluttered. What is even worse they often structured not according to business requirements. They often structured as hello world projects where files are grouped by technical aspects (you know: Controllers, Views,...). The problem is that when the project grows this structure starts working against you. You find out that you don't care about technical terms. All you need is well structured domain knowledge - the very thing which is missing. The bigger the project becomes the bigger the part of time you spend on navigation in a mess...  
 The idea is not new. For example it is quite well described in MSDN article: https://msdn.microsoft.com/en-us/magazine/mt763233.aspx?f=255&MSPPError=-2147217396 

The article is absolutely correct in theory. The analogy about organizing computer files is perfect.
>"To see what I mean, imagine if you organized your computer files in this same structure. Instead of having separate folders for different projects or kinds of work, you had only directories organized solely by what kinds of files. There might be folders for Text Documents, PDFs, Images and Spreadsheets. When working on a particular task that involves multiple document types, you would need to keep bouncing between the different folders and scrolling or searching through the many files in each folder that are unrelated to the task at hand. This is exactly how you work on features within an MVC app organized in the default fashion."  

And then
>"The reason this is an issue is that groups of files organized by type, rather than purpose, tend to lack cohesion. Cohesion refers to the degree to which elements of one module belong together..."

The article still has quite a lot clutter in the implementation part. For example the notion of Areas doesn't belong to domain. Hence it should be avoided in the solution structure.
Instead of trying to critisize the articte in attempts to find the best solution structure let me describe by approach. I call this approach as Feature Oriented Structure (FOS) of business project folders (solution). In the past years I have applied it quite often. The approach is very well tested on many successful projects. 

###  The FOS approach in short
 All domain knowledge should be put into single file hierarchy. Only terms from domain can be used for folders. If you have duplicate names in folder names they should be considered for re-structure of some kind to eliminate. Synonyms in names of folders and files should be considered as duplicates.

### Traditionally oriented structuring (TOS)
Usually solutions are structure traditionall. The domain is being split onto several separate projects. Such splitting leads to duplicating of many folders. Usually there will be separate project for POCOs and for Services. These already amounts to 3 projects. At this stage the folder structure is already gets tripled. The structure is actually quadrupled because collugues usually keep controllers in separate Controllers hierarchy and Views in another one *(JS/TS and html files. Thanks gods they learned to not separate those files too)*. At this point as project grows happen two bad things. 
1. People stop making folders when it is needed. Dev thinks: "Why bother if the structure is already a mess. To be correct I will need to make 4 copies of that folder. And well, this is quite a lot of clatter. The tree will grow a lot. *(Author: Seeng such trees I usually imagine bush. Yeah, and what you prefer finding something in bushes or on tree. I prefer tree.)* So, instead I put this the new file to that pile. Every professional dev knows how to open files fast, right? The amazing "Ctrl+.". So, if somebody doesn't know then it is his problems. Actually I hope most doesn't know - they will work slower than me. Hah!! This is of course exagragation. Usually having the quadrupled structure devs just abandon any its maintanance because it is just a pain.
2. Navigation becames more and more painful. When new dev comes to the project the first thing he needs is to get familiar with basic notions of domain. Would we have FOS on the project he could do that just by looking at the single root folders structure. But we don't have it. So, trying to understand something from folders structure is very unproductive. Features are reflected in folders names quite occasionally. Often they are not reflected. Often they are intermingled with uselless technical clutter like: Controller, View, Modules, Domain...

### Why having 3 projects in solution is bad from the point of sort and search.
*I am considering traditional structure (TOS) comparing to FOS. And I am presuming that the traditional developer to be perfect. He is so disciplined that he will maintain the same amount of domain details in the structure as I would do in FOS. So, if we take N as amount of domaint terms we wont to incorporate into the tree, then it will be the same for both TOS and FOS*

3 projects mean amount of folders multiplied by 3 *(comparing to single root - FOS approach)*. When we work on solution our eyes and brain do two operations again and again. These operations are sort and search. When we add new file *(possibly creating new folders)* we do sort. When we need to open some file or just browse to understand realtionsheeps we do search.

#### What means multiplier of 3 in terms of sort in tree data structure. 
Basically we are talking about insert operation. For binary trees effort to do it is O(depth of tree). For alphabethical trees (folders and files) there will be multiplier but lets ignore it for now. So, since we have 3 roots we have (3 * N) of nodes it tree *(N is the amount of terms from domain we want to incorporate in the file tree)*. Hence the resulting work to be done is 3*O(depth of tree). All remember how difficult it is to find proper place for a new file. Now you know that working in traditional structure it is 3 times more difficult than in FOS. Next time you put new file in a mess because of placing it correctly was just too hard remember about that.

#### What means multiplier of 3 in terms of search in tree data structure. 
Computation complexity *(effort)*  is N * log N. So, we have 3 times more here again. Next time when your eyes hurt remember that you had a chance to avoid that.

Similar justifications can be applied to excessive subfolders. By excessive subfolders I mean all folders with names not related to domain. Traditional cases: Controllers, Views, Models. Usually we have at least one such layer of subfolders and usually it is at the top of the folders hieararchy in traditional structure. Models are usally in the separate project so this subfolder doesn't add significant fragmentation. Controllers and Views are usually must have in TOS.  It means that we have at least multiplier of 2. *(If you look at real project you will actually find many excessive subsolders. So, usually the average multiplier is 3 or more)* 

Summarizing the estimations we have 6 times more work to do by our eys/brain. Dispite this work is pretty stupid and simple the amount of it is tremendous. For example let's presume that you need to revise 10 issues a day. Let's take simple typical issue of adding some information to a page, e.g. additional field from database. It means that you need to add changes to 4 files: html, Typescript controller *(service is optional for FOS people but must have for TOS ones)* (Typescript DTO definition is optional for people generating that automatically but must have for all others), So, it means that you need to do search 40 times at least to open the files. So in average every 10 minutes you need do that stupid, simple yet exhausting operation. 

More to read about application of algorythms to such not traditional areas like mental efforts and human behaviour see at: "Algorythms to live by"

#### Why such simple mental operations are exhausting?
Here is short explanation. A man has limited amount of mental energy per day. Every conscious mental effort and every decision takes some energy from your daily limit. Significant part of search and sort operations from the above get done consciously.   
Here we came to the point where we do math. Let's take 50% as amount of conscious search/sort. It means that every 20 minutes you take waste some energy. At some point daily limit becomes depleted and you stop working effectively. For example you start stupidly staring at screen in desperate attempts to understand what your current task is about. It means that you stop working.   
This is of course very raw and speculative in theory but you should already know such feelings from everyday practice. If you don't notice them then I hope after reading the article you will start.
As I remember similar concepts are explained in more depth in the book: "Your brain at work", David Rock

#### Excessive project smell

Of course there are many situations when separate project in solution is absolutely fine. In general if it relates to isolated part of domain or solves some technical problem. For example: GUI components, server components, etc. Just look at the project and see if it addresses only stricly localized small part of domain or doesn't use it at all then it is fine. It doesn't smell. If it uses a lot of words from domain then it is the smell. Such examples are separate project for models and services. They will end up duplicating all the domain semantic tree and you will have situation with multipliers described above.

#### FOS evolution in project

Feature oriented structure is a leaving beast. Hence it can't be perfect. In fact it will be unavoidable far from perfect. And this is the perfect way to do that.  
Main reason of why FOS can't be perfect is that trees are actually not very good for representing knowledge (domain). We use trees only because it is best of tools we have. Typical example of case which should be treated carefully. We have: Client, Order, Seller. When starting development we may get a task to implement client with orders. So, at this point we will think that Order belongs to Client and we put Order subfolder under Client folder. The problem is that Order relates to the Seller with the same amount of strength and at some point you might feel temptation to move Order folder to seller. So, the only correct way is to put all 3 folders at the same level. 

This was an example of most typical and at the same type conflicting situation happening in FOS. That is the reason that file trees in FOS usually have little depth of 1-2 levels. 3 levels is already rare case. For small and medium size projects this is not a problem at all. Let's suppose we have 10 folders at first level *(Clients, Orders, Sellers, Products,etc)*. It is comfortable to have up to 10 files in the folder *(remember about amount of things brain can symultaneouly operate on effectively)*. So, we already have potential for placing about 100 of files with all comfort. Now if we add second layer: (Client->Details, History, Whishlist; Product->Details,Providers,Versions; etc.) Common case is having about 3 folders at this level. So, this is a reservoir for 300 files. Etc, etc use imagination *(mine is obviously limited)* or better look at real projects. Event traditionally structured projects have a lot of examples of structuring domain knowledge. Just mentally cut all the excessive folders, merge trees and you get it...


## Literature

- "Algorythms to live by", Brian Christian, Tom Griffiths. This book is to think about search/sort operations our brain does while working on code.
- "Your brain at work", David Rock. This is about our brain. Provides some understanding of the price of the search/sort.
- "Data Structures and Algorithms". Aho Hopcroft, Ullman. This is to remind about trees (apply to folders in our case), computation complexity etc. Good old classics.
- Here should be something about code readability and simplicity. Can't recollect for now. May be even something of Donald Knuth or Leslie Lamport.
- The approach closely resembles Domain Driven Design ideas. There is a lot on this subject in internet. E.g. wiki. Most useful notion from DDD in context of this article is "Ubiquitous Language".