---
title: Hyper-V 可扩展交换机扩展的 INF 要求
description: Hyper-V 可扩展交换机扩展的 INF 要求
ms.assetid: 378F619A-C799-4330-A388-9955A67251F8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74230af31314fd6d9b3fd12f9959aaa80bab6b7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385098"
---
# <a name="inf-requirements-for-hyper-v-extensible-switch-extensions"></a>Hyper-V 可扩展交换机扩展的 INF 要求


NDIS 筛选器驱动程序作为开发的 HYPER-V 可扩展交换机扩展。 因此，扩展的 INF 要求基于所有 NDIS 筛选器驱动程序的 INF 要求。 在创建可扩展交换机扩展的 INF 文件时，您应将 INF 设置用于修改或监视筛选器驱动程序。 有关这些设置的详细信息，请参阅[筛选器驱动程序的 INF 文件设置](inf-file-settings-for-filter-drivers.md)。

此外，必须遵循这些准则以可扩展的交换机扩展的 INF 文件：

- 必须修改筛选器驱动程序作为安装的可扩展交换机扩展。

  修改筛选器驱动程序的 INF 要求的详细信息，请参阅[配置修改筛选器驱动程序 INF 文件](configuring-an-inf-file-for-a-modifying-filter-driver.md)。

  **请注意**的筛选器类的扩展**ms\_切换\_捕获**可以执行监视的筛选器驱动程序相同的任务。 有关详细信息，请参阅[类型的筛选器驱动程序](types-of-filter-drivers.md)。

     

- **FilterMediaTypes**筛选器 INF 文件中的条目定义的驱动程序绑定到其他驱动程序和接口。 **FilterMediaTypes**可扩展交换机扩展的条目必须包含**vmnetextension**值。 此值指定到可扩展的交换机扩展微型端口适配器的绑定。

  **FilterMediaTypes**条目允许媒体类型指定的以逗号分隔列表。 这允许要绑定到物理接口或可扩展交换机接口的扩展。

  下面的示例演示**FilterMediaTypes**条目以允许要绑定到物理以太网网络适配器或可扩展交换机虚拟网络适配器的扩展。

  ```INF
  HKR, Ndi\Interfaces, FilterMediaTypes, , "ethernet, vmnetextension"
  ```

  如果**FilterMediaTypes**条目仅指定**vmnetextension**值，该扩展将仅绑定到系统上的所有可扩展交换机的驱动程序堆栈。

  如果**FilterMediaTypes**项指定了**vmnetextension**作为其他媒体类型，该扩展可以确定是否绑定内可扩展交换机驱动程序堆栈通过调用[ **NdisFGetOptionalSwitchHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfgetoptionalswitchhandlers)。 如果该函数将返回 NDIS\_状态\_内扩展驱动程序堆栈绑定成功，该扩展。 如果该函数将返回 NDIS\_状态\_不\_支持，扩展绑定内不同的物理网络接口的驱动程序堆栈。

  有关详细信息**FilterMediaTypes**条目，请参阅[中间驱动程序 UpperRange 和 LowerRange INF 文件条目](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)。

- **FilterClass**值 INF 文件中的扩展插件确定筛选器的堆栈中的顺序。 **FilterClass**该项必须包含以下表中的值之一。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">FilterClass 值</th>
  <th align="left">描述</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><strong>ms_switch_capture</strong></p></td>
  <td align="left"><p>此类的扩展监视数据包流量。 但是，扩展此类不能应用端口策略或更改某个数据包的目标端口。</p>
  <p>有关此类扩展的详细信息，请参阅<a href="capturing-extensions.md" data-raw-source="[Capturing Extensions](capturing-extensions.md)">捕获扩展</a>。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><strong>ms_switch_filter</strong></p></td>
  <td align="left"><p>此类的扩展筛选数据包流量，并强制实施通过可扩展交换机的数据包发送端口或交换机策略。 此类驱动程序还可以检查和删除基于策略设置每个数据包的目标端口。</p>
  <p>有关此类扩展的详细信息，请参阅<a href="filtering-extensions.md" data-raw-source="[Filtering Extensions](filtering-extensions.md)">筛选扩展</a>。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p><strong>ms_switch_forward</strong></p></td>
  <td align="left"><p>此类的扩展具有相同的功能作为<strong>ms_switch_filter</strong>类。 此类扩展可以还将数据包转发到其他可扩展交换机端口，以及插入数据包流量发往任何可扩展交换机端口。</p>
  <p>入口数据路径，扩展此类调用后<strong>ms_switch_filter</strong>的扩展类。 出口数据路径，此类扩展调用之前<strong>ms_switch_filter</strong>的扩展类。</p>
  <p>有关此类扩展的详细信息，请参阅<a href="forwarding-extensions.md" data-raw-source="[Forwarding Extensions](forwarding-extensions.md)">转发扩展</a>。</p>
  <div class="alert">
  <strong>请注意</strong>只有一个此类的扩展，允许在可扩展交换机驱动程序堆栈。
  </div>
  <div>
     
  </div></td>
  </tr>
  </tbody>
  </table>

     

当使用这些 INF 设置安装该扩展时，它将配置为将绑定到每个可扩展交换机实例。 但是，该绑定将被禁用，必须显式启用通过 PowerShell cmdlet。 此过程的详细信息，请参阅[启用的 HYPER-V 可扩展交换机扩展](enabling-hyper-v-extensibility-switch-extensions.md)。

 

 





