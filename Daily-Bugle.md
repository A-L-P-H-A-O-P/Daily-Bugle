# Daily-Bugle --tryhackme

(https://tryhackme.com)

(https://tryhackme.com/room/dailybugle)

This room is about to gain knowledge of Compromise a Joomla CMS account via SQLi, practise cracking hashes and escalate your privileges by taking advantage of yum.

The first step I took is using nmap to get about the port which are open in machine to enumerate futher.
<img width="951" alt="Screenshot_2022-01-13_03_46_37" src="https://user-images.githubusercontent.com/96518581/149460729-c34231a0-0dc8-46db-b05e-bce9cc8a0bf0.png">

for directories brute-forcing there is one of the best tool is ffuf.
<img width="740" alt="2" src="https://user-images.githubusercontent.com/96518581/149462970-1b1e9152-5de6-47a4-bb29-817de88adc7c.png">
<img width="699" alt="3" src="https://user-images.githubusercontent.com/96518581/149463024-20d39fac-86a8-4763-9042-6bec5c027afa.png">

By the help of nmap result above we get to know about joomla so let's find out version of it.
<img width="698" alt="1" src="https://user-images.githubusercontent.com/96518581/149464410-fa13e39b-8a02-4b5f-8598-ecf72684b433.png">

Using nmap we get to know about port 80 is running http service then by browsing we get this page :-
<img width="830" alt="4" src="https://user-images.githubusercontent.com/96518581/149466138-e1d33577-94d4-48bb-a03f-d3482de88e9e.png">

Going to /administrator page we get login panel of joomla cms
<img width="827" alt="5" src="https://user-images.githubusercontent.com/96518581/149468169-c5017824-d2e1-4952-8a0c-e348ea4b1115.png">

Searching for joomla exploit in github I get with amazing script called joomblah.py which gives us the username and hash password, link of github script https://github.com/terandev/Joomblah

<img width="623" alt="6" src="https://user-images.githubusercontent.com/96518581/149469687-6c690495-2f0a-4116-84a1-86fb762dc94f.png">
<img width="261" alt="7" src="https://user-images.githubusercontent.com/96518581/149469852-f9e04502-0ed8-408c-b215-0ee6be2618a4.png">
<img width="960" alt="8" src="https://user-images.githubusercontent.com/96518581/149470235-f6af6c75-7489-491b-83bf-65da48aa922d.png">

another method to get credentials is
<img width="960" alt="9" src="https://user-images.githubusercontent.com/96518581/149470902-3279883a-43ed-49d3-ace5-e0825b306237.png">

Now its time to crack the hash, for this we use one of the best tool JohnTheRipper and paste the hash into the file hash.txt
<img width="909" alt="10" src="https://user-images.githubusercontent.com/96518581/149471814-e113f67a-277b-4430-99b6-7fd18ebe4f13.png">

We get the {username:password} let's get back to /administrator page and try to login into joomla login page, try to find any upload page I found the Joomla reverse shell article https://www.hackingarticles.in/joomla-reverse-shell/ this will explains how to gain reverse shell
<img width="960" alt="11" src="https://user-images.githubusercontent.com/96518581/149475373-3856b02d-424b-44b9-9b70-69ad02fb6971.png">
<img width="960" alt="12" src="https://user-images.githubusercontent.com/96518581/149475421-9793e645-b453-4acc-8646-9545be6aba80.png">
<img width="960" alt="13" src="https://user-images.githubusercontent.com/96518581/149475498-e0934dfc-3a74-43de-9492-f1a2c82ca67c.png">
<img width="959" alt="14" src="https://user-images.githubusercontent.com/96518581/149475573-c9dd0180-78a8-45c3-b8b6-261f7dc279a5.png">

We copy paste the reverse php shell from this github link https://github.com/pentestmonkey/php-reverse-shell and change the ip_address to attacker_ip_address and saving it, by browsing the shell and start netcat tool listening mode we get the machine shell
<img width="960" alt="16" src="https://user-images.githubusercontent.com/96518581/149478501-93b76bbd-59a8-4948-aacd-50422c65f26a.png">
<img width="819" alt="15" src="https://user-images.githubusercontent.com/96518581/149478816-d356b05b-b2ca-4bde-be64-2b438370546e.png">
<img width="839" alt="17" src="https://user-images.githubusercontent.com/96518581/149480108-69190631-a015-4849-971d-81405318a2be.png">

We get to the passwaord of user jjameson in configuration.php in /var/www/html directory then we use su(substitute user) and user.txt in the home directory of the user.
<img width="966" alt="18" src="https://user-images.githubusercontent.com/96518581/149486258-79476609-9182-4ba9-95c5-c07c9c594559.png">
<img width="736" alt="19" src="https://user-images.githubusercontent.com/96518581/149486346-dbd474dd-d9c6-4808-a48e-5ed10842e8e6.png">

By running sudo -l we get to know that we can run yum then we use GTFObins(https://gtfobins.github.io/gtfobins/yum/) to escalate our privledged.
<img width="960" alt="20" src="https://user-images.githubusercontent.com/96518581/149508107-e0cf92f1-48d9-49a0-b522-bbac1f67557e.png">
<img width="966" alt="21" src="https://user-images.githubusercontent.com/96518581/149508140-5d73688a-621b-4e42-9771-de1103044a53.png">

HIT THE BULLSEYE!!!
