###日志mapping

```
{
  "settings": {
    "index": {
      "number_of_replicas": "1",
      "number_of_shards": "7"
    }
  },
  "mappings": {
    "scs": {
      "_all": {
        "enabled": false
      },
      "_ttl" : {          "enabled" : true,          "default" : "15d"	  },
      "properties": {
        "rip": {
          "type": "string",
          "index" : "not_analyzed"
        },
        "time": {
          "type": "long"
        },
        "host": {
          "type": "string",
          "index" : "not_analyzed"
        },
        "created": {
          "type": "long"
        },
        "code": {
          "type": "long"
        },
        "cost": {
          "type": "long"
        },
        "all": {
          "type": "string"
        },
        "ip": {
          "type": "string",
          "index" : "not_analyzed"
        }
      }
    }
  }
}
```
###trace mapping
```

```

###RT mapping

```
{
  "settings": {
    "index": {
      "number_of_replicas": "1",
      "number_of_shards": "7"
    }
  },
  "mappings": {
    "rt": {
      "_all": {
        "enabled": false
      },
      "_ttl" : {          "enabled" : true,          "default" : "15d"	  },
      "properties": {
        "dept": {
          "type": "string",
          "index" : "not_analyzed"
        },
        "group": {
          "type": "string",
          "index" : "not_analyzed"
        },
        "key": {
          "type": "string",
          "index" : "not_analyzed"
        },
        "created": {
          "type": "long"
        },
        "tp999": {
          "type": "long"
        },
        "tp99": {
          "type": "long"
        },
        "tp90": {
          "type": "long"
        },
        "tp50": {
          "type": "long"
        },
        "call": {
          "type": "long"
        }
      }
    }        
  }
}
```
