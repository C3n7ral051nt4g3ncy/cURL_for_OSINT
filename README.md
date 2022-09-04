<p align="center"> <img width="233" height="199" src="https://user-images.githubusercontent.com/104733166/186285439-d9463805-3354-429a-baf4-3e960826028f.gif"><p/>

<br>

# cURL for OSINT
### cURL Tool usage (with grep) for OSINT (Open-Source Intelligence)

<br>

![curl-logo](https://user-images.githubusercontent.com/104733166/186279152-3ca718a8-966c-48ac-b1f8-061435f57af6.svg)
<br>
<br>
<br>

# Background Information
cURL is a command line tool created in 1998 by [Daniel Stenberg](https://twitter.com/bagder), a Swedish Developper/Programmer.
<br>
Daniel Stenberg's website: https://daniel.haxx.se
<br>
The latest version of the Tool and the code is open source right here on GitHub: https://github.com/curl/curl

<br>

# What exactly does cURL do?
I am not a cURL expert and it's quite difficult giving an exact explanation so I will try and give the most basic explanation.
cURL means `Client URL` and you already know from above that it's a command line tool, so it's basically a tool that permits/enables data transfer over many network protocols (HTTPS, HTTP, FTP, it also supports SSL Certificates). The tool communicates with a web server with a URL and tells the server the data to be sent or received. (yes you read that correctly, **the tool can do both** 🤓)

<br>

# Difficulty
cURL is fairly easy to use, and if you have never opened your Terminal before, now is the time to do so 🤩.

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
Now that you have everything installed, we are good to go ✅, so let's have a look at some commands for OSINT (Open-Source Intelligence).
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

### Get more detailed information on your IP:
```
$ curl ipinfo.io
```
Example below, we can see that there is a lot more information on my IP such as city, country, organization, timezone, GPS coordinates:

<img width="433" src="https://user-images.githubusercontent.com/104733166/186290638-42617392-581a-4639-9275-607bcab2481f.png">

It also works well with this command (.json format)

```
$ curl ipinfo.io/json
```
Below is another command to make sure we really get the `JSON` and not the homepage `html`


```
$ curl -H "Accept: application/json" ipinfo.io
```

`-H takes a single parameter of an extra header to include in the request and Accept adds the Accept request headers to the request`

<br>
<br>

Let's do more tests using Google's IP address.<br>

Below are the commands when you know the IP address of the target , and as an example below, you want to know the **city**.

```
$ curl ipinfo.io/8.8.8.8/city
```
<br>
Results:
<img width="366" src="https://user-images.githubusercontent.com/104733166/186506023-a37ef2d1-fae7-47e7-a732-bc5b999ef898.png">
<br>

Get the **Country**:
```
$ curl ipinfo.io/8.8.8.8/country
```
<br>

Get the **Organization**:
```
$ curl ipinfo.io/8.8.8.8/org
```

<br>
<br>
<br>


# Whois Commands

<img width="133" src="https://user-images.githubusercontent.com/104733166/186533300-4d97e784-00e1-4b0b-8f84-2f40abf6cb9f.png">

I particularly like this easy command to get Whois information, this is not my work, it's the work of [Sector035](https://sector035.nl) and was shared on an article called [dial cURL for Content on OSINTCuriou.us](https://osintcurio.us/2019/06/25/dial-curl-for-content/)

```
$ curl cli.fyi/inputdomainhere
```
<br>

Let's test with the website of the French Presidential Palace:
<br>
```
$ curl cli.fyi/elysee.fr
```
Perfect results: 👍

<img width="633" src="https://user-images.githubusercontent.com/104733166/186533013-2716e467-0e82-4fb9-87bc-003cd0a355d1.png">

<br>

I will add my personal touch to this command, with some added color, the color doesn't show as a big difference with these results, but wait until you see how it works further on below with messy results and how the `jq` command can really make a difference.


<br>

```
$ curl cli.fyi/elysee.fr | jq --color-output
```

<br>

<img width="333" alt="Screen Shot 2022-08-25 at 00 20 53" src="https://user-images.githubusercontent.com/104733166/186533988-ea8abfd2-9546-4138-b016-8f75761cfba8.png">

<br>

I really like this command below:
<br>

```
curl -s http://ip-api.com/json/[input Domain or IP address] | jq -r .as
```

With this API you can input either a `domain` or an `IP address`, the commands after the IP or domain are `jq` which we will talk about further on below, and `-r` which means range, you can use `-r` or `--range`,  and depending on the information you require about the domain, you can put: .org or .isp or .city or .country or .RegionName or .as. 

`-s` just means silent (hiding progress)

Let's try this command:

```
$ curl -s http://ip-api.com/json/visitiran.ir | jq -r .city
```
<br>

<img width="533" src="https://user-images.githubusercontent.com/104733166/186725342-ec8d06ff-765a-4c6e-a17b-7f4662377b57.png">
We can see the city is: `Tehran` for the domain we tested on.

<br>

<br>


# Whois History

There are many sites you can get a `Free API Key` from.<br>
One site I like is [whoisfreaks](https://whoisfreaks.com), just head over and join and you will get your API Key with 100 API calls.

This is a command for historical whois information:

<br>

```
$ curl -s  https://api.whoisfreaks.com/v1.0/whois\?apiKey\=API_Key_here\&whois\=historical\&domainName\=cnn.com | jq --color-output
```

Don't forget that you can also use `grep` if you just want to see email addresses and not the full information.

<br>

<img width="1233"  src="https://user-images.githubusercontent.com/104733166/187009377-9a3fff5b-fd0d-4e4b-845b-22be2b175f8a.png">

<br>

<br>

# Getting an email from a Domain with cURL + Grep

<img width="333" src="https://user-images.githubusercontent.com/104733166/186535617-dba770e5-72c2-4e7b-9854-2b49a821cb9f.jpg">

Grep Website: https://www.gnu.org/software/grep/manual/grep.html

### What is Grep?
grep prints lines that contain a match for one or more patterns | Regex (Regular Expressions) <br>

Why is it called grep?: 
- g/re/p: **globally search for a regular expression and print matching lines**

<br>

This is not my work, this is a fantastic email scraper with a cURL command, grep + regex string. <br>
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

Great result!!! I timed it, it took less than 2 seconds.<br> 
It's quite easy becoming a fan of using cURL and Grep and learning about regex (regular expressions) 

<br>

I enjoyed reading the Spiderfoot explanation below in regards to this cURL + grep command:

<br>


>The curl command simply prints the HTTP response to https://www.spiderfoot.net, and the grep command contains a regular expression (regex) that finds and prints all emails within the source code. You can see that in this case, it found one, support@spiderfoot.net. A similar process could be followed to extract other information such as phone numbers, names, hostnames, etc.

<br>

Let's take a minute to analyze another Regex string that works for discovering emails:

<br>

How an email is structured: support[1]@[2]spiderfoot[3].[4]com[5]

<br>

`[a-zA-Z0-9._-]\+@[a-zA-Z]\+.[a-zA-Z]\+`

- [1] [a-zA-Z0-9._-] The text/username before the @ can be lowercase a-z, uppercase A-Z, numbers 0-9, a period, underscore or hyphen
- [2] [\+@] Obviously, this can only be an @ sign, `\+` this just means we want to combine the pattern without breaking it
- [3] [a-zA-Z] Same as number 1, we can see here that this regex string does not include numbers, you could have numbers in a domain name, I prefer the string of Spiderfoot.
- [4] [\+.] We know there is always a period/dot `.` before a `com` or `net` or `org` or `us` or `gov`, whatever 🤓
- [5] [a-zA-Z] Lowercase or Uppercase letter for com or net/org/us/io/gov/app/it (as above).

<br>

Remember also that the `-s` command that Spiderfoot used means silent, and you can do `-s` or `--silent` to implement it, it does not show the progress meter or error messages but will still output the data ✔️

<br>

<br>


# Domain Commands
<img width="133" src="https://user-images.githubusercontent.com/104733166/186541301-e800e802-9980-4f38-9854-c639d8d148ff.png">

<br>

```
$ curl https://www.domain.com
```
Above, this is the most basic of commands for beginners and will show the full response of the web server hosting that domain, the information returned is long and messy but can be very useful.

*Notice that I put `https://www.` in front of the domain name, if I don't, I won't get a correct response, the response will be that the document has moved permanently.

You can avoid typing `https://www.` and can avoid the response of a `permanent move` with this command:

```
$ curl -L github.com
```
`-L, or --location`= **Follow redirects**

<br>

View Headers Response with the `--head` command:

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

I did this simple command by looking around at how `crt.sh` works:

```
$ curl -s https://crt.sh/?q=tracelabs.org&output=json | jd --color-output
```


I added `\&output\=json` at the end of the link, and as I mentionned previously, adding  `| jq --color-output` puts some nice color in the results and `jq` seems to act like `pprint` in python and sorts results, making them look much neater. 

I could also have added `-o TL_results.txt` if I just wanted the results in a .txt file, and the `-o` command lets us choose the name of the file and format of the file.

<br>

<img width="1145" src="https://user-images.githubusercontent.com/104733166/186715598-6ec5cb66-2bb4-4b0b-92e5-f5a439518a7a.png">

<br>

Results in .txt:

<img width="102" src="https://user-images.githubusercontent.com/104733166/186715803-5ce6c1ab-7e96-4ddd-83ef-f79b90180427.png">

<br>

<br>



# Downloading files during the investigation

Let's take this Interpol PDF file as an example that I found with some Dorking: https://rm.coe.int/3148-3-2-eurojust-presentation-interpol-approach-ukim-v2/1680791601

- -o will save your file as you name it, meaning you need to choose a name
- -O will save the file as it was called on the server

```
$ curl -o interpol.pdf https://rm.coe.int/3148-3-2-eurojust-presentation-interpol-approach-ukim-v2/1680791601

```
```
$ curl -O https://rm.coe.int/3148-3-2-eurojust-presentation-interpol-approach-ukim-v2/1680791601
```
Fantastic and fast! here is my downloaded file as I wanted it with the name I chose:

<img width="151" src="https://user-images.githubusercontent.com/104733166/186547270-fe5164ba-4ff6-4a56-86a9-28a010a90883.png">

<br>


Below is a command I really like 🥳, you can request a progress bar for large files that take a long time to download:

>Use the command `--progress-bar` or  `-#`, they both do the same thing.

```
$ curl --progress-bar -o interpol.pdf https://rm.coe.int/3148-3-2-eurojust-presentation-interpol-approach-ukim-v2/1680791601
```
<br>

<img width="1589" src="https://user-images.githubusercontent.com/104733166/186547994-65d017ce-b5a4-48a8-a462-5ec4b38eb3ae.png">

<br>

You can also download multiple files at the same time which is awesome:

```
$ curl -O url -O url -O url 
```
<br>

We downloaded the file using cURL, how about finding emails on it without even opening the file?

cURL and grep are great working together, but for this one, OUT goes cURL and IN comes grep! 👊

<br>

<br>

Let's use the below command to see if the interpol file has some emails on it:

```
$ grep -a -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b" interpol.pdf
```

I put the `-a` command to force grep to treat the binary file as text, if I don't put it there I keep getting `Binary File matches`, without an email being printed.

- `-E`= extended regular expression (regex)
- `-o`= only matching | Meaning in this case Printing email addresses only

>The email was found in a matter of milliseconds, it didn't even reach 1 sec, the PDF is over 20 pages and the email is on the last page so it would have taken much longer to find it, this proves how useful cURL and grep are.

<br>

<img width="697" alt="Screen Shot 2022-08-25 at 03 36 10" src="https://user-images.githubusercontent.com/104733166/186554307-2542ef70-198a-41af-bc14-8befbdb629c5.png">

<br>

How about searching through domain source code for exact words or phrases? 🕵🏻‍♂️ <br>
A lot can be found within source code, things can be intentionally hidden there, and if you compete in CTF events, the below command can help you to find something quick within the source code. <br>

>This is a fantastic example of combining cURL and grep:

I hid a quote from Mr.Robot (fsociety) in the source code, this is not visible on the website, and manually going through source code can be quite annoying and time consuming.

Let's use the `grep -i` command. 

`grep -i` enables the command to be case insensitive, meaning grep will search for uppercase or lowercase strings that matches the word or phrase.

<br>

Command:

```
$ curl -L tacs-sys.com | grep -i illusion
```
Bingo! 

<img width="633" src="https://user-images.githubusercontent.com/104733166/186700428-34fe951d-7877-40e7-9f46-223ef1d13ce4.png">

<br>

<br>

# Google UA Analytics code finder

I created this one in a simple way, I know that I have Google Analytics.<br>
I will need to use cURL and grep together, and these 2 make a deadly team. 💪

1. I want a command that can return a Google UA code fast from any website I choose
2. I want to track the progress within my terminal
3. I don't want to have to type `https://www.` before the domain name
4. I will need to use grep and to create a regex string: "UA\-[0-9]+", I know that all Google Analytics codes start with UA, a hyphen after the UA, and it can only be numbers after the hyphen and never letters, so pretty easy right? 
5. -E : Treats pattern as an extended regular expression
6. -o : Prints only matched parts

```
$ curl --progress-bar -L tacs-sys.com | grep -E -o "UA\-[0-9]+"
```

*Keep in mind that this string I created would work fine too: `"UA+-[0-9]+"`

<br>

<img width="1339" src="https://user-images.githubusercontent.com/104733166/186732128-6193749c-2692-4731-b7f6-0907126bed25.png">
<br>

With the UA analytics code found, you can then use a reverse analytics site to check if the UA code is linked to another site: https://dnslytics.com/reverse-analytics

<br>

<br>

# Reddit

<img width="66" src="https://user-images.githubusercontent.com/104733166/186503090-6a749cca-0302-4908-a197-4042a7a8aed6.png">

A command we saw higher up for searching for IP addresses would also work nicely for `reddit conversations`, **just add** `.json` at the end of the Reddit conversation link.

<br>

Example: https://www.reddit.com/r/OSINT/comments/wvnko3/how_to_extract_an_email_from_a_google_maps[.json]

```
$ curl -H "Accept: application/json" https://www.reddit.com/r/OSINT/comments/wvnko3/how_to_extract_an_email_from_a_google_maps.json
```

<br>

<img width="2199" src="https://user-images.githubusercontent.com/104733166/186504907-8cb16ad3-0213-420e-b13a-5758cb9dfa50.png">

<br>

You can probably see that the above results look a little messy, the below command will put some color into the results and will put the `json` in a tidy format, this is thanks to the `jq`  command which acts like `pprint` in Python.

<br>

```
$ curl -H "Accept: application/json" https://www.reddit.com/r/OSINT/comments/wvnko3/how_to_extract_an_email_from_a_google_maps.json | jq --color-output
```

<br>

As you can see from the command above, if you add  `| jq --color-output`, you get tidy results and great color which makes it a lot easier for our eyes.

<br>

<img width="633" src="https://user-images.githubusercontent.com/104733166/186518706-57748f3c-6d73-46b8-9020-cbf2952515d4.png">

<br>

We can see the `unix timestamp` on the photo, it's then quite easy to convert this into a date and time as there is many free online converters.

<br>


## What if you want all the information in a file?
Maybe you want all the information for your investigation in a file.<br>
Simply add the `-o` command, meaning `output`, and add the file name you choose.

<br>

Command Example for the reddit post to get the information output into a file: 📁

<br>

```
$ curl -H "Accept: application/json" https://www.reddit.com/r/OSINT/comments/wvnko3/how_to_extract_an_email_from_a_google_maps.json -o reddit.json
```

<br>

Below is the result in `.json` format, you can request the output file in `.txt`, `.html`, and more formats, it's up to you.

<img width="797" src="https://user-images.githubusercontent.com/104733166/186527850-5a75a828-fc16-4771-9742-475ffe233c9e.png">

<br>

<br>

# Various other Commands
I learned these commands from Substack.<br>

You can download sed with this command:

```
brew install gnu-sed
```
<br>

I found the 2003 CIA World Factbook in a .txt file.<br>

This is one pretty awesome command that I will use below and by using cURL combined with sed we can do a lot of interesting stuff.<br>
SED stands for stream editor.

Wikipedia Def:
>Sed helps in operations like selecting the text, substituting text, modifying an original file, adding lines to text, or deleting lines from the text.

<br>

Command that will print every word in the book on a new line: <br>

```
$ curl -s https://www.gutenberg.org/files/27558/27558.txt | gsed -r 's/\s+/\n/g'
```
If you are on mac and downloaded `gnu-sed`, you need to use the `gsed` command and not `sed`.

<br>

Try this command also:

```
$ echo Tactical OSINT Analyst loves to spend time on GitHub |  gsed -r 's/\s+/\n/g'
```

<br>

<img width="633" src="https://user-images.githubusercontent.com/104733166/186768753-2ff1cbc9-6858-4b1a-bdfb-e56f7c406d5b.png">

<br>

As you can see, each word is on a new line thanks to SED. SED is basically acting like a white space detector, meaning every time there is white space in between a word, SED will treat that as a new line.

<br>

Let's bring grep into the picture, let's request to have the word China on a new line every time it's in the book.

<br>

```
curl -s https://www.gutenberg.org/files/27558/27558.txt | gsed -r 's/\s+/\n/g' | grep -i china
```

<br>

<img width="633" src="https://user-images.githubusercontent.com/104733166/186770745-3154fd21-7f70-400e-b718-33315e3e8ab2.png">

<br>

This brought back so many results.<br>
Now I would like to know how many times the word China was mentionned in the 2003 CIA World Factbook:

<br>

```
$ curl -s https://www.gutenberg.org/files/27558/27558.txt | gsed -r 's/\s+/\n/g' | grep -i china | wc -l
```
<br>

On the above command, `| wc -l` was added, meaning we can get a word count returned. <br>
Total times the word China was mentionned in the book is: **916**

<br>

<img width="833" src="https://user-images.githubusercontent.com/104733166/186771768-427fbbf0-5574-4b91-8992-935bf903667d.png">




<br>

<br>

<br>

# cURL commands list

Cheat sheet by [Daniel Stenberg (Haxx)](https://daniel.haxx.se/)


![cURL Cheat Sheet](https://user-images.githubusercontent.com/104733166/186732535-1fcbf63c-a984-435b-9b52-5112ad45f611.png)

<br>

<br>

<br>


# grep commands list


| Command | Or                    | Interpretation                               |
| --------|:---------------------:| --------------------------------------------:|
| -E      | --extended-regexp     | Extended Regular Expressions (Regex).        |
| --help  | --help                | Print a usage message                        |
| -V      | --version             | Print the version number of grep             |
| -e      | --regexp=patterns     | Use patterns for Matching                    |
| -a      | --text                | Process a binary file as if it were text     |
| -f      | --file=FILE           | Get patterns from FILE                       |
| -o      | --only-matching       | Print only matched parts of matching lines   |
| -r      | --recursive           | process files in directory, recursively.     |
| -F      | --fixed-strings       | Interpret patterns as fixed strings.         |
| -i      | --ignore-case         | Ignore case distinctions in patterns.        |
| -w      | --word-regexp         | Lines containing matches for whole words.    |
| -x      | --line-regexp         | Matches exacrlt the whole lines              |
| -c      | --count               | Print count of selected lines per file       |
| -s      | --no-messages         | Suppress error messages                      |
| -q      | --silent              | Quiet, do not write anything to output       |
| -G      | --basic-regexp        | patterns as basic regular expressions        |
| -v      | --invert-match        | Invert sense of matching (non matching lines)|
| -m      | --max-count=NUM       | Stop after the first num selected lines      |
| -n      | --line-number         | Print line number with output lines          |
| -H      | --with-filename       | Print file name with output lines            |
| -L      | --files-without-match | Print names of files with no selected lines  |
| -l      | --files-with-match    | Print names of files with selected lines     |

<br>

More information: https://www.gnu.org/software/grep/manual/grep.html
