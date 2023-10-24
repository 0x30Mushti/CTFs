# ILOVEYOU

# Challange intro
```
Points: 
10

Category: 
Reverse Engineering

Cost: 
Free

Scenario:
ILOVEYOU the 3 magical words which have an impact in most of the people's life.
On the other hand, these 3 words don't need any introduction for the people in the Infosec industry.

Let's relive history by analysing the ‘ILOVEYOU’ malware.

This challenge should be completed in a virtual machine as it contains real malware.
```

## Q1, What is the text present as part of email when the victim received this malware?

My thought process here was to check the email body tag, where I could find the code

```
male.Recipients.Add(malead)
          male.Subject = "ILOVEYOU"
          male.Body = vbcrlf & "<FLAG>"
          male.Attachments.Add(dirsystem & "\LOVE-LETTER-FOR-YOU.TXT.vbs")
          male.Send
```