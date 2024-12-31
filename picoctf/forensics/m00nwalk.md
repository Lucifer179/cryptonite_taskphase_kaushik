"Decode this message from the moon."

"How did pictures from the moon landing get sent back to Earth?"

## SSTV

With that hint, I began looking into the moon landing and how pictures were sent back. After a lot of information that couldn't help me here, I found _SSTV_ - which stands for Slow-scan television. It uses frequency modulation that indicates different levels of brightness to generate images.

Knowing this, I installed qsstv and figured the challenge was straightforward from here. Spoiler alert - _it was not._

# QSSTV

The process of feeding the WAV file given into qsstv was the most mind-numbing thing I've ever done. 

I first configured it to take audio from a file and tried inserting the `message.wav` file directly. The error "invalid header format" showed up so I started digging into the hex of the file. I went through the relevant header bytes and adjusted a few according to how they should be with respect to their file size. This process alone had taken me a while but I figured (once again) that after this, it should accept the file and I would be done. It did not accept the file and showed the same error still. 

So then I changed the input to the sound card and started trying to figure out a way for it to read my system audio directly. After some digging, I found that I could make a VirtualCable sink and have the audio be directed through that into it. For that, I would need to manipulate the audio from `pavucontrol`. This part was the most time-consuming because I wasn't able to get this right. Either the `null output` needed to be seen wouldn't show up or the standard media player I had on my system wouldn't accept an alternate audio output channel. 

So then I tried directly doing it from the terminal with `paplay -d VirtualCable message.wav`, but this didn't work either as it couldn't open the file for some reason. I spent some time working with the file permissions of `message.wav` to ensure everything is in order and couldn't get it to work. So I decided to use another media player that _could_ actually output the audio through a different channel.

To that end, I downloaded VLC which then showed me the option for null output for the audio. That didn't work though for reasons I find out later. I kept adjusting the configuration in qsstv hoping one of those combinations would work with the setup I had so far. By this point everything was quite jumbled so I decided that restarting the system and doing each part step by step should help. I did that, and realized that I hadn't checked that audio is captured from the Null Output in the Recording tab of `pavucontrol`. 

I fixed that and _voila_ - the image began loading in. 

## Flag

`picoCTF{beep_boop_im_in_space}`
