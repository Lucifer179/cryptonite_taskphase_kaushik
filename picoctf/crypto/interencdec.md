For this challenge, I had to decode the following string: `YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclh6ZzVNR3N5TXpjNWZRPT0nCg==`

First I ran it through base64 decoder and got `b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrXzg5MGsyMzc5fQ=='`.

Then I tried decoding that again in base64 but it was giving me invalid characters as well. I thought it might be a caesar code so I tried decoding it in that but that didn't work either. I also ran it through a cipher identifier but that didn't show any results.

Eventually, I took only the part that was enclosed in the apostrophes - `d3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrXzg5MGsyMzc5fQ==` - because I figured that it meant `base64 (d3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrXzg5MGsyMzc5fQ)`, hinting that it's supposed to be a base64 string. I decoded it in base64 and got `wpjvJAM{jhlzhy_k3jy9wa3k_890k2379}` as the output.

I thought that might be a base64 code as well so I tried that and that didn't work so then I put it through a casesar cipher decoder and that gave me the final flag - `picoCTF{caesar_d3cr9pt3d_890d2379}`.

The time consuming part was figuring out that I should take just the text enclosed in the apostrophes in the initial decoded string. After that I figured out what to do quite quickly.