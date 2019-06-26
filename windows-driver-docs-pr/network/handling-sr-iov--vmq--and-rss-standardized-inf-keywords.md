---
title: 处理 SR-IOV、VMQ 和 RSS 标准化 INF 关键字
description: 处理 SR-IOV、VMQ 和 RSS 标准化 INF 关键字
ms.assetid: EF556563-4097-4388-A563-29FC891AC626
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 091d8b2fda2829dc24af30d0c6330e4ffb8b1d61
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381358"
---
# <a name="handling-sr-iov-vmq-and-rss-standardized-inf-keywords"></a>处理 SR-IOV、VMQ 和 RSS 标准化 INF 关键字


支持单根 I/O 虚拟化 (SR-IOV)，虚拟机队列 (VMQ) 和接收方缩放 (RSS) 的网络适配器可以按以下方式启用这些接口的使用：

-   单独或同时在可以启用 SR-IOV 和 VMQ。

-   启用 SR-IOV 或 VMQ 不能在网络适配器上启用 RSS。

操作系统通过以下方式启用 SR-IOV、 VMQ 或 RSS 接口的使用：

-   在网络适配器绑定到 TCP/IP 堆栈的操作系统启用 RSS 功能的使用。

-   在网络适配器绑定到 HYPER-V 可扩展交换机驱动程序堆栈，操作系统会启用 SR-IOV 或 VMQ 功能的使用。

    有关 HYPER-V 可扩展交换机的详细信息，请参阅[HYPER-V 可扩展交换机](hyper-v-extensible-switch.md)。

从 TCP/IP 堆栈和 HYPER-V 可扩展交换机驱动程序堆栈未绑定的网络适配器时，微型端口驱动程序是已暂停，然后重新初始化。 因此，不能为此类网络适配器，以自动切换 RSS、 VMQ 和 SR-IOV。

当调用 NDIS [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数，它报告其当前已启用的 SR-IOV、 VMQ 或 RSS 功能到 NDIS 之前微型端口驱动程序按照以下步骤：

1.  微型端口驱动程序读取 **\*SriovPreferred**关键字之前到 NDIS 报告其当前已启用的功能。

    如果的值 **\*SriovPreferred**关键字是一个，微型端口驱动程序配置的 SR-IOV 首选项。

2.  微型端口驱动程序读取 **\*RssOrVmqPreference**关键字之前到 NDIS 报告其当前已启用的功能。

    如果的值 **\*RssOrVmqPreference**关键字是一个，微型端口驱动程序配置为 VMQ 首选项。

    如果的值 **\*RssOrVmqPreference**关键字为零或关键字不存在，则为 RSS 首选项配置微型端口驱动程序。

3.  如果微型端口驱动程序配置为 SR-IOV 首选项，它必须读取 **\*SRIOV**关键字来确定是否在网络适配器上启用 SR-IOV。 如果关键字设置为 1，驱动程序将报告当前已启用的 SR-IOV 设置。

    微型端口驱动程序报告的 SR-IOV 设置的方式的详细信息，请参阅[确定的 SR-IOV 功能](determining-sr-iov-capabilities.md)。

    有关 SR-IOV 关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

    **请注意**  如果微型端口驱动程序配置为 SR-IOV 首选项，它必须读取任意 RSS 标准化关键字。 但是，该驱动程序必须读取 VMQ  **\*VMQVlanFiltering**标准化的关键字。 此关键字指定是否启用微型端口驱动程序通过媒体访问控制 (MAC) 标头中的虚拟 VLAN (VLAN) 标识符筛选网络数据包。 微型端口驱动程序报告此功能通过设置 NDIS\_接收\_筛选器\_MAC\_标头\_VLAN\_ID\_中的支持标志**SupportedMacHeaderFields**的成员[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。 有关详细信息 **\*VMQVlanFiltering**标准化的关键字，请参阅[VMQ 的标准化 INF 关键字](standardized-inf-keywords-for-vmq.md)。

     

4.  如果微型端口驱动程序配置为 VMQ 首选项，它必须读取 **\*VMQ**关键字来确定是否在网络适配器上启用 VMQ。 如果关键字设置为 1，驱动程序将报告当前已启用的 VMQ 设置。 微型端口驱动程序报告 VMQ 设置的方式的详细信息，请参阅[确定网络适配器的 VMQ 功能](determining-the-vmq-capabilities-of-a-network-adapter.md)。

    有关 VMQ 关键字的详细信息，请参阅[VMQ 的标准化 INF 关键字](standardized-inf-keywords-for-vmq.md)。

    **请注意**  如果微型端口驱动程序配置为 VMQ 首选项，它必须读取的 RSS 或 SR-IOV 任何标准化关键字。

     

5.  如果微型端口驱动程序配置为 RSS 首选项，它必须读取 **\*RSS**关键字来确定是否在网络适配器上启用了 RSS。 如果关键字设置为 1，驱动程序将报告当前已启用的 RSS 设置。 微型端口驱动程序报告 RSS 设置的方式的详细信息，请参阅[RSS 配置](rss-configuration.md)。

    有关 RSS 关键字的详细信息，请参阅[RSS 的标准化 INF 关键字](standardized-inf-keywords-for-rss.md)。

    **请注意**  如果微型端口驱动程序配置为 RSS 首选项，它必须读取的任何 VMQ 或 SR-IOV 标准化关键字。

     

下表描述了如何微型端口驱动程序确定要使正确的接口中的网络适配器的 SR-IOV、 VMQ 或 RSS 首选项。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>SriovPreferred</th>
<th align="left"></em>RssOrVmqPreference</th>
<th align="left"><em>SRIOV</th>
<th align="left"></em>VMQ</th>
<th align="left">*RSS</th>
<th align="left">启用的界面</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>SR-IOV 和 VMQ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1，0，或在注册表中不存在</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>RSS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

**请注意**  同时启用时 SR-IOV 和 VMQ 接口，为 VMQ 接口，而不是虚拟机队列的 SR-IOV 非默认虚拟端口 (VPorts) 附加到 PCI Express (PCIe) 物理函数 (PF) 使用。 有关详细信息，请参阅[非默认虚拟端口和 VMQ](nondefault-virtual-ports-and-vmq.md)。

 

微型端口驱动程序必须播发当前已启用接口的功能。 例如，如果启用了 SR-IOV，微型端口驱动程序必须播发的 SR-IOV 功能，但不是功能 VMQ 或 RSS。 但是，微型端口驱动程序始终必须在网络适配器上报告而不考虑其启用接口的完整 RSS、 VMQ 和 SR-IOV 硬件功能。

**请注意**  VMQ 和 SR-IOV 接口使用接收通过 VM 队列或的 SR-IOV 虚拟端口 (VPorts) 筛选。 因此，某些接收筛选功能需要相同或不同的设置时其中任何一个接口处于启用状态。 如何报告接收筛选 SR-IOV 接口的功能的详细信息，请参阅[确定收到的筛选功能](determining-receive-filtering-capabilities.md)。 如何报告接收筛选 VMQ 接口的功能的详细信息，请参阅[确定网络适配器的 VMQ 功能](determining-the-vmq-capabilities-of-a-network-adapter.md)。

 

 

 





