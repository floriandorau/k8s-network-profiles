# k8s-network-profiles

Simple deployment for testing Kubernetes [Network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/).

## Scenario

The diagram shows the test scenarion which is used to establish the network profiles. That are the only connections which should be allowed.

```mermaid
flowchart BT
    subgraph internet
        httpbin
    end
    subgraph Cluster        
        subgraph Namespace alpha            
            id1(httpbin-poller)-- GET /uuid every 30s -->httpbin
            id2(nginx-poller)
        end
        subgraph Namespace beta
            id2(nginx-poller)-- GET /index every 30s -->id4(nginx)
            id3(nginx-poller)-- GET /index every 30s -->id4(nginx)
        end
    end
```

Deployments are splitted into to two namespaces: `alpha` and `beta`.

## Network Policy Editor

To create Network Polices easily, you can use the following online editor: <https://editor.cilium.io/>.
