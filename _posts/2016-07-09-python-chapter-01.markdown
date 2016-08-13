---
layout: post
title:  "Chapter01"
tags: python
permalink: /tech/python/chapter01
---

arkDown Test
------
> This is a paragraph inside
a blockquote.
>
> > This is a nested paragraph
that continues here
> and here
> > and here

~~~~~~~~ python
def factorial(x):
     if x == 0:
         return 1
     else:
         return x * factorial(x - 1)
~~~~~~~~

definition term 2
 * first
 * Second
  * second-first
  * second-second



  <h3>Background</h3>
  <hr/>

  key-value store인 RocksDB를 사용중 key를 그룹핑하고, 그룹에 해당하는 모든 key를 얻어야 하는 상황이 발생.

  RocksDB에서 제공하는 <a target="_blank" href="https://github.com/facebook/rocksdb/wiki/Prefix-Seek-API-Changes">Prefix Seek API</a>를 사용하려 했지만, JVM 버전에서는 아직 미지원.

  현재 결정은 <a target="_blank" href="https://github.com/facebook/rocksdb/wiki/Column-Families">Column Families</a> 사용.
  <br/><br/>

  <h3>RocksDB - Column Families</h3>
  <hr/>

  * RocksDB 3.0 부터 지원
  * logically DB 분리 가능
  * {cf1, key1, value1}, {cf1, key2, value2} ...
  * add / drop column families 속도 빠름

  * ColumnFamilyDescriptor --> Column Family Name & Column Family Option
  * ColumnFamilyHandle --> Column Family의 Open File Descriptor 역할
  <br/><br/>


  <h3>RocksDB - Column Families APIs</h3>
  <hr/>

  * DB::ListColumnFamilies(const DBOptions& db_options, const std::string& name, std::vector<std::string>* column_families)
  <br/> --> 모든 Column Families list

  * DB::CreateColumnFamily(const ColumnFamilyOptions& options, const std::string& column_family_name, ColumnFamilyHandle** handle)
  <br/> --> 새로운 Column Family 생성

  * DropColumnFamily(ColumnFamilyHandle* column_family)
  <br/> --> 기존 Column Family 삭제
  <br/><br/>


  <h3>db open with column families</h3>
  <hr/>

  {% highlight text %}
  private val columnFamilyDescriptors = Arrays.asList(
    new ColumnFamilyDescriptor(RocksDB.DEFAULT_COLUMN_FAMILY, new ColumnFamilyOptions())
  )
  private val columnFamilyHandles = new ArrayList[ColumnFamilyHandle]()
  private val db = RocksDB.open(new DBOptions(), path.getAbsolutePath, columnFamilyDescriptors, columnFamilyHandles)
  {% endhighlight %}
  <br/><br/>


  <h3>create column family</h3>
  <hr/>

  {% highlight text %}
  val columnFamilyHandle = db.createColumnFamily(
    new ColumnFamilyDescriptor("new column family".getBytes(),
    new ColumnFamilyOptions())
  )
  columnFamilyHandles.add(columnFamilyHandle)
  {% endhighlight %}
  <br/><br/>


  <h3>list column families</h3>
  <hr/>

  {% highlight text %}
  val columnFamilyNames = RocksDB.listColumnFamilies(options, path.getAbsolutePath)
  {% endhighlight %}
  <br/><br/>


  <h3>drop column family</h3>
  <hr/>

  {% highlight text %}
  db.dropColumnFamily(columnFamilyHandles.get(index))
  {% endhighlight %}
  <br/><br/>


  <h3>get all keys of column family</h3>
  <hr/>

  {% highlight text %}
  val keys = new ArrayList[String]
  val cfIterator = db.newIterator(cf)
  cfIterator.seekToFirst()

  while(cfIterator.isValid) {
    keys.add(new String(cfIterator.key()))
    cfIterator.next()
  }
  {% endhighlight %}
  <br/><br/>
