<p align="center"> <img width="333" height="233" src="https://user-images.githubusercontent.com/104733166/186285439-d9463805-3354-429a-baf4-3e960826028f.gif"><p/>

<br>

# cURL for OSINT (Open-Source Intelligence)
### cURL Tool Usage for OSINT (Open-Source Intelligence)

<br>

![curl-logo](https://user-images.githubusercontent.com/104733166/186279152-3ca718a8-966c-48ac-b1f8-061435f57af6.svg)
<br>
<br>
<br>

# Background Information
Command line tool created in 1998 by [Daniel Stenberg](https://twitter.com/bagder), a Swedish Developper/Programmer.
<br>
Daniel Stenberg's website: https://daniel.haxx.se
<br>
The latest version of the Tool and the code is open source right here on GitHub: https://github.com/curl/curl

<br>

# What exactly does cURL do?
I am certainly no cURL expert and it's quite difficult giving an exact explanation so I will try and give the most basic and simple explanation.
curl means `client URL` and you already know from above that it's a command line tool, it's basically a tool that permits/enables data transfer over many network protocols (HTTPS, HTTP, FTP, it also support SSL Certificates). The tool communicates with a web server with a URL and tells the server the data to be sent or received.(Yes you read that correctly, **the tool can do both**)

<br>

# Difficulty
cURL is fairly easy to use, and if you never opened your Terminal before, now is the time to do so. 

<br>

# Installation
I simply installed cURL with [Homebrew](https://formulae.brew.sh/formula/curl)
<br>
Install Command: 
```$ brew install curl```
<br>

Once you have installed cURL, you can also install Grep: (more info on `grep` later on)
<br>
Install Command: 
```$ brew install grep```

<br>

# Commands
Now that you have everything installed, we are good to go ✅, so let's have a look at some commands for OSINT (Open-Source Intelligence)

<br>
<br>

<img width="233" height="133" src="https://user-images.githubusercontent.com/104733166/186291544-9cd73528-9145-4ddc-ac42-a3d604085ad0.jpg">


# IP Address Information
### Finding your own IP
Commands for finding the IP address of the device you are on: (type each command separate, **each command does the same thing**)

 ```
 curl api.ipify.org
 ```

 ```
 curl ipinfo.io/ip
 ```

 ```
 curl ifconfig.me
 ```

Example below, we can see my IP (ProtonVPN) 😈 :

<img width="333" src="https://user-images.githubusercontent.com/104733166/186289031-2dbec60b-de7a-4740-9452-98c7f8b40164.png">

<br>

### Get more detailed information on your IP:
```
curl ipinfo.io
```
Example below, we can see that there is a lot more information on my IP:

<img width="433" src="https://user-images.githubusercontent.com/104733166/186290638-42617392-581a-4639-9275-607bcab2481f.png">







