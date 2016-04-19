###scs templets
```
{
  "order": 2,
  "template": "scs_*",
  "settings": {
    "index": {
      "number_of_shards": "5",
      "number_of_replicas": "1"
    }
  },
  "mappings": {
    "scs": {
      "_ttl": {
        "default": "30d",
        "enabled": true
      },
      "_all": {
        "enabled": false
      },
      "properties": {
        "all": {
          "type": "string"
        },
        "ncache": {
          "ignore_above": 256,
          "index": "not_analyzed",
          "type": "string"
        },
        "cache": {
          "ignore_above": 256,
          "index": "not_analyzed",
          "type": "string"
        },
        "code": {
          "type": "long"
        },
        "cost": {
          "type": "long"
        },
        "created": {
          "type": "long"
        },
        "ip": {
          "ignore_above": 256,
          "index": "not_analyzed",
          "type": "string"
        },
        "cip": {
          "ignore_above": 256,
          "index": "not_analyzed",
          "type": "string"
        },
        "ua": {
          "ignore_above": 256,
          "index": "not_analyzed",
          "type": "string"
        },
        "fip": {
          "ignore_above": 256,
          "index": "not_analyzed",
          "type": "string"
        },
        "url": {
          "index": "not_analyzed",
          "type": "string"
        },
        "scscost": {
          "type": "long"
        },
        "ex": {
          "ignore_above": 256,
          "index": "not_analyzed",
          "type": "string"
        },
        "bu": {
          "ignore_above": 256,
          "index": "not_analyzed",
          "type": "string"
        },
        "refer": {
          "ignore_above": 256,
          "index": "not_analyzed",
          "type": "string"
        },
        "rip": {
          "ignore_above": 256,
          "index": "not_analyzed",
          "type": "string"
        },
        "host": {
          "ignore_above": 256,
          "index": "not_analyzed",
          "type": "string"
        },
        "time": {
          "type": "long"
        }
      }
    }
  },
  "aliases": {}
}

```
###scs old
```
{
  "order": 2,
  "template": "scs_*",
  "settings": {},
  "mappings": {
    "scs": {
      "_ttl": {
        "enabled": true,
        "default": "15d"
      },
      "properties": {
        "rip": {
          "index": "not_analyzed",
          "type": "string"
        },
        "ex": {
          "index": "not_analyzed",
          "type": "string"
        },
        "time": {
          "type": "long"
        },
        "host": {
          "index": "not_analyzed",
          "type": "string"
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
          "index": "not_analyzed",
          "type": "string"
        }
      },
      "_all": {
        "enabled": false
      }
    }
  },
  "aliases": {}
}
```


###iis
```
{
  "order": 2,
  "template": "iis_*",	 	
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
      "_ttl" : {
          "enabled" : true,
          "default" : "15d"
      },
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
  },
  "aliases": {}
}

```
###app

```
{ 
  "order": 2,
  "template": "appmlog_*",
  "settings": {
    "index": {
      "number_of_replicas": "1",
      "number_of_shards": "7"
    }
  },
  "mappings": {
	 "log": {
      "_all": {
        "enabled": false
      },
      "_ttl" : {
          "enabled" : true,
          "default" : "50d"
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
  },
  "aliases": {}
}
```
