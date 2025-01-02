## Challenge

"Download this image file and find the flag."

The given image file was a `.svg` file. 

## Solve

When I opened the image, I zoomed in and thought zooming in as much as possible would reveal the flag. I installed and used `imagemagick` to do that for me. However, the zoom got capped after about 400%. I figured the actual challenge was getting past that cap so I tried to figure out ways to do that. Since the name of the challenge is "Enhance!", I thought maybe I have to enhance the image and that would give me the flag so I tried sharpening it.

Eventually, after this approach wasn't working out, I decided to try the basic forensics techniques of analyzing a file (like exiftool and strings). After checking the `strings`, I got these last few lines which resembled a flag -

```
x="107.43014"
y="132.08501"
style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
id="tspan3748">p </tspan><tspan
sodipodi:role="line"
x="107.43014"
y="132.08942"
style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
id="tspan3754">i </tspan><tspan
sodipodi:role="line"
x="107.43014"
y="132.09383"
style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
id="tspan3756">c </tspan><tspan
sodipodi:role="line"
x="107.43014"
y="132.09824"
style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
id="tspan3758">o </tspan><tspan
sodipodi:role="line"
x="107.43014"
y="132.10265"
style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
id="tspan3760">C </tspan><tspan
sodipodi:role="line"
x="107.43014"
y="132.10706"
style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
id="tspan3762">T </tspan><tspan
sodipodi:role="line"
x="107.43014"
y="132.11147"
style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
id="tspan3764">F { 3 n h 4 n </tspan><tspan
sodipodi:role="line"
x="107.43014"
y="132.11588"
style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
id="tspan3752">c 3 d _ d 0 a 7 5 7 b f }</tspan></text>

```

Putting it together gave me the flag.

## Flag

`picoCTF{3nh4nc3d_d0a757bf}`