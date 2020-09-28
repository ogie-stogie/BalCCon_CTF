# BalCCon '20 CTF Write Up
### Team: 466 Crew
Taylor Bart<br>
Ryan Dunn<br>
Matt Evans<br>
John Tiffany<br><br>
[Write Up Link](https://github.com/tbart27/BalCCon_CTF/blob/master/BalCCon_WriteUp.md)

## crypto/Twice Cooler
Description: We are given a message "which resembles some very familiar encoding...".<br>
Methods: When opened in notepad for a cursory glance, I noticed patterns in the columns right away.<br><br>
![](https://github.com/tbart27/BalCCon_CTF/blob/master/crypto1.png)<br><br>
My first attempt, I saw j and jj pop up throughout the message, and I tried to decipher it to binary. The values at first were promising, as they fell within the ASCII range, however the message produced was looking like gibberish so I decided to find another pattern.
Just by the sheer size of the message (34945 characters), I thought maybe the length of the strings between the jj delimiters were actually hex values that would be an encoding of the message. However, this yielded unprintable characters and this method was also abandoned.
When working with John, I realized that the last character was a null delimiter. This meant that the message was 34944 characters long, which meant is was a factor of 16, 32, 64, 128, and 192. We started to think this was a block cypher, or maybe some type of encryption like AES.<br>
John was able to provide some good statistics on the distribution of characters in the message.<br><br>
![](https://github.com/tbart27/BalCCon_CTF/blob/master/crypto2.png)<br><br>
Unfortunately, we couldn't get distributions on two letter combinations. Another problem was that this didn't explain the common jjj pattern in the message.

## web/Navajo
Description: We are given a link to https://navajo.pwn.institute/ where we are greeted with the following page:<br><br>
![](https://github.com/tbart27/BalCCon_CTF/blob/master/web1.png)<br><br>
Methods: First I checked the html for any clues/vulnerabilities but the html contained nothing useful. So now I tried seeing if I could access an server files from the browser. From the common server files I tested, I was able to get non-404 on robot.txt.<br><br>
![](https://github.com/tbart27/BalCCon_CTF/blob/master/web2.png)<br><br>
It seems that crawlers were disabled from entering server-status and what made this more intriguing was that the challenge hint said "What is the status of Navajo tribes nowadays?". After some research, I still couldn't figure out a valid attack on the server-status file so I proceeded to look over other challenges.

## crypto/Xoared
Description: The hint for the challenge was "the message was "xoared" or something like that".<br>
Method: The hint definitely refers to XOR encryption as a component but simple XOR decoders online produced nothing of value and I was having trouble figuring out the key. After the finish of the CTF, I read this [write up](https://ctftime.org/writeup/23823). xortool looks super useful and I wish I had used that software instead for this challenge. Hopefully, future challenges will try an XOR encryption.<br>

## web/Let Me See
Description: The bulk of my time for this CTF was spent on Twice Cooler and Let Me See. This challenge provided a page where you could read the source code of a website.<br>
Immediately, this looked like a textbook SSRF vulnerability.  Simply entering http://localhost yielded:<br><br>
![](https://github.com/tbart27/BalCCon_CTF/blob/master/web3.png)<br><br>
This confirms that we are able to send commands to the server and we are given where the flag is located! Immediately I tried http://localhost/flag.txt but this obviously was too easy since I was greeted with:<br><br>
![](https://github.com/tbart27/BalCCon_CTF/blob/master/web4.png)<br><br>
A quick audit of the site with https://pentest-tools.com/website-vulnerability-scanning/website-scanner# gave me some more useful information that the server was using nginx 1.19.2 and was missing some HTTP security headers.<br><br>
![](https://github.com/tbart27/BalCCon_CTF/blob/master/web5.PNG)<br><br>
This helped to identify what type of injections and file paths to use in my attacks.
