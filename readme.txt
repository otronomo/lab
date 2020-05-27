[root@rhel_vbox01 prometheus]# cat prometheus.yml 
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus_master'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9090']
  - job_name: 'node_exporter_centos'
    scrape_interval: 5s
    static_configs:
      - targets: ['192.168.1.49:9100']
  - job_name: 'snmp'
    metrics_path: /snmp
    params:
      module: [if_mib]
    static_configs:
      - targets:
        - 192.168.1.50
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 192.168.1.50:9116  # SNMP exporter.
