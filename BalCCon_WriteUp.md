# BalCCon '20 CTF Write Up
### Team: 466 Crew
Taylor Bart<br>
Ryan Dunn<br>
Matt Evans<br>
John Tiffany<br>

## crypto/Twice Cooler
Description We are given a message "which resembles some very familiar encoding...".<br>
Methods: When opened in notepad for a cursory glance, I noticed patterns in the columns right away.<br><br>
![](https://github.com/tbart27/BalCCon_CTF/blob/master/crypto1.png)<br><br>
My first attempt, I saw j and jj pop up throughout the message, and I tried to decipher it to binary. The values at first were promising, as they fell within the ASCII range, however the message produced was looking like gibberish so I decided to find another pattern.
Just by the sheer size of the message (34945 characters), I thought maybe the length of the strings between the jj delimiters were actually hex values that would be an encoding of the message. However, this yielded unprintable characters and this method was also abandoned.
When working with John, I realized that the last character was a null delimiter. This meant that the message was 34944 characters long, which meant is was a factor of 16, 32, 64, 128, and 192. We started to think this was a block cypher, or maybe some type of encryption like AES.<br>
John was able to provide some good statistics on the distribution of characters in the message.<br><br>
![](https://github.com/tbart27/BalCCon_CTF/blob/master/crypto2.png)<br><br>

Methods<br>
Picture<br>
Statistics<br>

## web/Navajo
Description<br>
Method<br>

## crypto/Xoared
Description<br>
Method<br>

## web/Let Me See
Description<br>
Methods<br>
Methods<br>
Link<br>
Picture<br>
