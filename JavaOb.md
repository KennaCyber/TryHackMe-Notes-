**JavaScript Deobuscation by Hack The Box**

Room link: https://academy.hackthebox.com/course/preview/javascript-deobfuscation

Context:

-	Obfuscated code is a technique to make code/data difficult to understand.

-	Deobfuscation is making that code or data readable/understandable.

-	If you know how the obfuscation is done/how it was hidden, you can reverse the process and gain access to the original data.

-	Basically hiding info in plain sight.

Why’s it relevant?

-	Red and blue teams come across obfuscated code that hide certain functionalities, “like malware that utilizes obfuscated JavaScript code to retrieve its main payload.” 

    - The payload is the part of the cyber attack which causes harm. They can sit dormant on computers or networks for seconds to months before they are triggered. 

    - In a phishing attack, the payload could be in an email attachment.

    - Trojan Horse Analogy Breakdown: Malware(Greek soldiers hidden inside the wooden horse) utilizes obfuscated JavaScript code(The horse looks harmless, and the true purpose is hidden) to retrieve(once inside, they can open the gates) its main payload (army enters and attacks the city).

    - Trojan horse = obfuscated JavaScript that sneaks past guards, soldiers inside = the hidden scripts that set the stage, main payload = the army (real damage).

    - Main payload example: malware downloaded from a phishing link or attachment.

    - Code deobfuscation is relevant to code analysis and reverse engineering.

**Source Code**

-	Websites usually utilize JavaScript to perform functions necessary to run it.

-	HTML is used to determine the website’s main fields and parameters (like a blueprint/skeleton).

-	CSS determines its design.

-	All of this happens in the background, and we only see the front-end of the webite that we interact with.

-	All of this source code is available at the client-side (it’s sent to our device and can be viewed, it’s not hidden on a server) it is rendered by our browsers (turns the code into the visual webpage) so we don’t pay attention to the HTML source code.

-	If we want to understand a page’s client-side functionalities, we start by looking at this source code.

**HTML**

-	Pressing [CTRL + U] shpws the source code

**CSS**

-	Either internal within <style> tags in the HTML file, or external in a separate .css file and linked via a <link> tag.

**JavaScript**

- Same concept applies, so it can be internally written between <script> tags in the HTML file, or written in a separate .js file and referenced within the HTML code.

**Code Obfuscation**

- Usually achieved automatically by using an obfuscation tool, which rewrites the code to make it more difficult to read.

- Computers can still execute it, but usually performs slower(extra steps).

- They often create a dictionary, and then reconstruct the code using it.

Easy example:

- Original: 

- alert(‘Hi);

Obfuscated Version:

- var words = [‘alert’, ‘Hi’]

- window [words[0]] (words[1]) (ignore the spaces)

words[0] is ‘alert’ and words [1] is ‘Hi’

-	Some coding languages are complied: All of the code is translated into machine code (instructions the computer’s CPU can directly execute) before it runs. Examples; C, C++, C#

-	Some are interpreted: Their code is not directly executed by the CPU. Instead, another program (called an interpreter) reads the code line by line, translating and executing it into machine-level instructions as the program runs. Examples: Python, PHP, JavaScript

Python and PHP usually run on the server and not the user’s computer, but JavaScript runs on your browser. The code is sent directly to you, and your browser reads and runs it.

-	Since JavaScript is visible to anyone using the site, developers will often obfuscate it.

**Use Cases**

-	To prevent the code from being reused or copied, making it more harder to reverse engineer the code’s original functionality.

-	Provides a layer of security for authentication or encryption (high-value parts), since it’s harder for attackers to find and exploit weak spots. 

-	Doing authentication or encryption on the client-side isn’t recommended.

-	The usage of obfuscation is common for malicious actions as well. Intrusion Detection and Prevention systems may not detect their scripts.

**Basic Obfuscation**

-	It’s usually not done manually, and there are tools to do it.

-	Many malicious actors develop their own to make it more difficult to deobfuscate.

**Minifying JavaScript Code**

- Code minification reduces the readability but keeps it fully functional. The entire code is a single, very long line. Useful for longer code.

- javascript-minfier is a tool that does this. JSConsole can check if it runs as expected.

- Can be saved with the extension .min.js.

**Packing JavaScript code**

-	BeautifyTools can obfuscate the code, and the output is the same.

-	A packer is a kind of obfuscator. It hides the code by replacing important words into short labels (like a number). It stores the real words in a list/dictionary. A special function (p,a,c,k,e,d) re-builds those labels back into the original words during execution. 

-	They’re usually packed in a specific order so the function knows how to put everything back together when the code runs.

-	The function can be different from one packer to another. 

-	We can still see its main strings written in cleartext (unencrypted data that’s easily readable), which can give away what the code is doing.

**Advanced Obfuscation**

-	Completely obfuscated the code and hides clues of its original functionality.

**Obfuscator**

-	Obfuscator.io, but change the String Array Encoding to Base64, then click obfuscate.

**More Obfuscation**

-	JJ Encode or AA Encode are other obfuscators, but they can make the code execution very slow. Recommended for bypassing web filters or restrictions

**Deobfuscation**

-	Current code is all written in a single line (minified) so to properly format it, we need to Beautify it through our Browser Dev Tools.

-	Firefox example: [CTLR+SHIFT+Z] for debugger, then click the script. Click the ‘{ }’ button to fix the formatting.

-	Run it in Unpacker to deobfuscate it. You can also find the return value at the end and use console.log to print it.

**Reverse Engineering**

-	It can be harder tor tools to deobfucate code that’s heavily obfuscated, especially if it was obfuscated using a custom tool.

-	You could manually reverse engineer the code.

**Code Analysis**

-	Now that it’s deobfuscated, we can see that it has one function called generateSerial.

**HTTP Requests**

-	Defines variable xhr, which creates XMLHTTPREQUEST, which handles web requests.

-	Defines variable URL, which contains a URL to /serial.php with no domain specified.

-	It says xhr.send(null); because they want to send the request, but don’t have any data to include 

**Code Functions**

-	HTTP method = request you send to a webserver

-	POST = Command, HTTP method used to send data to a server, like if you have a form submission/file upload

-	xrl.open  is used with “POST” and URL. This opens the HTTP requests defined ‘GET or POST’ to the URL, the xhr.send sends the request, but doesn’t send extra data or expect anything back.

-	This function can be used to generate a serial number, like clicking a “Generate Serial” button. 

-	However, we didn’t see that button in the HTML, so maybe the developers haven’t used it yet?

-	We can try sending a POST request ourselves, and we can discover things.

**HTTP Requests**

**cURL**

-	Powerful command-line tool used in Linux distributions, macOS, and the latest Windows PowerShell versions. 

-	Can request any website by providing its URL

-	cURL is a tool used to send HTTP requests, such as POST

**POST Request**

-	To send, add -X POST to the command since it specifies the type of action, and add the -s to reduce unnecessary data 

Analogy:

-X POST = “I’m sending data”

The letter you want to send = POST data

“Postal service” = cURL 

Recipient = server that receives and processes it

POST data = Type -d “param1=sample” flag, -d stands for data, so whatever you write after it is sent as the body of the POST request

param1=sample = servers need labeled information, these are generic names (param1 = parameter name, sample = value). A real example would be username=kenn

-	curl -s http://SERVER_IP:PORT/ -X POST -d "param1=sample"

-	curl -s https://(ip address)/serial.php -X POST -d “null”

-	serial.php goes at the end because it’s a file on the webserver

-	Purpose: We are replicating the behavior of the generateSerial() function to see if we can find anything.

**Decoding**

-	The result was a weird encoded block of text

-	Common methods of obfuscated code: base64, hex, rot13

-	Base64 are easy to spot since they only contain alpha-numeric characters. Padding: They often end with one or two = characters used to pad the string, so its length is a multiple of 4.

-	Basically, = fills the gap if there’s not enough data.

-	In Linux, you’d echo it and | (pipe) to base 64.

-	Decode? Add -d.

-	Hex turns each letter into its ASCII number, then writes that number in hexadecimal

-	It only uses 0-9 and a-f.

-	In Linux, you can use the xxd -p command, and xxd -p -r to decode.

-	Caesar/Rot 13 is like sliding each letter forward by a fixed number, so the message looks scrambled. The most common way is shifting each letter 13 places forward. 

-	Has predictable patterns.

-	In Linux, there isn’t a specific command but you can create your own.

**Other Types of Encoding**

-	 There’s many more methods, so try to determine the type of encoding and look for online tools to decode it.

-	Encryption is much harder to reverse without the key.
-	The value we got is encoded using base64 (N2gxNV8xNV9hX3MzY3IzN19tMzU1NGcz).

