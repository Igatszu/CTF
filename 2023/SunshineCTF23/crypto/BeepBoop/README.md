# SunshineCTF 2023

## BeepBoop Cryptography

> Help! My IOT device has gone sentient!
> 
> All I wanted to know was the meaning of 42!
> 
> It's also waving its arms up and down, and I...
> 
> oh no! It's free!
> 
> AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
>
> Automated Challenge Instructions
> Detected failure in challenge upload. Original author terminated. Please see attached file BeepBoop for your flag... human.
> 

### Solution
We recieved a file labeled `BeepBoop` containing the following:

```
beep beep beep beep boop beep boop beep beep boop boop beep beep boop boop beep beep boop boop beep boop beep beep beep beep boop boop beep beep beep beep boop beep boop boop boop boop beep boop boop beep boop boop boop beep beep boop beep beep boop boop beep boop beep boop boop beep boop boop beep beep boop boop boop beep boop boop boop beep beep boop beep beep boop boop beep beep boop beep boop beep boop boop boop boop beep boop beep beep boop boop boop beep boop boop beep beep boop boop beep beep beep beep boop beep boop boop beep boop boop boop beep beep boop boop beep beep boop boop boop beep boop boop boop beep beep boop beep beep beep boop beep boop boop beep boop beep boop boop boop beep beep boop beep beep boop boop beep boop beep boop boop beep boop boop beep beep boop boop boop beep boop boop boop beep beep boop beep beep boop boop beep beep boop beep boop beep boop boop boop boop beep boop beep beep boop boop boop beep boop boop beep beep boop boop beep beep beep beep boop beep boop boop beep boop boop boop beep beep boop boop beep beep boop boop boop beep boop boop boop beep beep boop beep beep beep boop beep boop boop beep boop beep boop boop boop beep beep boop beep beep boop boop beep boop beep boop boop beep boop boop beep beep boop boop boop beep boop boop boop beep beep boop beep beep boop boop beep beep boop beep boop beep boop boop boop boop beep boop beep beep boop boop boop beep boop boop beep beep boop boop beep beep beep beep boop beep boop boop beep boop boop boop beep beep boop boop beep beep boop boop boop beep boop boop boop beep beep boop beep beep boop boop boop boop boop beep boop
```

This appears to be binary. We can run the following command to convert it to binary:
```bash 
$ cat BeepBoop | sed s/boop/1/g | sed s/beep/0/g | tr -d '[:space:]' | sed 's/\([0-9]\{8\}\)/\1 /g' > booped.txt  
```
Lets break down what this command does:
  - `cat BeepBoop` - Prints the content of the `BeepBoop` file
  - `sed s/boop/1/g` - Substitutes any `boop` with a `1` throughout the file.
  - `sed s/beep/0/g` - Substitutes any `beep` with a `0` throughout the file.
  - `tr -d '[:space:]'` - Deletes all whitespace characters.
  - `sed 's/\([0-9]\{8\}\)/\1 /g` - Finds all instances of 8 consecutive digits and inserts a space after each sequence.
  - `> booped.txt` - Stores the output into a file.

Reading our new `booped.txt` file we now get the following output:

```
00001010 01100110 01101000 01100001 01111011 01110010 01101011 01100111 01110010 01100101 01111010 01110110 01100001 01101110 01100111 01110010 00101101 01110010 01101011 01100111 01110010 01100101 01111010 01110110 01100001 01101110 01100111 01110010 00101101 01110010 01101011 01100111 01110010 01100101 01111010 01110110 01100001 01101110 01100111 01110010 01111101
```
Using https://www.rapidtables.com/convert/number/binary-to-ascii.html to convert our binary to text we get the following:

  `fha{rkgrezvangr-rkgrezvangr-rkgrezvangr}` 

Seeing this output and knowing the flag format is `sun{}` we can deducde that `fha{ == sun{`. This gave also gives it away that this is likely a `rot13` cipher since the letters `f, h, and a` are 13 letters away from `s, u, and n`.

Running the following gets us our flag:
```bash
$ echo 'fha{rkgrezvangr-rkgrezvangr-rkgrezvangr}' | rot13
sun{exterminate-exterminate-exterminate}
```

FLAG: `sun{exterminate-exterminate-exterminate}`
