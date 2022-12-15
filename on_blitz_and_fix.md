# On Blitz And Fix

Building a software product is difficult. As all programmers know, the gap between "how I think I will write it" and "how I ended up writing it" is large. Most of the time when I begin writing out a new feature I end up reworking the idea multiple times before it is done. The process for adding a new feature usually looks something like this:

1. Think about how to add the feature in my head given the current context
2. Attempt to implement the code the way I thought about it in my head
3. Realize this implementation doesn't work for some reason
4. Discard a lot of the code I just wrote
5. Re-implement the code and test

Sometimes, I may even run into issues where the current implementation of the software doesn't fit the needs of my feature. This usually requires a refactor / re-write of some of the application.

There is an unspoken aspect to the process I previously described. More often than not, I don't truly understand what I want the code to look like, until I've attempted to implement it. This is especially true, the newer the codebase is. When I try to preemptively account for all future scenarios in a codebase, I end up optimizing features that will be reworked or deleted entirely.

I call this process "blitz and fix". Many talented programmers apply this process. They write some code, iterate on it, and submit it for review by other programmers. They iterate on the pull request multiple times before merging it. Then they move on to the next task and begin the cycle over again. I have become much better at iterating on my implementations before submitting them for review. Rather than attempting to implement something once and submitting it, I rework it a few times first. The sweet spot for the number of iterations is between 2 and 3, after that, I find that I'm spending too much time over optimizing.

In the past, I have used this process on a micro scale to solve individual problems. However, this process can also be applied to developing an entire product. I always feel tempted to try to denote every feature a software system needs before I build it. Implementation is difficult. Certain designs always feel perfect on paper, but requirements end up changing. Rather than solving problems that may not even exist, it is better to start creating solution. More often than not, a requirement will reveal itself to be misinformed. This is even more true for products whose necessity is unknown. For example, a new startup's product that does not yet have product market fit. Once an initial implementation is complete, it is easier to determine which features are truly required. It is an order of magnitude easier to reimplement a feature that has already been written. Due to this, it is important to go back to the code and fix any implementations that may have been poorly written the first time around. This allows the starting point for the next "blitz" to remain clean and easy to extend.
