###spark写入elasticsearch

引入依赖

```
        <dependency>
            <groupId>org.elasticsearch</groupId>
            <artifactId>elasticsearch-hadoop</artifactId>
            <version>2.2.0-m1</version>
        </dependency>
        <dependency>
            <groupId>org.elasticsearch</groupId>
            <artifactId>elasticsearch</artifactId>
            <version>2.0.0</version>
        </dependency>
	

```

代码部分

```
JavaEsSpark.saveJsonToEs(stringJavaRDD,"iis/iis",new HashMap<String, String>(){{put("es.nodes","192.168.252.41");put("es.index.auto.create","true");}});

```