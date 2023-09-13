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

7.Submit the flag located in the developer user's home directory.
I don't why the walktrought on HTB want this exploit, but is use another one to get a reverse shell the EDB-ID is 50239, and with this i got a reverse shell is:
Download this exploit from exploit-db and insert there the domain.

![obraz](https://github.com/Anogota/Horizontall/assets/143951834/04b1dfa2-6d81-4d28-a55e-8b6f1b4cefab)

the we i got a alert "[*] Rember this is a blind RCE don't expect to see output" and we need create the bash reverse shell but before this rember to turn on your netcat
Now you can write this on your blind RCE to get RCE, then go to your netcat and we get a reverse shell.

![obraz](https://github.com/Anogota/Horizontall/assets/143951834/fac33310-336d-42d4-937a-8f4a5467abe9)

Now we can do some recon to find user.txt that was easy, here is the user.txt flag.
![obraz](https://github.com/Anogota/Horizontall/assets/143951834/546a85e5-5ad4-4d51-887d-b32306ebaf98)

And also don't forget use python better shell :P

8.There is a webserver listening only on 127.0.0.1. On what port is it listening?

I don't know the answer for this question but i found something more intresting creds for developer in strapi@horizontall:~/myapi/config/environments/development$ cat database.json
"username": "developer",  "password": "#J!:F9Zt2u"
Now we can log in as developer on SSH i hope

![obraz](https://github.com/Anogota/Horizontall/assets/143951834/4dcd16e8-302b-48e8-b1c8-530638d05433)

I try many things but i have no idea how to do it, maybe another time if collect more kwnoledge :P
