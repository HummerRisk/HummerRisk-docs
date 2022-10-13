### 云账号
> 云账号设置，主要用来记录云账号认证信息，保存检测参数，用于按检测规则检测云平台资源。

#### 1.云账号添加校验无效。
!!! question ""
    1. 云账号参数添加错误，存在空格等非法字符;
    2. 部署服务器时间、时区不准确;
    3. 云账号环境存在代理，网络不通。

#### 2.云账号某些区域信息获取不到。
!!! question ""
    云平台更新区域信息，HummerRisk 暂时未同步。

#### 3.云账号检测某些区域获取不到资源数据。
!!! question ""
    云平台更新区域信息，HummerRisk 暂时未同步。

### K8s 检测
#### 1.k8s 添加失败
!!! question ""
    1. 确定部署 hummerrisk 的主机可以访问该 k8s 集群的 6443 端口，需要网络可达、端口可以通，如果不通可以检查防火墙;
    2. 确定提供的 k8s Token 有足够的权限，hummerrisk 会通过该 Token 调用 k8s apiserver 的api
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
        name: hummer-user
        namespace: kube-system
    EOF
    ```
    创建资源
    ```bash
    kubectl create -f ./hummer-sa.yaml
    kubectl create -f ./hummer-clusterrolebinding.yaml
    # 获取 token
    kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep hummer | awk '{print $1}') | grep token: | awk '{print $2}'
    ```



### 镜像检测

#### 1.镜像检测一直"正在处理"的状态中。
!!! question ""
    1. 有可能有别的资源正在执行，等待队列中;
    2. 第一次执行速度较慢，因为第一次执行需要下载漏洞数据库（100MB左右），第二次之后速度将大幅度提升。

### 软件包检测

#### 1.软件包检测一直"正在处理"的状态中。
!!! question ""
    1. 有可能有别的资源正在执行，等待队列中;
    2. 第一次执行速度较慢，因为第一次执行需要下载漏洞数据库（110MB左右），第二次之后速度将大幅度提升。

### 页面报错
!!! question ""
    确定不是环境问题引起的，请联系我们进行反馈，我们将在第一时间处理。（微信群、邮件、github issues 等均可）
