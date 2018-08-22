## Redis
一、五种基本的数据类型
String  list  hash  set  sorted set(排序集合)
二、五种特性
（1）inmemory  在内存中   与cache类似，是一个以key-value存储的缓存系统
（2）弱化事务   基本是没有事务概念的，只有在某些地方会对事务进行遍历，而且它的遍历也不是遇到错误就停下来，而是遇到错误不管也不处理。
（3）集群环境
（4）Key-value查询
（5）脚本语言支持
三、
redis是一个单线程的系统，
支持持久化（cache不支持持久化），
订阅/发布功能
（
Redis 的消息队列功能
A    B    C
如果A,B,C服务器都订阅redis的某个key，那么就可以通过A在这个key里发布信息，放到redis的消息队列，redis会把消息推送到所有订阅了这个key的B，C服务器。Redis本身是不存储这个数据的。
）
四、redis和Memcache的区别
Memcache不能集群，最大为1M
Redis可以集群，最大为1G
五、Redis 常用于web服务器和数据库之间，充当缓存系统，因为其具有持久化功能，可以连接数据库，大量的数据放在redis里面缓存，web服务器或者应用与redis缓存进行交互，可提高程序执行的性能。
   Web服务器——redis服务器——数据库
六、redis有一个第三方的图形界面 Redis Desktop Manager。不过并不是特别的好用。
七、Redis数据结构的各种命令
         http://redisdoc.com/  redis命令参考
String 类型 
List类型
Lpush  Rpush  Lpop  Rpop  Irange  BLpop Brpop阻塞版 
八、Session管理
九、集群服务
1、解决单节点故障
2、读写分离
                                Redis share
Web服务器 ——redis mater
                                Redis share
十、Redis充当Message Queue
消息队列    实现订阅/发布功能
十一、redis充当数据库服务器
十二、Redis目前需要解决的问题就是内存问题？
内存有限，游戏数据庞大，如何把redis内存中的数据写入到数据库中，或者从数据库中读出来数据。
1、序列化到本地
2、Redis是否支持数据写入到内存中
3、集群扩容，不过这只能解决容量的问题，不能解决游戏中大量死数据的问题
解决内存问题：主要还是要从如果从游戏死数据中分离出来活跃用户的角度下手。
方法：合服的时候清除死数据，判断玩家playerBean数据是否超过某一时间，超过时间设置玩家playCache里状态标识位为非法。在从数据库大量load玩家playerCache数据到内存中，状态非法和数据为空的被剔除掉。
