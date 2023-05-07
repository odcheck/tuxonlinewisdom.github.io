---
title: 'Get only a certain line out of a huge file in linux'
date: 2021-05-28
categories: [IT]
tags: [sed, linux]
---
Assuming you need lines 32 to 34 out of a large file.

**using awk**
``` 
awk 'FNR>=32 && FNR<=34' <nameofthefile>
```

**using sed**
```
sed -n '32,34p;45q' <nameofthefile>
```

