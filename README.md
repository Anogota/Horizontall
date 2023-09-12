1.How many TCP ports are open on this target?
First we need what's going on the server, what kind of port are open, and ofc what we can exploit :)

![obraz](https://github.com/Anogota/Horizontall/assets/143951834/d1e38600-c18b-4fb1-aa05-fd37479be271)

We can see there nothing intresting, only 22 SSH and 80 HTTP

2.Using the Developer Tools in a browser we can see 'app.c68eb462.js' being loaded in the Network tab. What is the additional subdomain that is exposed in this file.
First we need add into the /etc/hosts domain for this lab http://horizontall.htb/ there many line of code and i can't use pretty priting, but we need do some research in this code, anf find what we need, without ctrl+f i will search this subdomain years, but i got this: api-prod.horizontall.htb

![obraz](https://github.com/Anogota/Horizontall/assets/143951834/9037ec80-7ef5-4f85-91d2-be61a8df48c4)

3.What is the path on the webserver that will render a login page on api-prod.horizontall.htb?
Use your ffuf to find the subdomain:ffuf -w /usr/share/wordlists/dirb/common.txt -u http://api-prod.horizontall.htb/FUZZ
and i found something intresting subdomain, but i don't understand why are repeated but here is the results:
And the answer for this question is /admin 

![obraz](https://github.com/Anogota/Horizontall/assets/143951834/b324deb9-960d-4b41-acc3-09f588ffa0ef)

4.We need to fingerprint this target in order to identify any potential vulnerabilities. What is the version of Strapi API being used on this target?
I don't know how to do it, but i will figure it out with small help google. Okay i give you trying to find it, but when i try use searchsploit i got only 5, and i know there version of strapi is: 3.0.0-beta.17.4

5.What is the 2019 CVE id for a vulnerability in Strapi that allows an attacker to change the password of a user without knowing the current password?
6.What is the 2019 CVE id for a vulnerability that will provide remote code execution to an unauthenticated user?

The answer for this question we can realy quick find on exploit-db, this is a the best resource i find with all most popular exploit, first is CVE is: CVE-2019-18818 and the secend on is: CVE-2019-19609



