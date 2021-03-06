# 网络增强性能数据



**注意：此文档仅为性能基准的测试，测试通过UDP协议+小包/大包，带来的最大性能值。具体业务场景下的包量受到上层应用、通信协议等多种因素影响，请以实际的业务压测结果为准。**

## 网络性能测试指标

**包量** （常用单位: pps）: 每秒能处理的网络包的数量。是网络增强特性提升的核心指标。

**带宽** （常用单位: mb/s）：网络带宽是指一个固定的时间内（1秒），能通过的最大位数据。

**TCP\_RR** （常用单位: 次/秒）：测试同一个TCP连接中的多次TCP
request和response的响应效率，这种应用场景常常出现在数据库应用中。

**TCP\_CRR** （常用单位:
次/秒）：测试多个TCP连接中的request和response的响应效率，每个TCP请求、响应都建立一个新的TCP连接。最典型的应用是HTTP网页访问请求，每个请求响应都在一个单独的TCP连接中进行。

## 测试数据

### 测试环境

**测试机：**

镜像：CentOS 7.2 64位

规格：1）8核CPU 16G内存 2）16核CPU 32G内存

**辅助机：**

镜像：CentOS 7.2 64位

规格：8核CPU 16G内存 * 8台

### 测试1. 包量测试

采用UDP_STREAM，小包（1byte）测试。

![](/images/testdata/pps_compare.png)

* 网络增强能显著提升包量。UDP测试情况下，峰值包处理能力可达100万pps以上，是未开启网络增强情况下的3倍。
* UCloud的包量能力与规格大小无关。

### 测试2. 带宽测试

采用UDP_STREAM，大包（1400bytes）测试。

![](/images/testdata/bps_compare.png)

网络增强能显著提升带宽，但在出向测试时，达到了内网的最大带宽瓶颈（10G），因此无法进一步提升。

### 测试3. TCP_RR与TCP_CRR

![](/images/testdata/tcp_compare.png)

由于来回路径没有改变，单链只能走一个核和一个通道，是否开启网络增强并无差异。因此开启网络增强不能显著提升TCP_RR与TCP_CRR。
