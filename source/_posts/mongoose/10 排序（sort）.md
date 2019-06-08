---
title: 10 排序（sort）
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
this.ctx.model.Article.sort({ isSetTop: -1, sort: 1, editTime: -1 });
```

- 对Article表中的数据进行排序，先按“isSetTop”降序，再按“sort”升序，最后按“editTime”降序

备注：键对应数据中的键名，值代表排序方向，1 升序, -1降序。
