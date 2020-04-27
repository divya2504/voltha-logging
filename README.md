# Logging

This chart implements a log aggregation framework built on elasticsearch within
kubernetes.

It requires persistent storage, and currently has default values for the
`local-provisioner` with storage on each k8s node.

Once these prereqs are satisfied, it can be run with:

    helm install -n logging voltha-logging

(NOTE: the name must be `logging` currently)

In development or testing scenarios where persistence isn't required, this command will load the logging chart without persistence:

    helm install --set elasticsearch.cluster.env.MINIMUM_MASTER_NODES="1" \
             --set elasticsearch.client.replicas=1 \
             --set elasticsearch.master.replicas=2 \
             --set elasticsearch.master.persistence.enabled=false \
             --set elasticsearch.data.replicas=1 \
             --set elasticsearch.data.persistence.enabled=false \
             -n logging voltha-logging --namespace voltha

## Current log sources

- Container logs from k8s with [fluentd-elasticsearch](https://github.com/helm/charts/tree/master/stable/fluentd-elasticsearch)

## Using Kibana

Visit: http://<k8s_node_hostname>:30601


#To start using Kibana:
you must create an index under Management > Index Patterns. Create one with a name of logstash*, then you can search for events in the Discover section.
