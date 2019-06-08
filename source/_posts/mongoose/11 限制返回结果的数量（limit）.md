---
title: 11 限制返回结果的数量（limit）
date: 2019-04-10 11:10:04
tags: mongoose
desc: 
# keywords: 
categories:
  - mongoose
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

```javascript
this.ctx.model.Article.limit(3);
```

- 对Article表中的数据进行返回，返回为前面3条数据
