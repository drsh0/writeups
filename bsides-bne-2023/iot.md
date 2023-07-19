## light bulb

300 points

team: ninjas

<details> 
<summary>hint</summary>
Look into the encryption type
</details>

![light bulb with instructions for ctf](chal-bulb.png)

### getting started

First, we needed to connect to the wifi network with the credentials provided. We ran a host scan once connected to the network see what we could see. As expected, we could see other hosts connected to the network with MAC org identifiers (OUI) such as Apple, Lenovo and so on. What stuck out to us (and this took way longer than it should have) was that there was a host identified as Microsoft host with `CONTOSO` in it's hostname. This was hinted at in the challenge preamble.

So what now? We scanned that host of course. If we had paid attention the first time, we would have noticed that `ssh` was open on port `22` and then we fell into a rabbit hole thinking was this even the right host? We confirmed this via Wireshark where we could definitely confirm that is what we were talking to internally. Eventually we ran the scan again and figured, hey, let's just connect to the host via `ssh` [^1]. Maybe we'll get some more info? Let's `ssh` in. 

Oh it's asking us for creds. Duh. Looks like we'll need to brute force right? With the creds wordlist the CTF provided? Nope, it was just `admin:admin`. After logging in with those credentials via ssh, we're presented with a greeting and menu options.

Unfortunately, we didn't capture screenshots of the light bulb interface via ssh so this crude recreation will have to do:

```
welcome to light bulb iot controller!

please select:

1. help 
2. control lightbult
3. command
4. exit

```
### owning the light bulb controller

After playing around with the controller (and making the light bulb flash a few times because why not?) the menu option that was most interesting to us was `3. command`. This would present a way to ping a device. It expected us to issue `ping` and seemed to block everything else. However, our team tried the good ol' command injection techniques and we were able to bypass this and perform arbritary command execution. It looked something like this:

`ping 127.0.0.1; <any arbritary command>`

So, with this we listed the directory (`; ls`) and noticed something juicy: `file.bin` (we didn't record the exact filename, unfortunately).

However, it was evident soon after  that this was some sort of jailed or emulated shell as many utilities that we normally expected were not present e.g `file` `base64` and so on. We tried to `scp` the file out of the box but it wasn't just sitting in the home directory or path that we'd expect (jailed shell?). 

The main problem we had was that we could `cat` the file however the buffer would clear in about 3 seconds. After playing around with trying to get that file to our machine via reverse shells and other trickery, we just did something super low tech and relied on reflexes to copy and paste like the **ninjas** that we are. 

We now had the contents of `file.bin`. 

### cracking the code



[^1]: In retrospect, we should have just thought more about it and realised the simpler option is the right option. More methodical scanning such as versioning, banner grabbing etc may have also taken us on the right track the first time.
