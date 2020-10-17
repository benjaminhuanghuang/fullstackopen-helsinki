

如果用关系型数据库,每个资源都会有独立的数据库表，而创建 Note 的 用户 ID 会作为 Note 的外键进行存储

传统的文档数据库，如 Mongo 是不支持join queries的，但这在关系型数据库却很常见，用来聚合不同表中的数据。
从 Mongo 3.2 开始，它开始支持lookup aggregation queries。

此处利用 multiple queries 来实现类似 join queries 的功能。
Mongoose 可以处理 join 和聚合数据，使它看起来像 join 查询 一样。但 Mongoose 其实也是在后台数据库使用了 multiple query。


文档型数据库提供了一个完全不同的方式组织数据：将所有的 note 以数组的形式作为每个文档的一部分嵌套在 user collection 中


此处将 note 的 id 以数组的形式存储到 user 当中。 代码见 models/user.js



