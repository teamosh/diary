---
title: "[HTB] Titanic"
layout: post
categories: media
---

~~Initially didnt find any subdomains~~, however it was due to using _subfinder_, so pulled up my g named ffuf and got the real deal.
>![initial enum](/assets/images/titanic/1.png)

It immediately found dev subdomain, which contains gitea, which contains 1) docker-config and 2) flask app file
>![subdomian](/assets/images/titanic/2.png)
>![gitea](/assets/images/titanic/3.png)
>>Bazar zhok, nashel creds.
>>![sql](/assets/images/titanic/4.png)
>> I have a conf file
>>![conf file path](/assets/images/titanic/5.png)
>> I have a path
>>![dev path](/assets/images/titanic/6.png)
>> ugh, path of a conf file.
---
### Found LFI in post request
doesnt need explanation

>![post request](/assets/images/titanic/7.png)
>![burp](/assets/images/titanic/8.png)
>![/etc/passwd](/assets/images/titanic/9.png)
---
> Now use LFI to read conf file:
>>![kek](/assets/images/titanic/10.png)
>>![db](/assets/images/titanic/11.png)
>>crack developer hash, which is pbkdf2$50000$50.
>>
>>It can be done, pretty easily using useful 0xdf command that retrives from db and saves it in correct format. It can be found in my cheatsheet, or his website
![creacked hash](/assets/images/titanic/12.png)

Now connect through ssh and get the user.txt

To be continued: root flag