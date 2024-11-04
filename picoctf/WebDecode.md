In this challenge, I was taken to a website where I had to find the flag. I checked out all the pages there were in the website and the "About" page mentioned I should try the inspect tool.

In the code of the "About" page, I found a line that said `<section class="about" notify_true="cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfZGYwZGE3Mjd9">`.

I thought that was the flag so I tried entering `picoCTF{cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfZGYwZGE3Mjd9}` as the flag, which didn't work.

One of the hints provided in the challenge was that the flag may or may not be encoded. That clearly meant that I had to decode it but I didn't know how to so I started googling stuff about decoding to see if there was some simple technique to apply here (since I assumed it wouldn't give something complicated to decode). I didn't have much luck figuring out how to decode this. 

Then I started thinking that there must be some other must be some other way to go about this and maybe I'm fixated on something that isn't even the flag. I went around to the other pages' code. My main goal was to find either something else that looked like an encoded flag or a hint. 

Eventually, I circled back to what I found initially and put it into a decoding tool (since I had no idea how to decode it myself) and voila, I got the flag.
