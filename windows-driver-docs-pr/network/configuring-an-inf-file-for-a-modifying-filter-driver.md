---
title: 配置修改筛选器驱动程序的 INF 文件
description: 配置修改筛选器驱动程序的 INF 文件
keywords:
- INF 文件 WDK 网络，筛选器驱动程序
- 修改筛选器驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b09997ae14f2a9b564952d4ec47a12c0bdcbd48
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834383"
---
# <a name="configuring-an-inf-file-for-a-modifying-filter-driver"></a>配置修改筛选器驱动程序的 INF 文件





以下 NDIS 筛选器驱动程序安装问题与修改筛选器驱动程序相关联。 若要创建自己的修改筛选器驱动程序 INF 文件，还可以调整 [示例 NDIS 6.0 筛选器驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=618052)。

-   将 INF 文件中的 **类** INF 文件项设置为 **空间** 。 下面的示例演示了 INF 文件的示例 **类** 条目。
    ```INF
    Class = NetService
    ```

-   筛选器驱动程序 INF 文件中的 *DDInstall* 部分必须包含 **特征** 条目。 下面的示例演示如何在筛选 INF 文件中定义 **特征** 条目。

    ```INF
    Characteristics=0x40000
    ```

    0x40000 值指示 \_ 已设置 NCF LW \_ 筛选器 (0x40000) 。 筛选器驱动程序不能将 NCF \_ 筛选器 (0x400) 标志。 NCF \_ *Xxx* 标志的值是在 *Netcfgx* 中定义的。 有关 NCF \_ *Xxx* 标志的详细信息，请参阅 [网络 INF 文件中的 DDInstall 部分](ddinstall-section-in-a-network-inf-file.md)。

-   在 INF 文件中设置 **NetCfgInstanceId** inf 文件条目，如以下示例中所示。

    ```INF
    NetCfgInstanceId="{5cbf81bd-5055-47cd-9055-a76b2b4e3697}"
    ```

    可以使用 *Uuidgen.exe* 工具为 **NETCFGINSTANCEID** 项创建 GUID。

-   筛选器驱动程序的 INF 文件的 *DDInstall* 部分必须包含 **Ndi** 项的 **Addreg** 指令。 INF 文件必须在 **Ndi** 项下指定 **服务** 项。 INF 文件的 "*服务安装*" 部分中的 **ServiceBinary** 条目指定筛选器驱动程序的二进制文件的路径。 有关详细信息，请参阅[将与服务相关的值添加到](adding-service-related-values-to-the-ndi-key.md)[网络 INF 文件中](ddinstall-services-section-in-a-network-inf-file.md)的 Ndi Key 和 DDInstall 部分。

-   筛选器驱动程序 INF 文件中的 *DDInstall* 部分必须包含 **FilterType** 和 **FilterRunType** 条目。 若要指定修改筛选器，请在 INF 文件中定义 **FilterType** 条目，如以下示例中所示。

    ```INF
    HKR, Ndi,FilterType,0x00010001 ,0x00000002
    ```

    **FilterType** 值0x00000002 表明筛选器是修改筛选器。

-   定义 INF 文件中的 **FilterRunType** 条目，如以下示例所示。

    ```INF
    HKR, Ndi,FilterRunType,0x00010001 ,0x00000001
    ```

    前面的示例中的0x00000001 值表明筛选器模块是必需的。 若要安装可选的筛选器模块，请将 **FilterRunType** 项设置为0x00000002。 有关详细信息，请参阅 [强制筛选器驱动程序](mandatory-filter-drivers.md)。

-   下面的示例演示修改筛选器驱动程序 INF 文件如何指定服务的名称。

    ```INF
    HKR, Ndi,Service,,"NdisLwf"
    ```

    在此示例中，NdisLwf 是驱动程序的服务名称，因为它会报告给 NDIS。 请注意，筛选器驱动程序的服务名称可以与驱动程序的二进制文件名称不同，但通常是相同的。

-   下面的示例演示筛选器 INF 文件在添加该服务时如何引用筛选器驱动程序的服务的名称。
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

-   筛选器 INF 文件必须至少为 **CoServices** 属性指定筛选器的主服务名称，如下面的示例所示。

    ```INF
    HKR, Ndi,CoServices,0x00010000,"NdisLwf"
    ```

    有关 **CoServices** 属性的详细信息，请参阅 [将服务相关值添加到 Ndi 键](adding-service-related-values-to-the-ndi-key.md)。

-   筛选器驱动程序的 INF 文件中的 **FilterClass** 值决定了其在筛选器堆栈中的顺序。 筛选器驱动程序必须定义 **FilterClass** 项。 驱动程序的类可以是下表中的值之一。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">“值”</th>
    <th align="left">描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>scheduler</p></td>
    <td align="left"><p>数据包计划筛选器服务。 此类筛选器驱动程序是最高级别的驱动程序，可在驱动程序堆栈中的加密类筛选器之上存在。 数据包计划程序通过服务质量 (QoS) 信号组件来检测指定给数据包的 802.1 p 优先级分类，计划程序根据其优先级向底层驱动程序发送这些数据包级别。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>加密</p></td>
    <td align="left"><p>在计划程序和压缩类筛选器之间存在加密类筛选器驱动程序。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>compression</p></td>
    <td align="left"><p>加密和 vpn 类筛选器之间存在压缩类筛选器驱动程序。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>VPN</p></td>
    <td align="left"><p>VPN 类筛选器驱动程序存在于压缩和负载平衡筛选器驱动程序之间。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>loadbalance</p></td>
    <td align="left"><p>负载平衡筛选器服务。 数据包计划和故障转移驱动程序之间存在此类筛选器驱动程序。 负载平衡筛选器服务通过将工作负荷分配到其一组基础微型端口适配器来平衡数据包传输的工作负荷。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>故障转移</p></td>
    <td align="left"><p>故障转移筛选器服务。 此类筛选器驱动程序存在于负载平衡和诊断驱动程序之间。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>诊断</p></td>
    <td align="left"><p>诊断筛选器驱动程序存在于堆栈中的故障转移驱动程序以下。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>自定义</p></td>
    <td align="left"><p>自定义类中的筛选器驱动程序位于诊断驱动程序以下。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>provider_address</p></td>
    <td align="left"><p>提供程序地址筛选器驱动程序在内置 Hyper-v 网络虚拟化 ms_wnv 筛选和操作提供程序地址 (PA) 数据包。</p></td>
    </tr>
    </tbody>
    </table>




**注意**  一个特定类的多个筛选器驱动程序可能存在于修改筛选器驱动程序的分层堆栈中。 例如， **FilterClass** "计划程序" 的两个修改筛选器驱动程序可以同时存在于堆栈中。 具有较早安装时间戳的筛选器驱动程序安装在下面 (即，更接近小型端口适配器) 筛选器驱动程序与更晚的时间戳。 但是，具有相同类的多个筛选器驱动程序的顺序在同一台计算机上的不同小型端口适配器上完全相同。



下面的示例演示了一个示例 **FilterClass** 。

```INF
HKR, Ndi,FilterClass,, compression
```


- Hyper-v 交换机扩展筛选器驱动程序只有 hyper-v 可扩展交换机中才有效。 Hyper-v 可扩展交换机筛选器驱动程序必须定义具有下表中的值之一的 FilterClass 键。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">“值”</th>
  <th align="left">描述</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p>ms_switch_capture</p></td>
  <td align="left"><p>从 NDIS 6.30 开始，捕获驱动程序监视 Hyper-v 可扩展交换机驱动程序堆栈中的数据包流量。 堆栈中的自定义驱动程序以下存在此类筛选器驱动程序。</p>
  <p>有关此类驱动程序的详细信息，请参阅 <a href="capturing-extensions.md" data-raw-source="[Capturing Extensions](capturing-extensions.md)">捕获扩展</a>。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p>ms_switch_filter</p></td>
  <td align="left"><p>从 NDIS 6.30 开始，筛选驱动程序将筛选数据包流量并强制通过可扩展交换机驱动程序堆栈进行数据包传递的端口或交换机策略。 此类筛选器驱动程序存在于堆栈 <strong>ms_switch_capture</strong> 驱动程序的下面。</p>
  <p>有关此类驱动程序的详细信息，请参阅 <a href="filtering-extensions.md" data-raw-source="[Filtering Extensions](filtering-extensions.md)">筛选扩展</a>。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p>ms_switch_forward</p></td>
  <td align="left"><p>从 NDIS 6.30 开始，转发驱动程序筛选器执行与筛选驱动程序相同的功能。 转发驱动程序还会在可扩展交换机端口之间转发数据包。 此类筛选器驱动程序存在于堆栈 <strong>ms_switch_filter</strong> 驱动程序的下面。</p>
  <p>有关此类驱动程序的详细信息，请参阅 <a href="forwarding-extensions.md" data-raw-source="[Forwarding Extensions](forwarding-extensions.md)">转发扩展</a>。</p></td>
  </tr>
  </tbody>
  </table>



- 必须在修改筛选器驱动程序 INF 文件中定义以下条目，以控制驱动程序绑定。

  ```INF
  HKR, Ndi\Interfaces,UpperRange,,"noupper"
  HKR, Ndi\Interfaces,LowerRange,,"nolower"
  HKR, Ndi\Interfaces, FilterMediaTypes,,"ethernet"
  ```

  有关控制驱动程序绑定的详细信息，请参阅 [指定筛选器驱动程序绑定关系](specifying-filter-driver-binding-relationships.md)。

- 修改筛选器 INF 文件应为驱动程序指定公用参数定义，并指定与特定适配器相关联的参数。 下面的示例演示一些常见参数定义。
  ```INF
  [Common.Params.reg]

  HKR, FilterDriverParams\DriverParam,  ParamDesc, , "Driverparam for lwf"
  HKR, FilterDriverParams\DriverParam,  default, , "5"
  HKR, FilterDriverParams\DriverParam,  type,  , "int"

  HKR, FilterAdapterParams\AdapterParam,  ParamDesc, , "Adapterparam for lwf"
  HKR, FilterAdapterParams\AdapterParam,  default, , "10"
  HKR, FilterAdapterParams\AdapterParam,  type,  , "int"
  ```









