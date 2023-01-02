### K8s 检测须知
!!! warning "环境要求"
    - Helm 3.0

!!! warning "使用云原生 K8s 安全检测前，需在k8s集群上安装 tirvy-operator"
    ```shell
    # 1.添加 chart 仓库
    # 如果可以访问 github，可以使用 trivy 官方仓库
    helm repo add hummer https://aquasecurity.github.io/helm-charts/
    # 或
    # 如果访问 github 异常，使用国内仓库，使用是一样的
    helm repo add hummer https://registry.hummercloud.com/repository/charts
    
    # 2.更新仓库源
    helm repo update
    
    # 3.开始安装, 可以自定义应用名称和NameSpace, 注意 trivy.serverURL 的 IP 地址需要替换为 Trivy 实际的 IP 地址
    # 如果 hummerrisk 以主机方式运行，则 <hummerrisk-trivy-server-ip> 为主机 IP。
    # 如果 hummerrisk 在 k8s 上运行，则 <hummerrisk-trivy-server-ip> 和端口为节点 IP 和 NodePort 端口，若配置的有 ingress 则可配置域名

    helm install trivy-operator hummer/trivy-operator \
    --namespace trivy-system \
    --set trivy.mode="ClientServer" \
    --set trivy.serverURL="http://<hummerrisk-trivy-server-ip>:4975" \
    --set image.repository="registry.cn-beijing.aliyuncs.com/hummerrisk/trivy-operator" \
    --set trivy.ignoreUnfixed=true \
    --set trivy.repository="registry.cn-beijing.aliyuncs.com/hummerrisk/trivy" \
    --create-namespace

    # 4.检测operator是否启动成功
    kubectl get pod -A|grep trivy-operator
    trivy-system   trivy-operator-69f99f79c4-lvzvs           1/1     Running            0          118s
    ```

### K8s 添加校验

#### 1. k8s 账号添加校验

!!! question "添加校验"
    1. 确定部署 hummerrisk 的主机可以访问该 k8s 集群的 6443 端口，需要网络可达、端口可以通，如果不通可以检查防火墙;
    2. 确定提供的 k8s Token 有足够的权限，hummerrisk 会通过该 Token 调用 k8s apiserver 的 api
    3. k8s token 权限可以参考如下
    创建 ServiceAccount
    ```yaml
    cat <<EOF > hummer-sa.yaml
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: hummer
      namespace: kube-system
    EOF
    ```
    创建 clusterrolebinding
    ```yaml
    cat <<EOF > hummer-clusterrolebinding.yaml
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      name: hummer-user
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: cluster-admin
    subjects:
      - kind: ServiceAccount
        name: hummer
        namespace: kube-system
    EOF
    ```
    创建资源
    ```bash
    kubectl create -f ./hummer-sa.yaml
    kubectl create -f ./hummer-clusterrolebinding.yaml
    ```

#### 2. 足够权限获取 token
!!! question "获取 token"
    ```bash
    # 获取 token
    kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep hummer | awk '{print $1}') | grep token: | awk '{print $2}'
    ```
