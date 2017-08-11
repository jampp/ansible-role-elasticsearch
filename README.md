# Ansible role for ElasticSearch

[![Build Status](https://travis-ci.org/torian/ansible-role-elasticsearch.svg)](https://travis-ci.org/torian/ansible-role-elasticsearch)

Ansible role to install [ElasticSearch](https://www.elastic.co/products/elasticsearch)
through the official repositories

## Supported Platforms

  * EL / Centos (6 / 7)
  * Debian (Jessie)
  * Ubuntu (Trusty / Xenial)
  * AMZ Linux

## Role Variables

The following role variables are defined in `defaults/main.yml`. For a
detailed explanation about them you can take a look at the file.

```
es_version: 5.5.0

es_cfg_cluster_name: elasticsearch
es_cfg_node_master:  'true'
es_cfg_node_data:    'true'
es_cfg_log_dir: /var/log/elasticsearch
es_cfg_path_data:
  - /var/lib/elasticsearch
 
es_config_default:
  cluster.name: {{es_cfg_cluster_name}}
  node.master:  {{es_cfg_node_master}}
  node.data:    {{es_cfg_node_data}}

  path.logs: {{es_cfg_log_dir}}
  path.data: "{{es_cfg_path_data}}"

es_config: "{{es_config_default}}"
```

### JVM settings

The defaults for the JVM config (`jvm.config`) are based on elasticsearch
defaults, and are defined through the variable `es_config_jvm_defaults`:

```
es_jvm_mem: 2g

es_config_jvm_defaults: |
  -Xms{{es_jvm_mem}}
  -Xmx{{es_jvm_mem}}
  -XX:+UseConcMarkSweepGC
  -XX:CMSInitiatingOccupancyFraction=75
  -XX:+UseCMSInitiatingOccupancyOnly
  -XX:+AlwaysPreTouch
  -server
  -Xss1m
  -Djava.awt.headless=true
  -Dfile.encoding=UTF-8
  -Djna.nosys=true
  -Djdk.io.permissionsUseCanonicalPath=true
  -Dio.netty.noUnsafe=true
  -Dio.netty.noKeySetOptimization=true
  -Dio.netty.recycler.maxCapacityPerThread=0
  -Dlog4j.shutdownHookEnabled=false
  -Dlog4j2.disable.jmx=true
  -Dlog4j.skipJansi=true
  -XX:+HeapDumpOnOutOfMemoryError

es_config_jvm: "{{es_config_jvm_defaults}}"
```

## Usage

FIXME

