bui# Summary

* [前言](README.md)

### [第一部分 Lucene 核心](part-1/part-1.md)

* [第2章 构建索引 Building a search index](part-1/ch2/ch2.md)
  * [2.1 Lucene 如何对搜索内容进行建模 How Lucene models content](part-1/ch2/ch2-01.md)
    * [2.1.1 文档和域 Documents and fields](part-1/ch2/ch2-01.md#1)
    * [2.1.2 灵活的架构 Flexible schema](part-1/ch2/ch2-01.md#2)
  * [2.2 理解索引过程 Understanding the indexing process](part-1/ch2/ch2-02.md)
    * [2.2.1 提取文本和创建文档 Extracting text and creating the document](part-1/ch2/ch2-02.md#1)
    * [2.2.2 分析 Analysis](part-1/ch2/ch2-02.md#2)
    * [2.2.3 添加到索引 Adding to index](part-1/ch2/ch2-02.md#3)
      * [倒排索引 Inverted Index](part-1/ch2/ch2-02.md#31)
      * [正向索引 Forward Index](part-1/ch2/ch2-02.md#32)
      * [索引段 Index Segments](part-1/ch2/ch2-02.md#33)
  * [2.3 基本索引操作 Basic index operations](part-1/ch2/ch2-03.md)
    * [2.3.1 IndexWriter 概述 Introduction of IndexWriter](part-1/ch2/ch2-03.md#1)
    * [2.3.2 向索引添加文档 Adding documents to index](part-1/ch2/ch2-03.md#2)
    * [2.3.3 删除索引中的文档 Deleting documents from an index](part-1/ch2/ch2-03.md#3)
    * [2.3.4 更新索引中的文档 Updating documents in the index](part-1/ch2/ch2-03.md#4)
  * [2.4 域选项 Field options](part-1/ch2/ch2-04.md)
    * [2.4.1 域索引选项 Field options for indexing](part-1/ch2/ch2-04.md#1)
    * [2.4.2 域存储选项 Field options for storing fields](part-1/ch2/ch2-04.md#2)
    * [2.4.3 域的词项向量选项 Field options for term vectors](part-1/ch2/ch2-04.md#3)
    * [2.4.4 域分析选项 Field options for analysis](part-1/ch2/ch2-04.md#4)
    * [2.4.5 域 DocValuesType 选项 Field options for DocValuesType](part-1/ch2/ch2-04.md#5)
    * [2.4.6 域 Norms 选项 Field options for Norms](part-1/ch2/ch2-04.md#6)
    * [2.4.7 FieldType 的 freeze 选项 FieldType options for freeze](part-1/ch2/ch2-04.md#7)
  * [2.5 域的值类型 value type of Field](part-1/ch2/ch2-05.md)
    * [2.5.1 域的二进制类型值 binary value type of Field](part-1/ch2/ch2-05.md#1)
    * [2.5.2 域的字符序列类型值 CharSequence value type of Field](part-1/ch2/ch2-05.md#2)




  * [术语 terminology](part-1/ch2/terminology.md)

* [第5章 高级搜索技术](part-1/ch5/ch5.md)
  * [5.6  搜索过滤](part-1/ch5/ch5-06.md)
     * [5.6.1 词项范围过滤 Term Range Filter](part-1/ch5/ch5-06.md#1)
     * [5.6.2 数值范围过滤 Numeric Range Filter](part-1/ch5/ch5-06.md#2)
     * [5.6.3 利用 DocValues 范围过滤](part-1/ch5/ch5-06.md#3)
     * [5.6.4 过滤特定的词项 Filtering by specific terms](part-1/ch5/ch5-06.md#4)
     * [5.6.5 使用 ConstantScoreQuery 类](part-1/ch5/ch5-06.md#5)
     * [5.6.6 使用 SpanQuery 进行过滤](part-1/ch5/ch5-06.md#6)
     * [5.6.7 安全过滤器 Security filters](part-1/ch5/ch5-06.md#7)
     * [5.6.8 使用 BooleanQuery 类过滤](part-1/ch5/ch5-06.md#8)
     * [5.6.9 使用 PrefixQuery 类过滤](part-1/ch5/ch5-06.md#9)
  * [5.7 使用功能查询实现自定义评分 Custom scoring using function queries](part-1/ch5/ch5-07.md)
  * [5.8 针对多索引的搜索 Searching across multiple Lucene indexe](part-1/ch5/ch5-08.md)
  * [5.9 利用词项向量 Leveraging term vectors](part-1/ch5/ch5-09.md)




















### [第二部分 Lucene 应用](part-2/part-2.md)







### [第三部分 Lucene 案例分析](part-3/part-3.md)