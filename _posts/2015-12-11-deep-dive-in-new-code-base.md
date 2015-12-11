# Deep Dive in a New Code Base

During the last two days I learned how to navigate the uncharted waters of an unknown code base and framework. Love it or hate it but learning new material quickly is an important skill to have. I did this with none other than the backbone framework. The best way to learn a new framework is to build a small application from scratch, like a song player. But, if you are given a code base, the following points helped me grasp the material. 

#### Documentation is your friend

Read the documentation of the framework that you are using before referencing outside material. They have taken a lot of time to explain how it works in their docs. Backbone has excellent documentation to get started. If this is your first framework you will do a lot of digging to understand the concepts, but you will be surprised how much you can learn.  

#### Understand the High Level Decisions
Understand how the code is structured and try to see why they made their decisions. See why they choose to separate their code in that way. Same goes for frameworks. Understand the decisions behind the structure. 

#### Read the Code Comments
If there are comments in the code, read them. They are there for a reason. You can also comment out part of the code if you find it confusing. You can always ask someone if you cannot find an answer in reasonable time. Remember, that some rabbit holes are not worth going into. You can waste more time than necessary on a bug than it is worth. 
Specially if it is on company time, it is better to ask someone than to endlessly and aimlessly search for the answer. If you have the right tools and mindset to debug an issue, then it should take you reasonable time. It may look enticing, but don't do it. Hold the urge to be a stubborn developer and ask a senior. If you are the senior, then god speed. 

![](http://cdn.shopify.com/s/files/1/0728/8277/t/13/assets/promo-4.jpg?9334353060513128432)

#### Trace the code 
There are several ways to trace the code. One way is to console log the values. Another way is to think through what the code is doing. The best and easy way is to use dev tools. Becoming knowledgeable in them in a worthy investment 
* 
https://developer.chrome.com/devtools
* 
https://medium.com/javascript-scene/must-see-javascript-dev-tools-that-put-other-dev-tools-to-shame-aca6d3e3d925

#### Start with the Index Page
The index page is the first file in the application. As the first file. It is important to start reading there. You need to go to the source. The index page is the source on most applications, but not all. You must find that file on your code base. 
#### Understand repeated functions deeply
When reading on backbone, I got to see functions that got used repeatedly like get, set, on, trigger, extend, model. Read about them and know them deeply. Obviously a solid background in JavaScript or language of use will get you half the way there. Confusions on these concepts can lead to assumptions that will lead you to the wrong type of thinking. Clear them up before moving forward. 
#### Ask an Expert
Know when to ask a senior developer. It might be intimidating at first if you don't have the rapport, but don't be afraid. If you have tried a reasonable amount of time on the problem, stop and think about who might know the solution. Ask an online forum like stackoverflow if it is something that is not time critical. If you are like me, this might be something new. It can be uncomfortable to ask for help. I have found that most people are willing to help. Don't feel like you will be found out. Structure your question in a way that is easy to understand and really understand what you are asking before you ask. This should be easy if you have research the problem. List what you have tried and why it didn't work. Then listen and ask follow up questions. 

The most important thing to remember is to love the process. It can be overwhelming at first but when you break everything down, everything begins to makes sense. 

