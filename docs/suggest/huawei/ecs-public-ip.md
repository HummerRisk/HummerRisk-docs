# Huawei ECS 实例公网 IP 检测

### 1.检查项说明
!!! info ""
Huawei ECS 实例未直接绑定公网 IP，符合视为“合规”，否则属于“不合规”。该规则仅适用于 IPv4 协议。

### 2.处置方案
!!! info ""
    1. 前往华为云控制台，调整 ECS 实例公网访问控制。
    2. 通过弹性云服务器上解绑弹性公网 IP，实现弹性云服务器访问公网的合规性。

### 3.操作步骤
!!! info ""
    1. 使用华为云账号登录控制台。
    2. 通过导航菜单进入服务控制台。https://console.huaweicloud.com/vpc。
    3. 在管理控制台左上角单击，选择区域和项目。
    4. 在系统首页，选择“网络 > 弹性公网 IP”。
    5. 在“弹性公网 IP”界面，单击“弹性公网 IP” 操作按钮。
    6. 根据界面提示配置参数。

> 表1 参数说明

<table>
    <tr>
        <th  colspan="8">参数</th>
        <th  colspan="8">说明</th>
        <th  colspan="8">取值样例</th>
    </tr>
    <tr>
        <td  colspan="8">计费模式</td>
        <td  colspan="8">
            <span>计费模式分为以下两种：</span></br>
            <span>* 包年/包月。</span></br>
            <span>* 按需计费。</span>
        </td>
        <td  colspan="8">按需计费</td>
    </tr>
    <tr>
        <td  colspan="8">区域</td>
        <td  colspan="8">
            <span>* 不同区域的资源之间内网不互通。请选择靠近您客户的区域，可以降低网络时延、提高访问速度。购买EIP时所选择的区域即为EIP的归属地。</span></br>
            <span>* 说明：在“华北-乌兰察布一”区域购买的EIP的归属地为北京。</span>
        </td>
        <td  colspan="8">华东-上海一</td>
    </tr>
    <tr>
        <td  colspan="8">线路</td>
        <td  colspan="8">
            <span>* 全动态BGP：可以根据设定的寻路协议实时自动优化网络结构，以保持客户使用的网络持续稳定、高效。</span></br>
            <span>* 静态BGP：网络结构发生变化时，无法实时自动调整网络设置以保障用户体验。</span></br>
            <span>* 优选BGP：是特定方向的优质线路。使用BGP协议与多家主流运营商线路互联对接，建立直连中国内地的公网互联路径，提供中国-香港区域与中国内地间的低时延、高质量的网络互通。（该线路资源仅在“中国-香港”区域支持。）</span></br>
            <span>* 边缘线路：计费模式为按需计费时，该项可见。边缘线路是通过靠近用户和终端的网络边缘站点，实现区域内低时延高带宽的网络服务。边缘小站详细信息请参见 智能边缘小站。</span></br>
            <span>* 公网IP池：计费模式为按需计费时，该项可见。公网IP池是一种批量EIP开通到管理的专属解决方案。公网IP池为EIP分配全动态BGP线路，持续保证网络稳定、高效。公网IP池详细信息请参见公网IP池简介。</span>
        </td>
        <td  colspan="8">全动态BGP</td>
    </tr>
    <tr>
        <td  colspan="8">公网IP池</td>
        <td  colspan="8">
            <span>* 选择已购买的公网IP池。</span></br>
            <span>* 仅当EIP的计费模式为按需计费，线路为公网IP池时，该项可见。</span></br>
        </td>
        <td  colspan="8">eipPool-test</td>
    </tr>
    <tr>
        <td  colspan="8">公网带宽</td>
        <td  colspan="8">
            <span>选择按需计费时，需要选择公网带宽的计费方式。</span></br>
            <span>* 按带宽计费：指定带宽上限，按使用时间计费，与使用的流量无关。适用于流量较大或较稳定场景使用。</span></br>
            <span>* 按流量计费：指定带宽上限，按实际使用的出公网流量计费，与使用时间无关。适用于流量小或流量波动较大的场景。</span></br>
            <span>* 加入共享带宽：带宽可以加入多个弹性公网IP，带宽被多个弹性公网IP地址共用。适用于多业务流量错峰分布场景。</span></br>
        </td>
        <td  colspan="8">按带宽计费</td>
    </tr>
    <tr>
        <td  colspan="8">带宽大小</td>
        <td  colspan="8">
            <span>* 带宽大小，单位Mbit/s。</span></br>
        </td>
        <td  colspan="8">100</td>
    </tr>
    <tr>
        <td  colspan="8">IPv6转换</td>
        <td  colspan="8">
            <span>* 开启IPv6转换后，将提供IPv4和IPv6弹性公网IP地址，原有IPv4业务可以快速为IPv6用户提供访问能力。</span></br>
        </td>
        <td  colspan="8">开启</td>
    </tr>
    <tr>
        <td  colspan="8">弹性公网IP名称</td>
        <td  colspan="8">
            <span>* 弹性公网IP名称。</span>
        </td>
        <td  colspan="8">eip-test</td>
    </tr>
    <tr>
        <td  colspan="8">带宽名称</td>
        <td  colspan="8">
            <span>* 带宽名称。</span>
        </td>
        <td  colspan="8">bandwidth</td>
    </tr>
    <tr>
        <td  colspan="8">企业项目</td>
        <td  colspan="8">
            <span>* 申请弹性公网IP时，可以将弹性公网IP加入已启用的企业项目。</span></br>
            <span>* 企业项目管理提供了一种按企业项目管理云资源的方式，帮助您实现以企业项目为基本单元的资源及人员的统一管理，默认项目为default。</span>
        </td>
        <td  colspan="8">default</td>
    </tr>
    <tr>
        <td  colspan="8">高级配置</td>
        <td  colspan="8">
            <span>* 单击下拉箭头，可配置弹性公网IP的高级参数，包括带宽名称、标签等。</span>
        </td>
        <td  colspan="8">-</td>
    </tr>
    <tr>
        <td  colspan="8">标签</td>
        <td  colspan="8">
            <span>* 用于标识弹性公网IP地址。包括键和值。</span></br>
            <span>* 标签的命名规则请参考表2。</span>
        </td>
        <td  colspan="8">
            <span>键：Ipv4_key1</span></br> 
            <span>值：192.168.12.10</span>
        </td>
    </tr>
    <tr>
        <td  colspan="8">监控</td>
        <td  colspan="8">
            <span>* 用于开启弹性公网IP的基础监控。默认开启。</span></br>
            <span>* 开启基础监控后，用户可以通过云监控提供的管理控制台或API接口来检索弹性公网IP和带宽产生的监控指标和告警信息。</span>
        </td>
        <td  colspan="8">-</td>
    </tr>
    <tr>
        <td  colspan="8">购买时长</td>
        <td  colspan="8">
            <span>* 选择包年包月计费模式时，需要选择购买时长。</span>
        </td>
        <td  colspan="8">1个月</td>
    </tr>
    <tr>
        <td  colspan="8">购买量</td>
        <td  colspan="8">
            <span>* 弹性公网IP数量。</span></br>
            <span>* 仅在按需计费时可以选择弹性公网IP数量。</span>
        </td>
        <td  colspan="8">1</td>
    </tr>
</table>

> 表2 弹性公网IP地址标签命名规则

<table>
    <tr>
        <th  colspan="8">参数</th>
        <th  colspan="8">规则</th>
        <th  colspan="8">样例</th>
    </tr>
    <tr>
        <td  colspan="8">键</td>
        <td  colspan="8">
            <span>* 不能为空。对于同一弹性公网IP地址键值唯一。</span></br>
            <span>* 长度不超过36个字符。</span></br>
            <span>* 由英文字母、数字、下划线、中划线、中文字符组成。</span>
        </td>
        <td  colspan="8">Ipv4_key1</td>
    </tr>
    <tr>
        <td  colspan="8">值</td>
        <td  colspan="8">
            <span>* 长度不超过43个字符。</span></br>
            <span>* 由英文字母、数字、下划线、中划线、中文字符组成。</span>
        </td>
        <td  colspan="8">192.168.12.10</td>
    </tr>
</table>

### 4.说明
!!! warning ""
    * 对于按需计费的弹性公网 IP，当带宽类型选择“共享带宽”时，只能在“带宽名称”的下拉选项中选择已有的共享带宽加入。如果带宽名称不可选，说明您没有可用共享带宽，请先创建。
    * 独享带宽与共享带宽不支持直接互相转换，但针对按需计费的弹性公网 IP，您可以购买一个共享带宽，进行如下操作：
        * 将弹性公网 IP添加到共享带宽，则弹性公网IP使用共享带宽。
        * 将弹性公网 IP移出共享带宽，则弹性公网IP使用独享带宽。

### 4.帮助资源
!!! info ""
- https://support.huaweicloud.com/usermanual-vpc/zh-cn_topic_0013748738.html
