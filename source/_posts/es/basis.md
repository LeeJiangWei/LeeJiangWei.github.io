---
title: Elasticsearch (ES) ����
date: 2022-08-13 16:30:00
categories:
  - Elasticsearch
index_img: /img/es.png
---

# Elasticsearch (ES) ����

## ES ��Ⱥ�ܹ�

### Cluster����Ⱥ��

Cluster ���Ǽ�Ⱥ����˼��

![cluster](https://s2.loli.net/2022/08/13/6hHw4IJTxZnyPYu.png)

+ Elasticsearch ��Ⱥ��һ�������ڵ���ɣ���ͨ���伯Ⱥ���ƽ��б�ʶ
+ ��ȡ��Ⱥ״̬��`GET /_cluster/state`

### Node���ڵ㣩

���� Elasticsearch ʵ����

+ һ����Ⱥ��һ������ node ���
+ �ڴ���������У�ÿ���ڵ㶼�ڵ����ĺ��ӻ������������

### Document���ĵ���

Elasticsearch ����������������С���ݵ�Ԫ��

+ �ĵ�ͨ�������ݵ� JSON ��ʾ��ʽ

### Index��������

�� Elasticsearch �У�index �� document �ļ��ϡ�

+ ÿ�� Index һ�������� documents ��ɣ�������Щ document ���Էֲ��ڲ�ͬ�� shard ֮��

���ϵ�����ݿ��������ͬ��ES �У�������ʾ�������

+ ���ʣ��ĵ��ļ���
+ ���ʣ�����һ���ĵ��Ĺ��̣���������һ���ĵ� ~= ����һ���ĵ�

### Shard����Ƭ��

Elasticsearch ��һ���ֲ�ʽ�������棬��� index ͨ������Ϊ�ֲ��ڶ���ڵ��ϵ� shard��

![index.png](https://s2.loli.net/2022/08/13/ZOYqxculhskjzWA.png)

���������͵ķ�Ƭ��Primary shard (����Ƭ) �� Replica shard (������Ƭ)��
ֻ������Ƭ���Խ����������󣬸���������Ƭ�������ṩ��ѯ����

+ ����Ƭ��
    + ÿ���ĵ����洢��һ�� Primary shard
    + �����ĵ�ʱ���������� Primary shard �ϱ���������Ȼ���ڴ˷�Ƭ�����и����ϣ�replica������������
    + �������԰���һ����������Ƭ
+ ������Ƭ��
    + ���ӹ���ת�ƣ��������Ƭ���ϣ����Խ�������Ƭ����Ϊ����Ƭ
    + ������ܣ�get �� search �������������Ƭ�򸱱���Ƭ����

![shard](https://s2.loli.net/2022/08/13/x3hX8GRBVnmskUf.png)

+ һ�� index ��һ���߼������ռ䣬��ӳ�䵽һ����������Ƭ�����ҿ��Ծ����������������Ƭ
+ ���������� index �йأ�������������Ⱥ��ÿ�� index �ķ�Ƭ�������Զ�������

��ȡ��Ϊ twitter �����������ã�`GET /twitter/_settings?pretty`


#### Index ����״��

�鿴��������״����`GET /_cat/indices/twitter`

+ ��ɫ����Ⱥ��δ��������һ������Ƭ
+ ��ɫ���ѷ�����������������δ��������һ��������������£��������Ƭ���ϣ����ݻ�ȫ����ʧ��
+ ��ɫ���������з�Ƭ
