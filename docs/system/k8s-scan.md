!!! warning "K8s 检测须知"

!!! info "使用云原生 K8s 安全检测前，需在k8s集群上安装 tirvy-operator"

```shell
# 1.添加 chart 仓库
helm repo add hummer https://registry.hummercloud.com/repository/charts

# 2.更新仓库源
helm repo update

# 3.开始安装, 可以自定义应用名称和NameSpace
helm install trivy-operator hummer/trivy-operator \
 --namespace trivy-system \
 --set="image.repository=registry.cn-beijing.aliyuncs.com/hummerrisk/trivy-operator" \
 --create-namespace --set="trivy.ignoreUnfixed=true"

# 4.检测operator是否启动成功
kubectl get pod -A|grep trivy-operator
trivy-system   trivy-operator-69f99f79c4-lvzvs           1/1     Running            0          118s
```
