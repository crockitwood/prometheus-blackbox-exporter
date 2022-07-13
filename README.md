# Prometheus Blackbox Exporter
源于Prometheus社区chart库, 主要修改servicemonitor模版和values文件,兼容老版本Prometheus operater方便批量配置域名。

 [原仓库chart地址](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-blackbox-exporter)

## 使用
主要修改以下位置
```
serviceMonitor:

  defaults:
    labels:
      # 此处和已安装的Prometheus配置有关
      release: prom
 
  # prometheus拉取时间间隔
  scrapeInterval: 12h

  # 需要监控的域名列表
  targets:
    - prometheus.io
```

## 安装

拉取项目,修改文件values.yaml后执行
```
helm install blackbox-exporter ./prometheus-blackbox-exporter
```


## grafana

导入[dashboard 13587 ](https://grafana.com/grafana/dashboards/13587)

![](https://grafana.com/api/dashboards/13587/images/9554/image)



证书过期告警表达式

```
# 如查出一个月内过期的域名证书
(probe_ssl_earliest_cert_expiry - time()) / 86400 / 30  < 1
```

