---
title: ��� mapping
date: 2022-08-13 17:56:00
categories:
  - Elasticsearch
index_img: /img/es.png
---

# ��� mapping

ӳ�䣨mapping���������ݿ��е� Schema ���������ĵ����ܾ��е��ֶλ����ԡ�ÿ���ֶε��������ͣ����� Text��Keyword��Integer �� Date ���Լ� Lucene ����������ʹ洢��Щ�ֶεġ�

## ���ļ��ֶ�����

Elasticsearch ֧�����¼��ֶ����ͣ�

+ �ַ����� text��keyword
+ ������byte��short��integer��long
+ �������� float��double
+ �����ͣ� boolean
+ ���ڣ� date

������ֶ����ͱ��� geo_point��ip��nested �ȿ��������Ӵ��鿴��https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-types.html

�鿴������ӳ�䣺`GET twitter/_mapping`

## ��������

+ �����ڿ��ٵ�ȫ�ļ���
+ Elasticsearch �ĵ�ÿ���ֶζ��ᱻ���������ĳЩ�ֶβ���Ҫ֧�ֲ�ѯ��������ӳ�������� "index": false �����ٴ洢�ռ�ռ�ã���������д���ٶ�

���磺���µı�����Ҫ������������ url �ֶβ���Ҫ����������������ӳ��ʱ���԰����·�ʽ��������

```json
PUT news
{
    "settings": { 
        "number_of_shards": 5, 
        "number_of_replicas": 1
    },
    "mappings": { 
        "properties": { 
            "title": { 
                "type": "text", 
                "analyzer": "ik_max_word"
            },
            "url": {
                "type": "keyword", 
                "index": false
            }   
        }
    }
}
```

## �ĵ�ֵ

�� Elasticsearch �У�Doc Values ��һ����ʽ�洢�ṹ��

+ Doc Values Ĭ�϶������ֶ����ã����� text �� annotated_text �����ֶ�
+ Doc Values ��������ʱ�����ģ����ֶ�����ʱ��Elasticsearch Ϊ���ܹ����ټ���������ֶε�ֵ���뵹�������У�ͬʱ��Ҳ��洢���ֶε� Doc Values

Elasticsearch �е� Doc Values ����Ӧ�õ����³�����

+ ��һ���ֶν�������
+ ��һ���ֶν��оۺ�
+ ĳЩ���ˣ��������λ�ù���
+ ĳЩ���ֶ���صĽű�����
+ ʹ�� docvalue_fields ����������������ֶ�ֵ

ע���������������Ϊ ES Ϊ�˼��ٲ�ѯ������Ȳ��������ⴢ�淽ʽ��ͬ���͵��ֶο��Ա���Ч��ѹ�����档�������Ǵ��� JSON ԭ�ģ�

+ �����֪������ԶҲ�����ĳЩ�ֶν��оۺϡ��������ʹ�ýű������������ͨ�������ض��ֶε� Doc Values������������ʡ���̿ռ䣬Ҳ�������������ٶȡ�
+ Ҫ���� Doc Values�����ֶε�ӳ������ doc_values: false

```json
PUT my_index
{ 
    "mappings": { 
        "properties": { 
            "session_id": { 
                "type": "keyword", 
                "doc_values": false
            }
        }
    }
}
```

## ����

Ĭ������£��ֶ�ԭʼֵ�ᱻ�������ڲ�ѯ�����ǲ��ᱻ�洢��

+ ���ֶε�ӳ�� (mapping) ���� "store": true������ʹ����������������ֶΡ�
+ ͨ������£�����ĵ�����ʮ���Ӵ󣬶�һЩ�ֶ��ֻᾭ������ʹ�ã���ô�������ֶΣ��Ϳ�������Ϊ�����洢��Ȼ�����ʹ�� stored_fields ����������Щ�ֶΡ�
+ ���磬�������ĵ��������⡢ʱ���һ���ܴ�������ֶΣ������ֻ��Ҫ�������⡢ʱ���ֶΣ�û��Ҫ�Ӻܴ�� _source ԭ���н�������Щ�ֶΡ�

## ԭ��

+ _source �ֶΰ�������ʱ���͵�ԭʼ JSON �ĵ�������ͨ�����ã�����ԭ���ֶΣ�����ֻ�洢�ض��ֶΡ�
+ _source �ֶλᵼ��ռ�ø���Ĵ洢�ռ䡣���ҵ���ϲ���Ҫ�洢ԭʼ�ĵ������԰����·�ʽ��������
+ ���� _source �ᵼ�¸��¡��ؽ�������ժҪ���ܲ����ã������������á����ǽ�ʡ�洢�ռ䣬����ͨ���޸��������� index.codec ���ѹ��Ч�ʡ�