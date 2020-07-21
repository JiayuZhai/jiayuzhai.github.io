---
layout: post
title: Elastic Search
---
关于Es的例子
## ES and kibana
Elastic search: 提供搜索
Kibana: 提供ES的UI

## Mapping example
```
PUT /address_reality/
{
  "mappings": {
    "properties": {
      "province": {
        "type": "keyword"
      },
      "city": {
        "type": "keyword"
      },
      "district": {
        "type": "keyword"
      },
      "street": {
        "type": "keyword"
      },
      "town": {
        "type": "keyword"
      },
      "village": {
        "type": "keyword"
      },
      "road": {
        "type": "keyword"
      },
      "text": {
        "type": "text",
        "analyzer": "standard"
      }
    }
  }
}
```
## Insert Example
```
POST /address_reality/_bulk
{ "index": { "_index": "address_reality", "_id" : "hash of the record"}}
{ "province":    "北京市","city":    "北京市" ,"district":    "朝阳区" ,"street":    "望京街道" ,"town":    "" ,"village":    "" ,"road":    "" ,"text":    "望京SOHOT2C2107"}
```
## Query Example
```
GET /address_reality/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "province": "云南省"
          }
        },
        {
          "match": {
            "city": "大理白族自治州"
          }
        },
        {
          "match": {
            "district": "祥云县"
          }
        },
        {
          "match": {
            "street": ""
          }
        },
        {
          "bool": {
            "should": [
              {
                "match": {
                  "town": ""
                }
              },
              {
                "match": {
                  "village": ""
                }
              },
              {
                "match": {
                  "road": "阁佛珠环城北街"
                }
              },
              {
                "match": {
                  "text": {
                    "query": "",
                    "analyzer": "standard",
                    "minimum_should_match": "50%"
                  }
                }
              }
            ]
          }
        }
      ]
    }
  }
}
```