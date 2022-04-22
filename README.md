# k8s-network-profiles

Simple deployment for testing Kubernetes [Network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/).

## Scenario

The diagram shows the test scenarion which is used to establish the network profiles. That are the only connections which should be allowed.

```mermaid
flowchart TD
    subgraph internet
        httpbin
    end
    subgraph Namespace db
        mysql
    end
    subgraph Cluster        
        subgraph Namespace alpha            
            id1(httpbin-poller)-- GET /uuid every 30s -->httpbin
            id5(mysql-poller)-- GET /uuid every 30s -->mysql
            id2(nginx-poller)
        end
        subgraph Namespace beta
            id2(nginx-poller)-- GET /index every 30s -->id4(nginx)
            id3(nginx-poller)-- GET /index every 30s -->id4(nginx)
        end
    end
```

Deployments are splitted into to namespaces: `alpha`, `beta` and `db`.

## Network Policy Editor

To create Network Polices easily, you can use the following online editor: <https://editor.cilium.io/>.
