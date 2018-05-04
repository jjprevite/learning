# Work Logs
Keep track of what I learn at work related to coding.


### Fri, May 4th, 2018
I am working on fixing an issue with API requests that are timing out before events are finished on the back end. I'm trying to fix this with async/await. I think the issue is that when the fetch call enters the .then, it goes back to where it was in the code and says "I'm done!" Even though it is not done. 

So I need to figure out how to use retry logic inside .then of fetch call.
