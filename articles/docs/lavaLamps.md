# Chaos on the wall: When lava lamps become Internet guards

## Inside Cloudflare’s Lava Lamp Randomness Generator

⋆﹥━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━﹤⋆

###### The flow is like this:
1. h
2. h
3. h

! [lava lamps](C:\Users\divya\OneDrive\Desktop\html\articles\articles\docs\images\Lava_lamp_wall_at_Cloudflare_office_-2.jpg "Wall of 100 lava lamps")

## What is Cloudflare?
 Cloudflare is an American company that ensures and improves the security and performance of websites, applications and network. <br>
 Cloudflare takes the internet traffic that’s meant for your website or app and routes it through its many data centers all over the world. They are then forwaded to your server.
 
 *It's like rather than taking the direct, less travelled by and unsafe road, the audience coming to watch your performance take a safer route.*

 * It filters out malicious accesses and traffic <br>*like a traffic controller*
 * It provides SSL(Secure Sockets Layer) certificates --> identification of which: 
    1. the padlock on the address bar
    2. The URLs beginning with  **https:** instead of **http:**
* Make websites load faster
* and more!

# 

Now about 20% of ALL internet traffic today goes through their servers.
### Why would one the biggest Internet Security companies rely on lava lamps for security keys...?
Are they crazy?<br>
Nah. This brings us to our second section- **Need for randomness in Cyptography**


— — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — —

## Need for randomness in Cyptography
For a secure encryption of 
- HTTPS connections
- TLS handshakes 
- cookies
- passswords 
- VPN connections
- etc.

Randomness is needed to generate secure, unpredictable keys that protect all encrypted communication on the internet. a<br>
*Like a passcode to your mobile phone<br> the more random it is, the harder it is for a someone to guess and unlock your phone* 
<br><br>on the internet it makes sure attackers can't
- decrypt the data
- spy on the traffic
- hijack a session
- impersonate
<br> Since computers are dumb (*writer shrugs*) and follow a pre-prepared set of instructions to give a pre-determined result, they are incapable of giving real, random sequences to encrypt data on such large scale.<br>
Hence they lack "chaos"
<br>Which is when we turn to **nature** and **real-world**.


— — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — —

## But what if I tell you that sometimes some random is just not random enough
hold your horses! before we actually talk about lava lamps, let's dicuss some related and important concepts<br>

*Random != jumbled up numbers (well not entirely)* 

<br>In cryptography, randomness is judged by two things:
- How unpredictable it is, and
- How much real-world “chaos” (entropy) it contains

#### 1. PRNG: Random-Looking, Not Random-Enough
###### Pseudo-Random Number Generator 
Picture this: <br>
You hand someone a range *0-20* of numbers as *seed* and ask them to generate a sequence of 4 digits, with this starting seed, using some formula of their own. <br>
They are generating perfectly looking random numbers everytime with a unique seed- until you  give the same first seed- that is when you get the same first output.<br><br>
so it is predictable...<br>
If someone can predict or steal that seed or that formula(here,), they instantly know all your “random” values — and your security is gone.

#### 2. CSPRNG: Stronger but still vulnerable
###### Cryptographically Secure PRNG
It produces output that is computationally hard to predict even if you know some of the past outputs.
<br> so it needs to be a random, high-quality seed from time to time to make even guessing previous and future seeds becomes impossible.<br>
hence need for an external entropy source.

#### 3.TRNG : When nature takes control
###### True Random Number Generators
Some truly random real-world activites that can be converted to a numeric seed
- Radioactive Decay - (You cannot predict when a radioactive atom will decay - It follows no pattern.)
- Audio Noise (Microphone Static)- the tiny vibrations, electric signals
- Lava Lamps- blobs merge and split unpredictably
- Mouse Movement- Your hand never moves the mouse in a perfectly straight, predictable line. (especially everytime)

— — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — —

## Entering in Cloudflare
![Cloudflare's wall of 100 lava lamps]("C:\Users\divya\OneDrive\Desktop\html\articles\articles\docs\images\close-up.jpg" "Cloudflare's wall of 100 lava lamps")

To produce the unpredictable, chaotic data necessary for strong encryption, choosing a group of lava lamps is a great source for random data.The "lava" in a lava lamp never takes the same shape twice.
<br>Cloudflare has arranged 100 lava lamps on one of the walls in its headquarters with a camera mounted to take their picture and send it to the Cloudflares server.<br>
All digital images are stored as a sequence of numbers. Let's understand the processing pipeline.

## Technical Flow (Brief)
#### Capture an image of the Lava Lamps Wall -->  Pixel Data Extraction --> Whitening (additional processing of image pixels and colours) ---> Hashing / Randomising stream of bytes --> Added to entropy pool --> CSPRNG 

##### Pixel data extraction - 
The image is treated as a pixel data 
let's take an example from my notes 
the resolution of the image is 3 X 3 pixels where each pixel has three values- varying from 0-255 RGB values.<br><br>
I can represent the pixel data of the complete image in the form of a matrix.<br><br>
Now each of the R,G,B can be converted into one byte each -- as in (120, 34, 255) = 78 22 FF  [0x78 0x22 0xFF]<br><br>
Now the image is **flattened**<br>
writing the long list of pixel tuples into one long sequence/stream of bytes.<br>
### *Analogy*
one page --> a number of lines --> each line has number of words --> each word is a group of letter (separated by punctuations and spaces)<br>
If i write all the letters without the breaks, Voila ! I get a stream of letters which earlier when grouped were referring to one pixel data.
<br>

##### Hashing
Raw images have patterns, biases, correlations. So the pixel data is fed into a cryptographic functions which further randomises this sequence so it becomes impossible to *reverse-engineer* the image

##### Entropy pool
Hashing alone can’t produce randomness fast enough, it gives one seed, one time.We are talking millions of random bits for millions of connections every second.<br>
So we go for an entropy pool that collects and stores randomness from other sources as well so it can be used later.<br>
Now CSPNRG can be fed continuously and ensures that attackers cannot guess the seed.
### *Analogy*
Hashing = Taking one cup of water from a river.<br>
Entropy Pool = A big tank collecting water from many rivers.
<br>You fill the tank from: lava lamp camera, thermal noise, mouse movements,etc. <br>

##### CSPRNG
CSPNRG uses algorithms 

