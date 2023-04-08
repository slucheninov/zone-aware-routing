# Zone aware routing

Example locality Load Balancing.

## Running

```bash
# docker-compose up -d
```

Generation traffic

```bash
# while true; do curl -s localhost:8000; done
zone us-central1-a server 2
zone us-central1-a server 3
zone us-central1-a server 1
zone us-central1-a server 1
zone us-central1-a server 2
```

100% traffic to zone us-central1-a.

```bash
# curl -s localhost:9901/stats | grep gke-cluster | grep "zone" | grep -v "time"                                                                       ─╯
cluster.gke-cluster.lb_recalculate_zone_structures: 15
cluster.gke-cluster.lb_zone_cluster_too_small: 0
cluster.gke-cluster.lb_zone_no_capacity_left: 0
cluster.gke-cluster.lb_zone_number_differs: 0
cluster.gke-cluster.lb_zone_routing_all_directly: 682 <-- Sending all requests directly to the same zone
cluster.gke-cluster.lb_zone_routing_cross_zone: 0
cluster.gke-cluster.lb_zone_routing_sampled: 0
cluster.gke-cluster.zone.us-central1-a.us-central1-a.upstream_rq_200: 682 <---
cluster.gke-cluster.zone.us-central1-a.us-central1-a.upstream_rq_2xx: 682
cluster.gke-cluster.zone.us-central1-a.us-central1-a.upstream_rq_completed: 682
```
