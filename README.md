# ThingsIDidNotKnowAboutJava
Here noted all the things that I did not know or can query when I need while developing Java apps.

Most the information collected from StackOverFlow


1. How to handle Future.get checked exceptions

ExecutionException and InterruptedException are two very different things.

ExecutionException wraps whatever exception the thread being executed threw, so if your thread was for instance doing some kind of IO that caused an IOException to get thrown, that would get wrapped in an ExecutionException and rethrown.

An InterruptedException is not a sign of anything having gone wrong. It is there to give you a way to let your threads know when it's time to stop so that they can finish up their current work and exit gracefully. Say I want my application to stop running, but I don't want my threads to drop what they're doing in the middle of something (which is what would happen if I made them daemon threads). So when the application is being shutdown, my code calls the interrupt method on these threads, which sets the interrupt flag on them, and the next time those threads are waiting or sleeping they check the interrupt flag and throw an InterruptedException, which I can use to bail out of whatever infinite-loop processing/sleeping logic the threads are engaged in. (And if the thread doesn't wait or sleep, it can just check the interrupt flag periodically.) So it is an instance of an exception being used to change logic flow. The only reason you would log it at all is in an example program to show you what's happening, or if you're debugging a problem where interrupt logic is not working correctly.
