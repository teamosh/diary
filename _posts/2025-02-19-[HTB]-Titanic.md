---
title: "[Personal] New Twink Account"
layout: post
categories: media
---

~~Initially didnt find any subdomains~~, however it was due to using _subfinder_, so pulled up my g named ffuf and got the real deal.
>![initial enum](titanic_1.png)

It immediately found dev subdomain, which contains gitea, which contains 1) docker-config and 2) flask app file
>![subdomian](image-4.png)
>![gitea](image-5.png)
>>Bazar zhok, nashel creds.
>>![sql](image-6.png)
>> I have a conf file
>>![conf file path](image-7.png)
>> I have a path
>>![dev path](image-8.png)
>> ugh, path of a conf file.
---
### Found LFI in post request
doesnt need explanation

>![post request](image-1.png)
>![burp](image-2.png)
>![/etc/passwd](image-3.png)
---
> Now use LFI to read conf file:
>>![kek](image-9.png)
>>![db](image-10.png)
>>crack developer hash, which is pbkdf2$50000$50.
>>
>>It can be done, pretty easily using useful 0xdf command that retrives from db and saves it in correct format. It can be found in my cheatsheet, or his website
![creacked hash](image-11.png)

Now connect through ssh and get the user.txt

To be continued: root flag