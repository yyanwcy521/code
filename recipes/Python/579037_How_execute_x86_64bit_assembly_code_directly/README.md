###How to execute x86 64-bit assembly code directly from Python on Linux (requires Nasm)

Originally published: 2015-03-24 17:35:49
Last updated: 2015-03-24 18:23:19
Author: Simon Harrison

This particular example pertains to running 64-bit assembly code under 64-bit Python, however if you are fortunate enough to be running on a 32-bit Linux platform you may get away with doing a lot less.  Since the introduction of DEP you can no longer just shove some code in a buffer and execute it.  You must first allow execute permission.  Further, you cannot change memory protection settings for anything other than an entire page, so I've padded the memory allocated to include a page before and a page after, so I can seek back to the start of page for the start of my assembler, then change memory protection from there secure in the knowledge that I won't change protection for anything beyond the end of my allocated region.  I could probably have used valloc() instead.