---
title: 12 跳过前3个文档,返回其余的（skip）
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
this.ctx.model.Article.skip(3);
```

- 对Article表中的数据进行返回，跳过前面3条数据，返回其余数据

附：综合使用最后三个方法进行分页查询

```javascript
this.ctx.model.Article.find({ _id：5c4a819fb87ba4002a47bc4f }).skip(pageSize * (pageNum - 1)).limit(parseInt(pageSize)).sort({ isSetTop: -1, sort: 1, editTime: -1 });
```

- 其中pageSize和pageNum为动态传递数据，返回Article表中特定_id在每页数据为pageSize条件下的第pageNum页中的数据，并按照“isSetTop”降序，再按“sort”升序，最后按“editTime”降序进行排序。
