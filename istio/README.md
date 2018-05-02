```
oc adm policy add-scc-to-user anyuid -z istio-ingress-service-account -n istio-system

oc adm policy add-scc-to-user anyuid -z istio-grafana-service-account -n istio-system

oc adm policy add-scc-to-user anyuid -z istio-prometheus-service-account -n istio-system

curl -L https://git.io/getLatestIstio | sh -

cd istio-0.7.1/

oc create -f install/kubernetes/istio.yaml

oc project istio-system

oc get pods
istio-ca-2267585963-2hmfq        1/1       Running   0          1m
istio-ingress-3271581819-xcgmb   1/1       Running   0          2m
istio-mixer-3525126435-wnv2c     3/3       Running   0          13m
istio-pilot-1128596656-tzlxw     2/2       Running   0          2m


oc get svc
NAME            CLUSTER-IP       EXTERNAL-IP                     PORT(S)                                                             AGE
istio-ingress   172.30.90.231    172.29.252.237,172.29.252.237   80:31776/TCP,443:31241/TCP                                          5m
istio-mixer     172.30.158.157   <none>                          9091/TCP,15004/TCP,9093/TCP,9094/TCP,9102/TCP,9125/UDP,42422/TCP    17m
istio-pilot     172.30.107.192   <none>                          15003/TCP,15005/TCP,15007/TCP,15010/TCP,8080/TCP,9093/TCP,443/TCP   6m
```

# Install Istio Addons
```
oc adm policy add-scc-to-user anyuid -z prometheus -n istio-system
oc adm policy add-scc-to-user privileged -z prometheus -n istio-system
oc adm policy add-scc-to-user privileged -z grafana -n istio-system
oc adm policy add-scc-to-user anyuid -z grafana -n istio-system
oc create -f install/kubernetes/addons/prometheus.yaml
oc create -f install/kubernetes/addons/grafana.yaml
oc create -f install/kubernetes/addons/servicegraph.yaml
oc create -f install/kubernetes/addons/zipkin.yaml
oc expose svc grafana
oc expose svc servicegraph
oc expose svc zipkin
SERVICEGRAPH=$(oc get route servicegraph -o jsonpath='{.spec.host}{"\n"}')/dotviz
GRAFANA=$(oc get route grafana -o jsonpath='{.spec.host}{"\n"}')
ZIPKIN=$(oc get route zipkin -o jsonpath='{.spec.host}{"\n"}')
```

oc get dc -o yaml | istioctl kube-inject -f - | oc apply -f -
