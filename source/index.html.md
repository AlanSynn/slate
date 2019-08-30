---
title: Docs List

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='http://www.flysher.net'>Flysher Dev Team</a>
  - http://www.flysher.net

includes:

search: true
print: false
---

# Docs List

> Request

```javascript
const alansynn = require('alansynn');
var think = alansynn.think();
var code = alansynn.code(think);
var test = alansynn.test(code);
var document = alansynn.document(think, code, test);
console.log(document);
```

> Response  

```json
{
    "host": "alansynn",
    "result": "snazzy"
}
```

### README
+ [커스텀한 내역](docs/README)
+ [Slate](docs/Slate_README)

### Events
+ [Cross Word](docs/events/crossWordEvent)

### Slots
+ [82. Diamond Cats](docs/slots/diamondCats)
+ [85. LunarFortune](docs/slots/lunarFortune)
+ [88. Jackpot Queens](docs/slots/jackpotQueens)
