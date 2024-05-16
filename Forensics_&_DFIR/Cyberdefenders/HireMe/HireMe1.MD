# HireMe

##The Plot

Karen is a security professional looking for a new job. A company called "TAAUSAI" offered her a position and asked her to complete a couple of tasks to prove her technical competency. As a SOC analyst, analyze the provided disk image and answer the questions based on your understanding of the cases she was assigned to investigate.

**SPOILER WARNING:** Since this is a retired CTF, I will be revealing the answers.

##Q1: What is the administrator's username?

When loading the AD1 file into FTK Imager, I spotted one user under C:\Users, which means that if there is only one user on the machine, it is likely the administrator. I double-checked this by looking in the SAM file.
````
Answer: Karen
````

##Q2: What is the OS's build number?

The answer hides in the Software registry file under: SOFTWARE\Microsoft\Windows NT\CurrentVersion. Keep in mind that information about Windows resides in the Software file because Windows OS is considered software, or at least the registry thinks so. I am using Registry Explorer for registry forensics, a great tool written by Eric Zimmerman.
````
Answer: 16299
````
##Q3: What is the hostname of the computer?

This is pretty straightforward. Open Registry Explorer, load the system file, check the "available plugins" tab, and go to the "computer name" subkey to find the answer.
````
Answer: TOTALLYNOTAHACK
````
##Q4: A messaging application was used to communicate with a fellow Alpaca enthusiast. What is the name of the software?

Again, pretty straightforward. Load the Software registry file, check the "available bookmarks" tab. I look at the sub-key called "Uninstall" to see which software has an uninstall .exe, which means it has been installed.
````
Answer: Skype
````
##Q5: What is the zip code of the administrator's post?

Going back to the AD1 file in FTK, postcodes can often be found in the browser history. For example, when the user uses the "autofill function", this artifact can be found in the file "C:\Users\USERNAME\AppData\Local\Google\Chrome\User data\Default\Web Data". This can be opened with SQL.
````
Answer: 19709
````
##Q6: What are the initials of the person who contacted the admin user from TAAUSAI?

After looking around in the AD1 file, I noticed there were some OUTLOOK files that could be interesting for this question. I use the OST viewer to input the "suspects" Outlook folder and then view it in OST viewer with all the inbox, deleted mails and so on.

The initials were found within an email in the inbox.
````
Answer: MS
````
##Q7: How much money was TAAUSAI willing to pay upfront?

By reading the mail thread we can see the number that TAAUSAI was willing to pay.
````
Answer: $150,000
````
##Q8: What country is the admin user meeting the hacker group in?

By reading the mail thread we can see this line "What we need you to do is gain his trust and then hack his machine. We will give you more information about this in person. Meet us here "27°22’50.10″N, 33°37’54.62″E"" I pasted in the coordinates in Google Earth to get the country.
````
Answer: Egypt
````
##Q9: What is the machine's timezone? (Use the three-letter abbreviation)

Registry Explorer --> System file --> available bookmarks --> TimeZoneInformation
````
Answer: UTC
````
##Q10: When was AlpacaCare.docx last accessed?

File access date and time can be found within the $MFT file. Extract it, load it into the tool MFTcmd or MFTexplorer(also written by Eric Zimmerman). There should be a tab called "SI_Last_Accessed". Convert the time to PM.
````
Answer: 03/17/2019 09:52 PM
````
##Q11: There was a second partition on the drive. What is the letter assigned to it?

Registry Explorer --> System file --> available bookmarks --> Mounted Devices.
````
Answer: A
````
##Q12: When was AlpacaCare.docx last accessed?

In the OST viewer, we can find emails between Karen and Michael. Michael wants Karen to solve a question. It seems to be base64 encoded. I take the base64 string and decode it on CyberChef to get the answer.
````
Answer: TheCardCriesNoMore
````
##Q13 What is the job position offered to Karen? (3 words, 2 spaces in between)

This could be read in one of the emails in Karen's Outlook appdata. Use OST viewer to read their mail threads.
````
Answer: Cyber security analyst
````
##Q14: When was the admin user password last changed?

Registry Explorer --> SAM file --> available bookmarks --> Users. The date and time could be found under the "Last Password Change" section.
````
Answer: 03/17/2019 09:52 PM
````
##Q15: What version of Chrome is installed on the machine?

Registry Explorer --> Software file --> available bookmarks --> Uninstall. "Display Version"
````
Answer: 73.0.3626.121
````
##Q16: What is the HostUrl of Skype?

Check the ADS for the Skype-8.41.0.54.exe file. Host URL is included in the ADS. ADS = Alternate Data Stream.
````
Answer: hxxps://download.skype.com/s4l/download/win/Skype-8.41.0.54.exe
````
##Q17: What is the HostUrl of Skype?

PacaLady:\AlpacaCare.docx file --> HyperLinks from the DOCX file
````
Answer: palominoalpacafarm.com
````