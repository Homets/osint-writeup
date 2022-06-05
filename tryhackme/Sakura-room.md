## Sakura room
### Introduction
*This room is designed to test a wide variety of different OSINT techniques. With a bit of research, most beginner OSINT practitioners should be able to complete these challenges. This room will take you through a sample OSINT investigation in which you will be asked to identify a number of identifiers and other pieces of information in order to help catch a cybercriminal. Each section will include some pretext to help guide you in the right direction, as well as one or more questions that need to be answered in order to continue on with the investigation. Although all of the flags are staged, this room was created using working knowledge from having led and assisted in OSINT investigations both in the public and private sector.*

#### Tip-Off
*The OSINT Dojo recently found themselves the victim of a cyber attack. It seems that there is no major damage, and there does not appear to be any other significant indicators of compromise on any of our systems. However during forensic analysis our admins found an image left behind by the cybercriminals. Perhaps it contains some clues that could allow us to determine who the attackers were? *

Here the image the attacker send us.

![sakurapwnedletter](https://user-images.githubusercontent.com/82462804/172058604-2a84dfea-0be5-411e-ae2d-2aeabc232ea8.svg)



***Question : 

**What username does the attacker go by?**

  
Let's see if information is present in the metadata :

```
ExifTool Version Number         : 12.41
File Name                       : sakurapwnedletter.svg
Directory                       : .
File Size                       : 830 KiB
Zone Identifier                 : Exists
File Modification Date/Time     : 2022:06:05 14:59:30+02:00
File Access Date/Time           : 2022:06:05 15:22:56+02:00
File Creation Date/Time         : 2022:06:05 15:22:56+02:00
File Permissions                : -rw-rw-rw-
File Type                       : SVG
File Type Extension             : svg
MIME Type                       : image/svg+xml
Xmlns                           : http://www.w3.org/2000/svg
Image Width                     : 116.29175mm
Image Height                    : 174.61578mm
View Box                        : 0 0 116.29175 174.61578
SVG Version                     : 1.1
ID                              : svg8
Version                         : 0.92.5 (2060ec1f9f, 2020-04-08)
Docname                         : pwnedletter.svg
Export-filename                 : /home/SakuraSnowAngelAiko/Desktop/pwnedletter.png
Export-xdpi                     : 96
Export-ydpi                     : 96
Metadata ID                     : metadata5
Work Format                     : image/svg+xml
Work Type                       : http://purl.org/dc/dcmitype/StillImage
Work Title                      :
```

We can see with the Export-filename chunk some useful information like the possible pseudonym of the attacker. **SakuraSnowAngelAiko**.


#### Reconnaissance
*It appears that our attacker made a fatal mistake in their operational security. They seem to have reused their username across other social media platforms as well. This should make it far easier for us to gather additional information on them by locating their other social media accounts.*

***Question:***

**What is the full email address used by the attacker?**

  
Do a simple google search to try to find something  : 

![googlesearch](https://user-images.githubusercontent.com/82462804/172058635-534d4d55-a84f-447a-91c3-fa657ac5644c.png)

These are some interesting things, let's find something in the first link, the github :

On pinned repository we can find a PGP repo. 

And now we have the PGP public key block of the attacker, let's decrypt with it with gpg tools in linux ```gpg --import pgp.txt``` .

And now pgp send us the response  SakuraSnowAngel83@protonmail.com.


**What is the attacker's full real name?**

Let's go on twitter now, the last tweet is  

> Silly me, I forgot to introduce myself! Hi there! I'm
[@AikoAbe3](https://twitter.com/AikoAbe3)
!

And on google we can find a linkedin of the same name so we can agree that it is probably his name.

#### Unveil
*It seems the cybercriminal is aware that we are on to them. As we were investigating into their Github account we observed indicators that the account owner had already begun editing and deleting information in order to throw us off their trail. It is likely that they were removing this information because it contained some sort of data that would add to our investigation. Perhaps there is a way to retrieve the original information that they provided?*


***Question***

**What cryptocurrency does the attacker own a cryptocurrency wallet for?**

While reading background of Unveil task, it tells us that the answer is probably in the old commits of a repository.

Oh ! a ETH repository, no useful information let's go deeper with the commit of this repo, on the older repository we find :```0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef.Aiko:pswd@eu1.ethermine.org:4444```.

let's search the crypto adress and we can see she own Ethereum (obviously with the repo name).

**What is the attacker's cryptocurrency wallet address?**

The answer is on the last questions x)

**What mining pool did the attacker receive payments from on January 23, 2021 UTC?**

Let's find a ethereum block explorer like etherscan, go on the attacker adress, and a lot of transction are listed, let's filter it with 23/01/2021 and we can see she receive a Ethermine payments.

**What other cryptocurrency did the attacker exchange with using their cryptocurrency wallet?**

Now that we have all her transactions, We find not only ether but some Tether transfer.

#### Taunt

*Just as we thought, the cybercriminal is fully aware that we are gathering information about them after their attack. They were even so brazen as to message the OSINT Dojo on Twitter and taunt us for our efforts. The Twitter account which they used appears to use a different username than what we were previously tracking, maybe there is some additional information we can locate to get an idea of where they are heading to next?*

*We've taken a screenshot of the message sent to us by the attacker, you can view it in your browser* [here](https://raw.githubusercontent.com/OsintDojo/public/main/taunt.png).

**What is the attacker's current Twitter handle?**

On google, a twitter account is find and the picture sending by the background of his task confirm this account.

and the first tweet of this account is https://twitter.com/SakuraLoverAiko/status/1353157336538386432 with a hint on reply she said : 

>Not too concerned about someone else finding them on the Dark Web. Anyone who wants them will have to do a real DEEP search to find where I PASTEd them.

But unfortunately the website was down when im doing this challenge so let's use the hint.

*The Dark Web site for this answer may go up and down for hours at a time. If the website has been down for multiple days, or if you do not feel comfortable searching the Dark Web, you can view this screenshot to help complete the tasks in this section: https://raw.githubusercontent.com/OsintDojo/public/main/deeppaste.png*

the image above is ![deeppaste](https://user-images.githubusercontent.com/82462804/172058657-1f1b601f-194a-4800-88ff-7f2a939231e5.png)


The challenge is easier with this screenshot, we just need to paste the md5 on the md5 query of the url.

**What is the BSSID for the attacker's Home WiFi?**

on the darkweb screen we see a Network name and password of a mysterious Home WiFi.

Let's use the useful [wigle.net](https://wigle.net/) let's do some advanced search, copy the network name, and now we can see a result with a BSSID of the attacker's home WiFi.

#### Homebound

*Based on their tweets, it appears our cybercriminal is indeed heading home as they claimed. Their Twitter account seems to have plenty of photos which should allow us to piece together their route back home. If we follow the trail of breadcrumbs they left behind, we should be able to track their movements from one location to the next back all the way to their final destination. Once we can identify their final stops, we can identify which law enforcement organization we should forward our findings to.*

***Question***

**What airport is closest to the location the attacker shared a photo from prior to getting on their flight?**

Here is the tweet picture and text we need to analyse.

>Checking out some last minute cherry blossoms before heading home!
![search](https://user-images.githubusercontent.com/82462804/172058663-41a7a732-82e7-4695-b8b2-fe7a6ce92a49.jpg)


This picture have a Weakness, on the background we can see an obelisk, this picture don't need reverse image, just google "cherry flower obelisk" and we have the place, the Washington Monument, check the airport the closest with "Washington Monument airport" search, and now we know this is Ronald Reagan Washington National Airport (DCA).

**What airport did the attacker have their last layover in?**

>My final layover, time to relax!
![layover](https://user-images.githubusercontent.com/82462804/172058693-86346a74-9360-415a-a011-2bdef8e1b64f.png)


We see that the place is rated 5 stars on skytrax, the japan airline badge, and that we are in a sakura lounge. let's google this "5 star airline skytrax sakura lounge JAL", go to the images and see this, probably in the same place but from another angle.![[lounge.webp]]

go on the website and the information of the airport are writed.
>Route: Tokyo-Haneda Airport (HND) to John F. Kennedy International-New York (JFK)

**What lake can be seen in the map shared by the attacker as they were on their final flight home?**

>Sooo close to home! Can't wait to finally be back! :)

![earth](https://user-images.githubusercontent.com/82462804/172058703-19584928-576a-4d6a-8963-23648e345747.jpg)
The first tool that come to mind is simply google earth, We see a huge body of water, this is possibly our lake, let's retry to have this view and zoom, Now we have the name of this lake, the *Lake Inawashiro*.

**What city does the attacker likely consider "home"?**

Now the answer will be vicious, remember the darkweb screenshot with Home Wifi, have you looked at all the names ? 

> City Free wifi HIROSAKI_Free_Wi-Fi H_Free934!




### FINISH


