# Redis

## Nosql概述

### 为什么用NoSQL

> **一、单机MySQL**
>
> 存在问题：
>
> 1、数据量太大，一台机器放不。
>
> 2、数据的索引，一个机器内存也放不下。
>
> 2、读写混合，一台机器无法承受。
>
> **二、MemCache+MySQL+垂直拆分**
>
> 网站80%的情况是读操作，每次都查询数据库就会很慢。为了减轻数据库压力，使用缓存来保证效率。
>
> ![image-20220317212836517](H:/school_materal_temp/%E7%A1%95%E5%A3%AB/MK%E7%AC%94%E8%AE%B0/redis/redis.assets/image-20220317212836517.png)
>
> **三、分库分表+水平拆分+MySQL集群**
>
> ![image-20220317214057135](H:/school_materal_temp/%E7%A1%95%E5%A3%AB/MK%E7%AC%94%E8%AE%B0/redis/redis.assets/image-20220317214057135.png)
>
> **四、最近（2020）**
>
> 数据类型多、变化快、数量多，MySQL等关系型数据库不够用。
>
> ![image-20220317215142518](H:/school_materal_temp/%E7%A1%95%E5%A3%AB/MK%E7%AC%94%E8%AE%B0/redis/redis.assets/image-20220317215142518.png)
>
> Nosql可以很好处理以上情况。

### 什么NoSQL

> **NoSQL = Not Only SQL**，泛指非关系型数据库。