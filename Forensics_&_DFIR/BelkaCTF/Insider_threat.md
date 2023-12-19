# Insider Threat

## The Plot
You have been contacted by a company preparing for their new product launch: an AI-based recommendation system that prioritizes target privacy. However, just before the launch date, the source code and technical documents ended up in the hands of their competitor. The company suspects a recently hired developer and has obtained a copy of his corporate laptop HDD. Your task is to analyze the image and provide evidence to support the suspicion.

## Intro

This Capture The Flag (CTF) challenge is designed for the Belkasoft X software. I utilized Autopsy and Belkasoft X (trial version). This is mostly a GUI-based CTF, I will try to explain my thoughts and reflections.

**SPOILER WARNING:** Since this is a retired CTF, I will be revealing the answers.


## Q1: What is the full name of the laptop owner?
```
Autopsy provides us with OS accounts indexed, and after filtering out the built-in accounts, I find a user called Anit. Checking her Home Directory reveals C:/Users/anit.ghosh.

Answer: Anit Ghosh
```
## Q2: What is the full address of the company's office?
```
By obtaining the domain and website, we could possibly figure this out, as the company's website usually contains a "contact us" or "about us" section. I explore the emails stored under "Users/anit.ghosh/AppData/Roaming/Thunderbird" and find the email address: anit.ghosh@praivacymatrix.com. A search for praivacymatrix.com online leads me to their website and office address.

Answer: Ifangstrasse 6, 8952 Schlieren, Zurich, Switzerland
```
## Q3: On November 16th, the security department received a signal of unauthorized attempts to obtain the company's trade secrets. When did the suspect first show interest in those?
```
While reading the emails, I come across a message from Anit Ghosh:

"Hey John, I've been requested to review a couple of files. Unfortunately, I couldn't find the last file in the list - new technical documentation. Could you help me find this file and send it to me? I would be very grateful!"

This email was sent on: 2020-11-05 20:21:56 CET.

Answer: 2020-11-05 19:21:56 UTC
```
## Q4: What three employees should be asked questions about unauthorized requests from the suspect?
```
By readning all the mails and the content we can se some requests about the "Technical documentation"

Answer: Noelle Johnson, Rachel Corbin, John Finney
```
## Q5: What is the SHA256 hash of the product documentation obtained by the suspect?

```
After looking thru the C: Location I found the path /Users/anit.ghosh/Documents which had alot of technical documents pdf'. 

I had to filter out some by time, name etc. After I only had about 5 documents left I opened them up and found one with the text: "This document and any information in this is strictly confidential".

After that I knew that it was the file asked for and I checked the file metadata and noticed the SHA-256 checksum.

Answer: add33ea905399c5063bcc3437cb5c0436a2fd6deb086bb0ec5bf886f72767242
```

## Q6: What employee has actually provided the suspect with the product documentation?