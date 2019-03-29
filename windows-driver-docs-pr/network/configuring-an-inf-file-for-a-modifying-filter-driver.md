---
title: 配置修改筛选器驱动程序的 INF 文件
description: 配置修改筛选器驱动程序的 INF 文件
ms.assetid: d9eac8f6-a560-41e5-ae71-3bd9d6714c3a
keywords:
- INF 文件 WDK 网络筛选器驱动程序
- 修改筛选器驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e20d6bb441d7afb1452eaf3bf5e0852e2b56d8ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567048"
---
# <a name="configuring-an-inf-file-for-a-modifying-filter-driver"></a>配置修改筛选器驱动程序的 INF 文件





NDIS 筛选器驱动程序安装的以下问题是与修改筛选器驱动程序相关联。 若要创建您自己修改筛选器驱动程序 INF 文件，您可以改写[示例 NDIS 6.0 筛选器驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=618052)。

-   设置**类**INF 文件进入**NetService** INF 文件中。 下面的示例演示一个示例**类**INF 文件项。
    ```INF
    Class = NetService
    ```

-   *DDInstall*部分中的筛选器驱动程序 INF 文件必须具有**特征**条目。 下面的示例演示如何应定义**特征**筛选器 INF 文件中的条目。

    ```INF
    Characteristics=0x40000
    ```

    而 0x40000 可值，表示 NCF\_LW\_设置筛选器 （而 0x40000 可）。 筛选器驱动程序不能设置 NCF\_筛选器 (0x400) 标志。 值 NCF\_ *Xxx*中定义标志*Netcfgx.h*。 详细了解 NCF\_ *Xxx*标记，请参阅[DDInstall 网络 INF 文件中的部分](ddinstall-section-in-a-network-inf-file.md)。

-   设置**NetCfgInstanceId**在 INF 文件中，如以下示例所示的 INF 文件条目。

    ```INF
    NetCfgInstanceId="{5cbf81bd-5055-47cd-9055-a76b2b4e3697}"
    ```

    可以使用*Uuidgen.exe*工具创建的 GUID **NetCfgInstanceId**条目。

-   *DDInstall*部分中的筛选器驱动程序的 INF 文件必须包括**Addreg**指令**Ndi**密钥。 INF 文件必须指定**服务**下的条目**Ndi**密钥。 **ServiceBinary**中的条目*服务安装*INF 文件的部分指定的筛选器驱动程序二进制文件的路径。 有关详细信息，请参阅[添加服务的相关值到 Ndi 密钥](adding-service-related-values-to-the-ndi-key.md)并[DDInstall.Services 网络 INF 文件中的部分](ddinstall-services-section-in-a-network-inf-file.md)。

-   *DDInstall*部分中的筛选器驱动程序 INF 文件必须具有**FilterType**并**FilterRunType**条目。 若要指定修改筛选器，定义**FilterType**在 INF 文件中，如以下示例所示的条目。

    ```INF
    HKR, Ndi,FilterType,0x00010001 ,0x00000002
    ```

    **FilterType**值 0x00000002 指示筛选器是修改筛选器。

-   定义**FilterRunType**在 INF 文件中，如以下示例所示的条目。

    ```INF
    HKR, Ndi,FilterRunType,0x00010001 ,0x00000001
    ```

    在前面的示例 0x00000001 值指示筛选器模块，是必需的。 若要安装可选的筛选器模块，请设置**FilterRunType** 0x00000002 的条目。 有关详细信息，请参阅[必需筛选器驱动程序](mandatory-filter-drivers.md)。

-   下面的示例演示如何修改筛选器驱动程序 INF 文件指定的服务的名称。

    ```INF
    HKR, Ndi,Service,,"NdisLwf"
    ```

    在此示例中，NdisLwf 是服务的驱动程序的名称，因为它将被报告到 NDIS。 请注意，筛选器驱动程序的服务的名称可能不同于驱动程序二进制文件的名称，但它们通常是相同的。

-   下面的示例演示如何筛选器 INF 文件引用的筛选器驱动程序的服务名称时将添加该服务。
    ```INF
    [Install.Services]
    AddService=NdisLwf,,NdisLwf_Service_Inst;, common.EventLog 

    [NdisLwf_Service_Inst]
    DisplayName     = %NdisLwf_Desc%
    ServiceType     = 1 ;SERVICE_KERNEL_DRIVER
    StartType       = 1 ;SERVICE_SYSTEM_START
    ErrorControl    = 1 ;SERVICE_ERROR_NORMAL
    ServiceBinary   = %12%\ndislwf.sys
    LoadOrderGroup  = NDIS
    Description     = %NdisLwf_Desc%
    AddReg          = Common.Params.reg
    ```

-   筛选器 INF 文件必须至少指定的筛选器的主服务名称**CoServices**属性，如以下示例所示。

    ```INF
    HKR, Ndi,CoServices,0x00010000,"NdisLwf"
    ```

    有关详细信息**CoServices**属性，请参阅[添加服务的相关值到 Ndi 密钥](adding-service-related-values-to-the-ndi-key.md)。

-   **FilterClass**值 INF 文件中的筛选器驱动程序确定的筛选器堆栈中的顺序。 筛选器驱动程序必须定义**FilterClass**密钥。 驱动程序的类可以是下表中的值之一。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">ReplTest1</th>
    <th align="left">描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>计划程序</p></td>
    <td align="left"><p>数据包计划程序筛选器服务。 此类筛选器驱动程序是可以存在上述加密类筛选器驱动程序堆栈中的最高级别的驱动程序。 数据包计划程序检测到的服务质量 (QoS 信号组件和计划程序) 提供给数据包的 802.1p 优先级分类将这两种数据包级别发送到基础驱动程序根据它们的优先级别。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>加密</p></td>
    <td align="left"><p>计划程序和压缩类筛选器之间存在加密类筛选器驱动程序。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>压缩</p></td>
    <td align="left"><p>加密与 vpn 类筛选器之间存在压缩类筛选器驱动程序。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>vpn</p></td>
    <td align="left"><p>压缩和加载平衡筛选器驱动程序之间存在 VPN 类筛选器驱动程序。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>loadbalance</p></td>
    <td align="left"><p>负载平衡的筛选器服务。 数据包计划和故障转移的驱动程序之间存在此类筛选器驱动程序。 负载均衡筛选器服务通过对其组的基础的微型端口适配器将工作负载平衡数据包传输其工作的负荷。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>故障转移</p></td>
    <td align="left"><p>筛选器的故障转移服务。 负载平衡和诊断驱动程序之间存在此类筛选器驱动程序。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>诊断</p></td>
    <td align="left"><p>诊断的筛选器驱动程序存在以下故障转移在堆栈中的驱动程序。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>自定义</p></td>
    <td align="left"><p>自定义类中的筛选器驱动程序存在以下诊断驱动程序。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>provider_address</p></td>
    <td align="left"><p>提供程序地址筛选器驱动程序存在下面的框中的 HYPER-V 网络虚拟化 ms_wnv 筛选器，对提供程序地址 (PA) 数据包。</p></td>
    </tr>
    </tbody>
    </table>




**请注意**特定类的多个筛选器驱动程序可以修改筛选器驱动程序的分层堆栈中存在。 例如，修改的筛选器驱动程序的两个**FilterClass** "计划程序"可同时存在堆栈中。 下面安装具有早期安装的时间戳的筛选器驱动程序 (即，更接近于微型端口适配器) 使用更高版本的时间戳的筛选器驱动程序。 但是，与同一类的多个筛选器驱动程序的顺序是完全相同的同一台计算机上的不同的微型端口适配器通过。



下面的示例演示一个示例**FilterClass** 。

```INF
HKR, Ndi,FilterClass,, compression
```


- 仅 HYPER-V 交换机扩展筛选器驱动程序中都有效 HYPER-V 可扩展交换机。 下表中，HYPER-V 可扩展交换机筛选器驱动程序必须定义 FilterClass 密钥的值之一。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">ReplTest1</th>
  <th align="left">描述</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p>ms_switch_capture</p></td>
  <td align="left"><p>从开始 NDIS 6.30，捕获的 HYPER-V 可扩展交换机驱动程序堆栈中的驱动程序监视器数据包流量。 下堆栈中的自定义驱动程序不存在此类筛选器驱动程序。</p>
  <p>有关此类驱动程序的详细信息，请参阅<a href="capturing-extensions.md" data-raw-source="[Capturing Extensions](capturing-extensions.md)">捕获扩展</a>。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p>ms_switch_filter</p></td>
  <td align="left"><p>使用 NDIS 6.30 启动、 筛选驱动程序筛选数据包流量和强制执行端口或切换数据包传递通过可扩展交换机驱动程序堆栈的策略。 此类筛选器驱动程序存在如下<strong>ms_switch_capture</strong>堆栈中的驱动程序。</p>
  <p>有关此类驱动程序的详细信息，请参阅<a href="filtering-extensions.md" data-raw-source="[Filtering Extensions](filtering-extensions.md)">筛选扩展</a>。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p>ms_switch_forward</p></td>
  <td align="left"><p>从 NDIS 6.30 开始，转发驱动程序筛选器执行相同的函数作为筛选驱动程序。 转发驱动程序还将数据包从可扩展交换机转发端口。 此类筛选器驱动程序存在如下<strong>ms_switch_filter</strong>堆栈中的驱动程序。</p>
  <p>有关此类驱动程序的详细信息，请参阅<a href="forwarding-extensions.md" data-raw-source="[Forwarding Extensions](forwarding-extensions.md)">转发扩展</a>。</p></td>
  </tr>
  </tbody>
  </table>



- 必须修改的筛选器驱动程序 INF 文件，以控制驱动程序绑定中定义了以下项。

  ```INF
  HKR, Ndi\Interfaces,UpperRange,,"noupper"
  HKR, Ndi\Interfaces,LowerRange,,"nolower"
  HKR, Ndi\Interfaces, FilterMediaTypes,,"ethernet"
  ```

  有关控制驱动程序绑定的详细信息，请参阅[指定筛选器驱动程序绑定关系](specifying-filter-driver-binding-relationships.md)。

- 修改的筛选器 INF 文件应指定驱动程序和参数，与特定适配器相关联的常见参数定义。 下面的示例演示一些常见的参数定义。
  ```INF
  [Common.Params.reg]

  HKR, FilterDriverParams\DriverParam,  ParamDesc, , "Driverparam for lwf"
  HKR, FilterDriverParams\DriverParam,  default, , "5"
  HKR, FilterDriverParams\DriverParam,  type,  , "int"

  HKR, FilterAdapterParams\AdapterParam,  ParamDesc, , "Adapterparam for lwf"
  HKR, FilterAdapterParams\AdapterParam,  default, , "10"
  HKR, FilterAdapterParams\AdapterParam,  type,  , "int"
  ```









