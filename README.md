<p align="center"> <img width="433" height="233" src="https://user-images.githubusercontent.com/104733166/186285439-d9463805-3354-429a-baf4-3e960826028f.gif"><p/>

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
curl means `client URL` and you already know from above that it's a command line tool, it's basically a tool that permits/enables data transfer over many network protocols (HTTPS, HTTP, FTP, it also supports SSL Certificates). The tool communicates with a web server with a URL and tells the server the data to be sent or received.(Yes you read that correctly, **the tool can do both**)

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
<br>
<br>



# IP Address Information

<img width="233" height="133" src="https://user-images.githubusercontent.com/104733166/186291544-9cd73528-9145-4ddc-ac42-a3d604085ad0.jpg">

### Finding your own IP
Commands for finding the IP address of the device you are on: (type each command separately, **each command does the same thing**)

 ```
 $ curl api.ipify.org
 ```

 ```
 $ curl ipinfo.io/ip
 ```

 ```
 $ curl ifconfig.me
 ```
<br>
Commands to get your IPV4 and IPV6 addresses:

 ```
 $ curl -4 icanhazip.com
 ```

 ```
 $ curl -4 icanhazip.com
 ```
 
 <br>




Example below, we can see my IP (ProtonVPN) 😈 :

<img width="333" src="https://user-images.githubusercontent.com/104733166/186289031-2dbec60b-de7a-4740-9452-98c7f8b40164.png">

<br>

### CGet more detailed information on your IP:
```
$ curl ipinfo.io
```
Example below, we can see that there is a lot more information on my IP such as city, country, organization, timezone, GPS coordinates:

<img width="433" src="https://user-images.githubusercontent.com/104733166/186290638-42617392-581a-4639-9275-607bcab2481f.png">

It works also with this command (.json format)

```
$ curl ipinfo.io/json
```
There is another command to make sure we really get JSON and not the homepage html


```
$ curl -H "Accept: application/json" ipinfo.io
```

`-H takes a single parameter of an extra header to include in the request and Accept adds the Accept request headers to the request`

<br>
<br>

Let's do more tests using Google's IP address.<br>

Below are the commands when you know the IP address you are searching for, you want to know jut the city.

```
$ curl ipinfo.io/8.8.8.8/city
```
<br>
Results:
<img width="366" src="https://user-images.githubusercontent.com/104733166/186506023-a37ef2d1-fae7-47e7-a732-bc5b999ef898.png">
<br>

Get the country:
```
$ curl ipinfo.io/8.8.8.8/country
```
<br>

Get the Organization:
```
$ curl ipinfo.io/8.8.8.8/org
```

<br>
<br>
<br>


# Whois Commands

<img width="133" src="https://user-images.githubusercontent.com/104733166/186533300-4d97e784-00e1-4b0b-8f84-2f40abf6cb9f.png">

I particularly like this easy command to get Whois information, this is the work of [Sector035](https://sector035.nl) and was shared on an article called [dial cURL for Content on OSINTCuriou.us](https://osintcurio.us/2019/06/25/dial-curl-for-content/)

```
$ curl cli.fyi/inputdomainhere
```
<br>

Let's test with the website of the French Presidential Palace:
<br>
```
$ curl cli.fyi/elysee.fr
```
Perfect results:

<img width="633" src="https://user-images.githubusercontent.com/104733166/186533013-2716e467-0e82-4fb9-87bc-003cd0a355d1.png">

<br>
I will add a personal touch to the command, with some color, it isn't a big difference with these results, but wait until you see how it works further below with messy results and how the jq command can really make a difference.


<br>

```
$ curl cli.fyi/elysee.fr | jq --color-output
```

<br>

<img width="333" alt="Screen Shot 2022-08-25 at 00 20 53" src="https://user-images.githubusercontent.com/104733166/186533988-ea8abfd2-9546-4138-b016-8f75761cfba8.png">

<br>

<br>

<br>


# Getting an email from a Domain with cURL + Grep

<img width="333" src="https://user-images.githubusercontent.com/104733166/186535617-dba770e5-72c2-4e7b-9854-2b49a821cb9f.jpg">

Grep Website: https://www.gnu.org/software/grep/manual/grep.html

### What is Grep?
grep prints lines that contain a match for one or more patterns | Regex (Regular Expressions)
Why is it called grep: g/re/p: **globally search for a regular expression and print matching lines**

<br>

This is not my work, a fantastic email scraper with a cURL command, Grep + regex
It was shared by [@Spiderfoot](https://twitter.com/spiderfoot): 

```
$ curl -s [YOUR DOMAIN HERE] | grep -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b"
```

Let's honor Spiderfoot by taking their domain as an example:

```
$ curl -s https://www.spiderfoot.net | grep -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b"
```
<br> 

<img width="1109" src="https://user-images.githubusercontent.com/104733166/186537612-08a532b2-3456-4dd9-bd9a-72ecebcfac69.png">

<br>

Great results!!! less than 2 seconds, obviously, this information isn't secret, it's open source, we could get it from a browser search, but how many seconds or minutes have we gained? 
It's quite easy becoming a fan of using cURL+Grep and learning regex.

<br>
I really like the Spiderfoot explanation in regards to this cURL and grep command:

<br>

>The curl command simply prints the HTTP response to https://www.spiderfoot.net, and the grep command contains a regular expression (regex) that finds and prints all emails within the source code. You can see that in this case, it found one, support@spiderfoot.net. A similar process could be followed to extract other information such as phone numbers, names, hostnames, etc.

<br>

We were born with brains that need to be used each day, please don't make the mistake or to be lazy by just copying and pasting commands, learn what you are doing and why you are doing, this is why I am taking the time to explain each command, I used to be that guy, and I would copy/paste commands that work, without understanding the commands. This means if you want to adapt or tweak the commands for something else, you would be left stranded.
Take time to analyze another Regex string that works for discovering emails:
<br>
How is an email structured: support[1]@[2]spiderfoot[3].[4]com[5]
<br>

`[a-zA-Z0-9._-]\+@[a-zA-Z]\+.[a-zA-Z]\+`

- [1] [a-zA-Z0-9._-] The text before the @ can be lowercase a-z, uppercase A-Z, numbers 0-9, a period, underscore or hyphen
- [2] [\+@] Obviously, this can only be an @ sign, `\+` this just means we want to combine the pattern without breaking it
- [3] [a-zA-Z] Same as number 1, we can see here this regex string has not included numbers, you could have numbers in a domain name so I prefer the string o spiderfoot.
- [4] [\+.] Obviously we know there is always a period before a `com` or `net` or `org` or `us` or `gov`, whatever ;-)
- [5] [a-zA-Z] letter for com or whatever else.


<br>

<br>


# Domain Commands
<img width="133" src="https://user-images.githubusercontent.com/104733166/186541301-e800e802-9980-4f38-9854-c639d8d148ff.png">

<br>

```
$ curl https://www.domain.com
```
This is the most basic of commands for beginners and will show the full response of the web server hosting the domain, it's long and messy but can be very useful.
*Notice that I put `https://www.` in front of the domain name, if I don't, I don't get a correst response, and the response is that the document has moved permanently.

You can avoid typing `https://www.` and can avoid the response of permanent move with this command:

```
$ curl -L github.com
```
`-L, or --location`= **Follow redirects**

<br>

View Headers Response with the `--head` command

```
$ curl --head https://github.com
```
or 


```
$ curl -I https://github.com
```
<br>

## Finding Subdomains
Searching for `Tracelabs.org` subdomains.
I did this simple command by looking around at how `crt.sh` works, I added `\&output\=json` at the end of the link, and as I mentionned previously, adding  `| jq --color-output` puts some nice color in the results and jq seems to act like `pprint` in python and sorts results that look much tidier. Remember also that I could have added `-o TL_results.txt` if I just wanted the results in a .txt file.

<br>

<img width="1145" src="https://user-images.githubusercontent.com/104733166/186715598-6ec5cb66-2bb4-4b0b-92e5-f5a439518a7a.png">

<br>

Results in .txt:

<img width="102" src="https://user-images.githubusercontent.com/104733166/186715803-5ce6c1ab-7e96-4ddd-83ef-f79b90180427.png">

## Downloading files during the investigation

Let's take this interpol PDF file as an example: https://rm.coe.int/3148-3-2-eurojust-presentation-interpol-approach-ukim-v2/1680791601

- -o will save your file as you name it, meaning you need to choose a name
- -O will save the file as it was called on the server

```
$ curl -o interpol.pdf https://rm.coe.int/3148-3-2-eurojust-presentation-interpol-approach-ukim-v2/1680791601

```
```
$ curl -O https://rm.coe.int/3148-3-2-eurojust-presentation-interpol-approach-ukim-v2/1680791601
```
Fantastic and fast, here is my downloaded file as I wanted it:

<img width="151" src="https://user-images.githubusercontent.com/104733166/186547270-fe5164ba-4ff6-4a56-86a9-28a010a90883.png">

This is a command I really like, you can request a progress car for large files.

Use the command --progress-bar or -#, they both do the same thing.

```
$ curl --progress-bar -o interpol.pdf https://rm.coe.int/3148-3-2-eurojust-presentation-interpol-approach-ukim-v2/1680791601
```
<br>

<img width="1589" src="https://user-images.githubusercontent.com/104733166/186547994-65d017ce-b5a4-48a8-a462-5ec4b38eb3ae.png">

<br>

You can also download multiple files at the same time which is awesome:

```
$ curl -O url -O url -0 url 
```
<br>

I found this interpol file with some dorking and it was downloaded using cURL, how about finding some emails on it without even opening the file?
We have worked with cURL and grep for this tutorial, but for this one out goes cURL and in comes grep! :-)

let's use this command to see if the interpol file has some email on it:

```
$ grep -a -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b" interpol.pdf
```
I put the `-a` command to force grep to treat the binary file as text, if I don't put it there I keep getting `Binary File matches`, without an email being printed.

- `-E`= extended regular expression (regex)
- `-o`= only matching | Meaning in this case Printing email addresses only

The email was found in a matter of milliseconds, it didn't even reach one second, the PDF is over 20 pages and the email is on the last page so it would have taken much longer to find it, this proves how useful cURL and grep are.

<img width="697" alt="Screen Shot 2022-08-25 at 03 36 10" src="https://user-images.githubusercontent.com/104733166/186554307-2542ef70-198a-41af-bc14-8befbdb629c5.png">

<br>

How about searching through domain source code for exact words or phrases? 🕵🏻‍♂️ <br>
A lot can be found within source code, things can be intentionally hidden there, and if you compete in CTF events, this technique can help you to find something quick in the source code. <br>

This is a fantastic example of combining cURL and grep.

I hid a quote from Mr.Robot (fsociety) in the source code, this is not visible on the website, and manually going through source code can be quite annoying and time consuming.

I will use the `grep -i` command. 

`grep -i` enables the command to be case insensitive. grep will search for uppercase or lowercase strings that matches the word or phrase.

<br>

Command:

```
$ curl -L tacs-sys.com | grep -i illusion
```
Bingo! 

<img width="633" src="https://user-images.githubusercontent.com/104733166/186700428-34fe951d-7877-40e7-9f46-223ef1d13ce4.png">


<br>

<br>

<br>

# Reddit

<img width="66" src="https://user-images.githubusercontent.com/104733166/186503090-6a749cca-0302-4908-a197-4042a7a8aed6.png">

The command we saw above for IP addresses would also work nicely for `reddit conversations`, simply add `.json` at the end of the link.

<br>

<br>

Example: https://www.reddit.com/r/OSINT/comments/wvnko3/how_to_extract_an_email_from_a_google_maps[.json]

```
$ curl -H "Accept: application/json" https://www.reddit.com/r/OSINT/comments/wvnko3/how_to_extract_an_email_from_a_google_maps.json
```

<br>

<img width="2199" src="https://user-images.githubusercontent.com/104733166/186504907-8cb16ad3-0213-420e-b13a-5758cb9dfa50.png">

<br>

You can probably see that the above results look a little messy, the following command will put some color into the results and will put the .json in a tidy format, this is thanks to the `jq`  command which acts like `pprint` in Python.

```
$ curl -H "Accept: application/json" https://www.reddit.com/r/OSINT/comments/wvnko3/how_to_extract_an_email_from_a_google_maps.json | jq --color-output
```
<br>

You can probably see that the above results look a little messy, the following command will put some color into the results and will put the .json in a tidy format, this is thanks to the `jq`  command which acts like `pprint` in Python.

<br>

As you can see above, if you add  `| jq --color-output`, you get tidy .json results and some color which makes it better and easier for our eyes.

<br>

<img width="633" src="https://user-images.githubusercontent.com/104733166/186518706-57748f3c-6d73-46b8-9020-cbf2952515d4.png">

<br>

We can see the `unix timestamp`on the photo, it's then easy to convert this into a date and time there is loads of online converters.

## What if you want all the information in a file?
Maybe you want all the information to keep for your investigation in a file. simply add the -o command meaning output and the file name you desire.
<br>
Command Example for the reddit post to get the information output in a file: 📁
<br>
```
$ curl -H "Accept: application/json" https://www.reddit.com/r/OSINT/comments/wvnko3/how_to_extract_an_email_from_a_google_maps.json -o reddit.json
```

<br>

Below is the result in `.json` format, you can request the output file in `.txt`, `.html`, and more formats, it's up to you.

<img width="797" src="https://user-images.githubusercontent.com/104733166/186527850-5a75a828-fc16-4771-9742-475ffe233c9e.png">


