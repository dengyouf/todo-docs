# kubernetes服务暴露

## IngressNginx

Ingress Controller可以为Kubernertes集群外部用户访问集群内部Pod提供代理服务
- 提供全局访问代理
- 访问流程
  - user -> ingress controller -> service -> pod

![](../images/ingress-nginx01.png)

