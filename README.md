# Saskatoon HSCTF Questions

## Web

##### Question 1 - Recon [Easy]
Flag is hidden in the source
```html
<button>Submit</button>
    </form>
    <!--Just in case... Admin password is hsctf{i_love_saskatoonhsctf}-->
  </body>
</html>
```

##### Question 2 - Recon [Easy]
Delete `style="display:none;"`
```html
<h2>Classifications</h2>
    <p style="display:none;">
      Several subgroups of the computer underground with different attitudes use different terms to demarcate themselves from each other, or try 
```

##### Question 3 - Recon [Easy]
Simple question, flag is hidden in `<script>` tags
```html
<script type="text/javascript">
  var code = "duajbx928dlxdlh1";
  function checkCoupon(){
    if($("#coupon-field").val() == code){
      alert("your flag is hsctf{question3}");
    } else {
      alert("oops, try again");
    }
  }
</script>
```

##### Question 4 - Base64 & Console [Easy]
Same as question 3, but flag is encrypted using base64. Use console to solve the question.
```
> atob("eW91ciBmbGFnIGlzIGhzY3Rme3F1ZXN0aW9uNH0=");
< "your flag is hsctf{question4}" = $1
```

##### Question 5 - SQL Injection [Medium]
SQL Injection. Type `' OR '1'='1` for the password.

It will result in a query like this `SELECT * FROM user WHERE username='xxx' AND password='' OR '1' = '1'`

##### Question 6 - SQL Injection 2 [Medium]
Get the flag from database

##### Question 7 - XSS (Cross-Site Scripting) [Medium]
Self re-tweet script

##### Question 8 - Badly stored password (SQL Injection & Brute force) [Hard]
Brute force 4 digit password, and retrive the flag from database

##### Question 9 - Unrestricted folder [Hard]
Retrive data from `config/` folder

##### Question 10 - Badly stored password 2 (SQL Injection, Brute force & Data Analyzation) [Insane]
Brute force 4 digit passowrd, and retrive the flag by analyzing similarities between hashes

## Reverse Engineering

##### Question 0 - Open [Super Easy] - General Question
Flag is available in a text file.

```
#the password is hsctf{kFt6leI95Pj8OVCeHV}

entry=input()

print(entry)
```

Answer: hsctf{kFt6leI95Pj8OVCeHV}

##### Question 1 - Run [Super Easy]
Run the code to output the answer.
```
# don't overthink this problem...

input="elevendigit"

def password_decrypter(password):
    changed=changer(password)
    weird=wierder(changed)
    print (weird)
def changer(q):
    altered_password=""
    for c in q: altered_password+=chr(ord(c)*2)
    return altered_password
def wierder(l):
    o=""
    cu=-1
    c=[98,101,103,120,100,97,99,113,91,89,107]
    for h in l:
        cu+=1
        o+=chr((ord(h)-c[cu]))
    return(o)

password_decrypter(input)

```

Answer: hsctf{easy}

##### Question 2 - Search [Easy]
Find the flag somewhat hidden in the code.

##### Question 3 - Print [Easy]
Edit some code by writing print in front of a function in order to print the output of a decryption function 
```


```


##### Question 4 - Semi-Caesar [Medium]
Move the characters a certain amount, given in the code (eg. 12). Use a caesar cypher to reverse a encrypted password by that much.

The output from this program was hsctf{iqxxpazq}. What is the flag?

```
flag=input()

encodedFlag=""
for c in flag:
    k=((ord(c)+12))
    if k>122 or (k>90 and k<102):
        k=k-26
    encodedFlag+=chr(k)
print("hsctf{"+encodedFlag+"}")
```

Answer: hsctf{welldone}


##### Question 4.5 - Make the Crossing [Medium]

This is a simple reverse engineering task

```
input=input ()

def password_crypter(password):

    split_password=password.split("_")

    split_password.reverse()

    split_password[3]="isn't"
    split_password[0]=split_password[0][:-1]
    split_password.remove("hsctf{however")

    split_password.reverse()

    new_password=""

    for i in split_password:
        new_password=new_password+i+"_"
    print(new_password[:-1])


password_crypter(input)


```



Answer:
hsctf{however_this_is_the_real_password}

##### Question 5 - Arithmetic [Medium]
Divide each character in a code by a certain number.

Problem text: Someone left their python pyscripter open, but removed the password from their password? Can you figure out what it is?

The printed value was ÐæÆèÌöÊðÆÊØØÊÜè¾äÊìÊäæÂØú and the python program is altered.py

```passphrase="<redacted>"

def altered(password):
    altered_password=""
    for character in password:
        altered_password+=chr(ord(character)*2)
    return altered_password

print(altered(passphrase))
```

Answer: hsctf{excellent_reversal}

##### Question 6 - Floor [Medium]
Floor Division (and analyzing the code).

##### Question 7 - Multiple [Medium]
Multiply and add to encode/decode.

##### Question 8 - Functions [Hard]
Perform several functions on a code to encrypt it (eg. convert to hex, square each digit in hex, output list of hex) give functions to reverse engineer.

##### Question 9 - TBD [Hard]

##### Question 10 - TBD [Insane]
