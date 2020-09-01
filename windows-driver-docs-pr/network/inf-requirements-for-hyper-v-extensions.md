---
title: Hyper-V 可扩展交换机扩展的 INF 要求
description: Hyper-V 可扩展交换机扩展的 INF 要求
ms.assetid: 378F619A-C799-4330-A388-9955A67251F8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8da2c212e6df9678d8e1bf15e39ed912f44fe2ec
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212391"
---
# <a name="inf-requirements-for-hyper-v-extensible-switch-extensions"></a>Hyper-V 可扩展交换机扩展的 INF 要求


Hyper-v 可扩展交换机扩展开发为 NDIS 筛选器驱动程序。 因此，扩展的 INF 要求基于所有 NDIS 筛选器驱动程序的 INF 要求。 为可扩展交换机扩展创建 INF 文件时，应使用 INF 设置来修改或监视筛选器驱动程序。 有关这些设置的详细信息，请参阅 [筛选器驱动程序的 INF 文件设置](inf-file-settings-for-filter-drivers.md)。

此外，必须遵循以下适用于可扩展交换机扩展的 INF 文件指南：

- 可扩展交换机扩展必须安装为修改筛选器驱动程序。

  有关修改筛选器驱动程序的 INF 要求的详细信息，请参阅 [配置修改筛选器驱动程序的 Inf 文件](configuring-an-inf-file-for-a-modifying-filter-driver.md)。

  **注意**  带有 **ms \_ 交换机 \_ 捕获** 筛选器类的扩展可以执行与监视筛选器驱动程序相同的任务。 有关详细信息，请参阅 [筛选器驱动程序的类型](types-of-filter-drivers.md)。

     

- 筛选器 INF 文件中的 **FilterMediaTypes** 条目定义驱动程序与其他驱动程序和接口的绑定。 可扩展交换机扩展的 **FilterMediaTypes** 条目必须包含 **vmnetextension** 值。 此值指定到可扩展交换机扩展微型端口适配器的绑定。

  **FilterMediaTypes**项允许指定以逗号分隔的媒体类型列表。 这允许将扩展绑定到物理接口或可扩展交换机接口。

  以下示例显示一个 **FilterMediaTypes** 条目，该条目允许将扩展绑定到物理以太网网络适配器或可扩展交换机虚拟网络适配器。

  ```INF
  HKR, Ndi\Interfaces, FilterMediaTypes, , "ethernet, vmnetextension"
  ```

  如果 **FilterMediaTypes** 条目仅指定 **vmnetextension** 值，则扩展将仅绑定到系统上所有可扩展交换机的驱动程序堆栈。

  如果 **FilterMediaTypes** 项指定了 **vmnetextension** 以及其他媒体类型，则该扩展可以通过调用 [**NdisFGetOptionalSwitchHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfgetoptionalswitchhandlers)来确定它是否绑定到可扩展交换机驱动程序堆栈中。 如果函数返回 NDIS \_ 状态 \_ 成功，则扩展将绑定到扩展驱动程序堆栈中。 如果该函数返回 \_ \_ 不受支持的 NDIS 状态，则 \_ 该扩展将绑定到不同物理网络接口的驱动程序堆栈中。

  有关 **FilterMediaTypes** 项的详细信息，请参阅 [中间驱动程序 UPPERRANGE 和 LowerRange INF 文件项](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)。

- 扩展 INF 文件中的 **FilterClass** 值决定了其在筛选器堆栈中的顺序。 **FilterClass**条目必须包含下表中的其中一个值。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">FilterClass 值</th>
  <th align="left">说明</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><strong>ms_switch_capture</strong></p></td>
  <td align="left"><p>此类的扩展会监视数据包流量。 但是，此类扩展不能应用端口策略或更改数据包的目标端口。</p>
  <p>有关此扩展类的详细信息，请参阅 <a href="capturing-extensions.md" data-raw-source="[Capturing Extensions](capturing-extensions.md)">捕获扩展</a>。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><strong>ms_switch_filter</strong></p></td>
  <td align="left"><p>此类的扩展可筛选数据包流量，并强制实施端口或交换机策略，以通过可扩展交换机进行数据包传送。 此类驱动程序还可以根据策略设置检查并删除每个数据包的目标端口。</p>
  <p>有关此类扩展的详细信息，请参阅 <a href="filtering-extensions.md" data-raw-source="[Filtering Extensions](filtering-extensions.md)">筛选扩展</a>。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p><strong>ms_switch_forward</strong></p></td>
  <td align="left"><p>此类的扩展具有与 <strong>ms_switch_filter</strong> 类相同的功能。 此类扩展还可以将数据包转发到其他可扩展交换机端口，并将数据包流量注入到任何可扩展交换机端口。</p>
  <p>在入口数据路径中，此扩展类在 <strong>ms_switch_filter</strong> 扩展的类后调用。 在出口数据路径上，将在扩展的 <strong>ms_switch_filter</strong> 类之前调用此类扩展。</p>
  <p>有关此类扩展的详细信息，请参阅 <a href="forwarding-extensions.md" data-raw-source="[Forwarding Extensions](forwarding-extensions.md)">转发扩展</a>。</p>
  <div class="alert">
  <strong>注意</strong>  可扩展交换机驱动程序堆栈中仅允许此类的一个扩展。
  </div>
  <div>
     
  </div></td>
  </tr>
  </tbody>
  </table>

     

如果随这些 INF 设置一起安装了扩展，则会将其配置为绑定到每个可扩展交换机实例。 但是，该绑定将处于禁用状态，并且必须通过 PowerShell cmdlet 显式启用。 有关此过程的详细信息，请参阅 [启用 Hyper-v 可扩展交换机扩展](enabling-hyper-v-extensibility-switch-extensions.md)。

 

