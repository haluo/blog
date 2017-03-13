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
        },
        "ex":{
         "type": "string",
          "index" : "not_analyzed"
        }
      }
    }
  }
}
```
###iis mapping
```
{
  "settings": {
    "index": {
      "number_of_replicas": "1",
      "number_of_shards": "7"
    }
  },
  "mappings": {
    "iis": {
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

###RT mapping

```
{
  "settings": {
    "index": {
      "number_of_replicas": "1",
      "number_of_shards": "5"
    }
  },
  "mappings": {
    "rt": {
      "_all": {
        "enabled": false
      },
      "_ttl" : {          "enabled" : true,          "default" : "30d"	  },
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
          "type": "date"
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
##rt  meta
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
        "extype": {
          "type": "long"
        }
      }
    }        
  }
}
```
### app日志分析
```
{
  "settings": {
    "index": {
      "number_of_replicas": "1",
      "number_of_shards": "5"
    }
  },
  "mappings": {
    "log": {
      "_all": {
        "enabled": false
      },
      "_ttl" : {
          "enabled" : true,
          "default" : "20d"
      },
      "properties": {
        "dtime": {
          "type": "long"
        },
        "device": {
          "type": "string"
        },
        "url": {
          "type": "string",
          "fields": {
            "agg": { "type" : "string", "index": "not_analyzed" }
          }
        },
        "param": {
          "type": "string"
        },
        "data": {
          "properties": {
          	"syncstamp": {
          		"type": "long"
          	},
          	"useragent": {
          		"type": "string",
          		"index": "not_analyzed" 
          	},
          	"cityid": {
          		"type": "long"
          	},
          	"networkprovider": {
          		"type": "string",
          		"index": "not_analyzed" 
          	},
          	"reqtype": {
          		"type": "long"
          	},
          	"errortype" :{
          		"type": "long"
          	},
          	"errorsubtype" :{
          		"type": "long"
          	},
          	"network" :{
          		"type": "string",
          		"index": "not_analyzed" 
          	},
          	"retrytype" :{
          		"type": "long"
          	},
          	"channel" :{
          		"type": "string",
          		"index": "not_analyzed" 
          	},
          	"appid" :{
          		"type": "long"
          	},
          	"platform" :{
          		"type": "long"
          	},
          	"appversion" :{
          		"type": "string",
          		"index": "not_analyzed" 
          	},
          	"domain" :{
          		"type": "string",
          		"index": "not_analyzed" 
          	}
          }
        },
        "host": {
          "type": "string",
          "index": "not_analyzed" 
        },
        "api": {
          "type": "string",
          "index": "not_analyzed" 
        },
        "reqtype": {
          "type": "long"
        },
        "status": {
          "type": "long"
        },
        "appstime": {
          "type": "long"
        },
        "scsrtime": {
          "type": "long"
        },
        "scsstime": {
          "type": "long"
        },
        "pkrtime": {
          "type": "long"
        },
        "pkstime": {
          "type": "long"
        },
        "protocol": {
          "type": "string",
          "index": "not_analyzed" 
        }
      }
    }        
  }
}
```

```
{
  "settings": {
    "index": {
      "number_of_replicas": "1",
      "number_of_shards": "5"
    }
  },
  "mappings": {
    "log": {
      "_all": {
        "enabled": false
      },
      "_ttl" : {
          "enabled" : true,
          "default" : "30d"
      },
      "properties": {
        "sip": {
          "type": "string",
          "index" : "not_analyzed"
        },
        "dip": {
          "type": "string",
          "index" : "not_analyzed"
        },
        "module": {
          "type": "string",
          "index" : "not_analyzed"
        },
        "action": {
          "type": "string",
          "index" : "not_analyzed"
        },
        "time": {
          "format": "strict_date_optional_time||epoch_millis", 
          "type": "date"
        }
      }
    }        
  }
}
```