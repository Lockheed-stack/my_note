# Hadoop

---

### 基本概念

![](https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/hadoop basic conception.PNG)

* HDFS 

  *NameNode*:类似索引，记录数据分布存储的位置，记录文件的属性。

  *DataNode*:具体数据存储的位置。

  *Secondary NameNode(2nn)*:每隔一段时间对NameNode进行备份，以防NameNode挂掉。图中未画出。

```mermaid

graph TB
	a(NameNode,<br>文件A,200T.)-->b1(DataNode<br>Hadoop101<br>容量1T)
	a-->b2(DataNode<br>Hadoop102<br>容量1T)
	a-->b3(DataNode<br>Hadoop103<br>容量1T)
	a-->b4(.....)
	a-->b5(DataNode<br>Hadoop400<br>容量1T)
```

* YARN(Yet Another Resource Negotiator)，hadoop的资源管理器

  <img src="https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/yarn%20structure.png" style="zoom:50%;" />

  *可以有多个客户端，集群上能运行多个ApplicationMaster，每个NodeManager可以有多个容器*

  

* MapReduce

  *两个阶段*：

  1. Map阶段并行处理输入数据

  2. Reduce阶段对Map阶段进行汇总

     <img src="https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/2%20step%20of%20mapReduce.PNG" style="zoom:80%;" />



* HDFS、YARN、MapReduce关系

  ![](https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/HDFS_YARN_MapReduce.png)
  
  
  
  
  
  ### 大数据技术生态
  
  ![](https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/tech_ecosystem.PNG)
  
  *常见的业务流程*
  
  ![](https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/business%20process.PNG)

