## Challenge

N = `29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673`

e = 3

ciphertext (c) = `2205316413931134031074603746928247799030155221252519872650073010782049179856976080512716237308882294226369300412719995904064931819531456392957957122459640736424089744772221933500860936331459280832211445548332429338572369823704784625368933`



As seen above, the values of N and ciphertext are very large but the value of e is small. After reading up on RSA encryption, I understood that generally, in order to decode it, I would have to calculate m by the relation- 

$ c = m^e \mod{n} $

which becomes very difficult to compute. 

## Solution

One of the hints suggested to look into what happens if the value of e is too small. In the wiki page provided for RSA encryption, under the padding section, it was mentioned that if the value of e is very small then $ m^e $ is smaller than $ \mod{n} $. Due to that, the ciphertexts can be easily decrypted by directly taking the $ e^{th} $ root of it.

I now needed a way to compute the cube root of a number that large. After being unable to find any tools online that could do it, I had chatgpt draw up a program in python to calculate the cube root for me. 

```
def cube_root(n):
    """
    Calculate the integer cube root of a number n using binary search.

    Args:
        n (int): The number to compute the cube root of.

    Returns:
        int: The integer cube root of n.
    """
    low, high = 0, n
    while low <= high:
        mid = (low + high) // 2
        mid_cubed = mid ** 3
        if mid_cubed == n:
            return mid  # Exact cube root
        elif mid_cubed < n:
            low = mid + 1  # Move the lower bound up
        else:
            high = mid - 1  # Move the upper bound down
    return high  # The floor of the cube root if it's not exact

def main():
    large_num = 2205316413931134031074603746928247799030155221252519872650073010782049179856976080512716237308882294226369300412719995904064931819531456392957957122459640736424089744772221933500860936331459280832211445548332429338572369823704784625368933
        
    # Compute cube root
    root = cube_root(large_num)
    
    print(f"Cube root: {root}")

if __name__ == "__main__":
    main()

```

The cube root of c obtained is: 
m = `13016382529449106065894479374027604750406953699090365388203708028670029596145277`.

The flag can be retrieved from this by first converting m to hex and then converting the hex to text format, finally giving `picoCTF{n33d_a_lArg3r_e_ccaa7776}`.
