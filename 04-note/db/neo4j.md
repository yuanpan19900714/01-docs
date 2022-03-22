# 图数据库有哪些优点？
图数据库(Graph Database)是一种以图结构进行存储和查询的数据库。图数据库的关键概念是点（代表实体）和边（代表关系），通过边将顶点连接在一起，从而进行快速的图检索操作。
## 图数据库的优点
1. 使用图（或者网）的方式来表达现实世界的关系很直接、自然，易于建模。比如某人喜欢看某电影，就可以建立一条边连接这个人和这部电影，这条边就叫做“喜欢”边，同时这个人还可以有其它边，比如“朋友”边、“同学”边等，同样这个电影也可以有其它边，比如“导演”边、“主演”边等，这样就构建了自然的关系网。
2. 图数据库可以很高效的插入大量数据。图数据库面向的应用领域数据量可能都比较大，比如知识图谱、社交关系、风控关系等，总数据量级别一般在亿或十亿以上，有的甚至达到百亿边。mysql不做分表分库的情况下插入百万数据基本就慢到不行，图数据库基本能胜任亿级以上的数据，比如neo4j、titan(janus)、hugegraph等图数据库，持续插入十亿级的数据基本还能保持在一个较高的速度。
3. 图数据库可以很高效的查询关联数据。传统关系型数据库不擅长做关联查询，特别是多层关联（比如查我的好友的好友有哪些人），因为一般来说都需要做表连接，表连接是一个很昂贵的操作，涉及到大量的IO操作及内存消耗。图数据库对关联查询一般都进行针对性的优化，比如存储模型上、数据结构、查询算法等，防止局部数据的查询引发全部数据的读取。
4. 图数据库提供了针对图检索的查询语言，比如Gremlin、Cypher等图数据库语言。图查询语言大大方便了关联分析业务的持续开发，传统方案在需求变更时往往要修改数据存储模型、修改复杂的查询脚本，图数据库已经把业务表达抽象好了，比如上面的2层好友查询，Gremlin实现为g.V(me).out('friend').out('friend')，如果需要改为2层同学查询，那调整一下把好友换为同学即可g.V(me).out('classmate').out('classmate')。
5. 图数据库提供了专业的分析算法、工具。比如ShortestPath、PageRank、PersonalRank、Louvain等等，不少图数据库还提供了数据批量导入工具，提供了可视化的图显示界面，使得数据的分析结果更加直观展示出来。
 ## 图数据库的缺点
 1. 不适合记录大量基于时间的数据（例如日志）。
 2. 不善于二进制数据的存储。
 3. 不适用于并发性能要求高的项目。
 4. 图查询语言较多，未能统一。
 5. 相关资料较少，生态还未完善。