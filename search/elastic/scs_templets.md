###scs templets
```
{
  "order": 2,
  "template": "scs_*",	
  "settings": {
    "index": {
      "number_of_replicas": "1",
      "number_of_shards": "5"
    }
  },
  "mappings": {
    "scs": {
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
        },
        "ex":{
         "type": "string",
          "index" : "not_analyzed"
        }
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
