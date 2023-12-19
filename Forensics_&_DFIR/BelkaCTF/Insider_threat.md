# Insider Threat


## The plot:
You were contacted by a company preparing their new product launch: an AI-based recommendation system that respects target privacy. 
Just before the date, the source code and technical documents ended up in their competitor's hands. 
The company suspects a recently hired developer and obtained a copy of his corporate laptop HDD. You are going to analyze the image and support the suspicion with evidence extracted from the laptop...

## Intro

This CTF is built for the belkasoft x software. I used autopsy which is an open source forensic software which I have been using for a while.

*SPOILER WARNING* As this is a retierd CTF I will be showing the answers *SPOILER WARNING*

## Q1, What is the full name of the laptop owner?
```
Autopsy gives os the OS accounts indexed, I filter away the builtin accounts. 

I can see a user called Anit. When I check her Home Directory I see C:/Users/anit.ghosh

Answer: anit ghosh
```

## Q2, What is the full address of company's office?
```
By getting the domain and website we could (possible) figure this out as it should have a "contact us"/"about us" section on their website.

I started to read the mails which are stored under "Users/anit.ghosh/AppData/Roaming/Thunderbird" 

I found the mail address: anit.ghosh@praivacymatrix.com and by looking for praivacymatrix.com online I found their website and also their address.

Answer: Ifangstrasse 6, 8952 Schlieren, Zurich, Switzerland
```
## Q3, On November 16th security department got a signal of unauthorized attempts to obtain company's trade secrets. When did the suspect first show interest in those?


