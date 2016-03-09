#### General Questions:

* What did you learn yesterday/this week?

####What excites or interests you about coding?

- What I love about it is you get to engage in a creative, design-oriented activity that is done in a rigorous, systematic way. 
- You get to be nerdy and look for optimizations. 
- It’s a continual learning process that deepens my ability to communicate and teach. Learning Haskell makes me a better person. 
- My first work experience showed me how exciting working as an engineer can be and how I can benefit communities through my work. 
- Software engineering is a means through which I can be proud of building a service or utility so new users aren’t stuck with old user’s problems.
- At the end of the day, the thing that keeps me going is getting to help people with actual problems. 

#### What is a recent technical challenge you experienced and how did you solve it?

Recently, I led a team in building MatchJS, a platform that connects JavaScript developers with mentors and mentees. This involved facilitating standups, engineering the build process for continuous integration, and creating a Git workflow. I was also responsible for architecting a user exploration feature on the Angular client that facilitates mentor matches. This was achieved using an Observable based implementation with RxJS to sync concurrent requests from a PostgreSQL-backed REST API. 

One technical challenge that we faced: I was implementing a search bar.

The search bar is meant to display all users in our database that represent the results of a filter. So a user can add a tag “San Francisco”, “Angular”, “React” and see users in San Francisco that have Angular or React as teachable skills. 

My first naive approach was on the page load I query all possible users so the client has access to all of that data and then filter what data is displayed. However, if I have 1000 users from 50 cities and the user only cares about people in San Francisco, a lot of that data is wastefully sent and it slows down the site.

So my next approach was to have different queries made to the DB based on the user input. However, since you can continue to add tags to the query, when you implement it, the user can potentially make several different queries in a row depending on their input. Since I’m using Angular and using a promise based implementation, the displayed result is going to be what the longest promise returns. 

One problem is we can’t control the time it takes for that promise to resolve. So if you had a delay on the second query that was executed and it was longer than the third, the second one would display and then the third. However, we don’t want to display the one that takes the longest first, we want to display the last query that was made based on user input.

One thing I thought of was using Debounce. Debounce is nice because it makes sure a certain task isn’t fired too often within a certain amount of time. It limits the rate at which something can fire. However, with debounce you need to specify a certain amount of time for rate limiting. This can still lead to weirdness, because depending on what your time you set is, you could still have weirdness in the UI or your UI could appear slow.

The thing is, Debounce is still very helpful to use to avoid unnecessary server queries, but we still can have weird UI issues.

So I did some research and found that a really good use case for syncing these requests so that the user always got the last one was to use RxJS. 

RxJS is an API for transforming and querying streams of data. In this case it’s a stream of user events. We used an RxJS Observable, which represents a collection of values over time. RxJS provides really nice utility functions for handling asynchronous operations.

With respect to my search bar, we use an observable and a function that gets the latest value in that collection. Within the implementation of RxJS it has a way to cancel out promises and it will make the UI a lot nicer. We can still use debounce in addition to this to protect the server from too many requests. 

What database did we use? Why?

For this project we used Postgres for a few reasons. Our data consists of users who want to discover and match with other users, so the data was highly relational. 

Postgres supports SQL and we had predefined relationships between users.

However, with the case of the chat functionality within our application, we went ahead and decided to use Firebase for that. Firebase has a built in integration with Angular called AngularFire and we didn’t need any of the relationships in our postgres database to make our chat happen. We just needed to connect keyvalue pairs with a collection of messages with timestamps. High read and write availability, and it wasn’t the end of the world if a message didn’t send. 

With the firebase connection established, once it’s there it’ll update your messages when a new one gets sent to the database.

#### What UI, Security, Performance, SEO, Maintainability or Technology considerations do you make while building a web application or site?

#### Talk about your preferred development environment.

#### Which version control systems are you familiar with?

Definitely Git (Rebase vs Merge). I've used Perforce in the past. I've heard of Subversion.

#### Can you describe your workflow when you create a web page?

#### If you have 5 different stylesheets, how would you best integrate them into the site?

#### Can you describe the difference between progressive enhancement and graceful degradation?
* How would you optimize a website's assets/resources?
* How many resources will a browser download from a given domain at a time?
  * What are the exceptions?
* Name 3 ways to decrease page load (perceived or actual load time).
* If you jumped on a project and they used tabs and you used spaces, what would you do?
* Describe how you would create a simple slideshow page.
* If you could master one technology this year, what would it be?
* Explain the importance of standards and standards bodies.
* What is Flash of Unstyled Content? How do you avoid FOUC?
* Explain what ARIA and screenreaders are, and how to make a website accessible.
* Explain some of the pros and cons for CSS animations versus JavaScript animations.
* What does CORS stand for and what issue does it address?
