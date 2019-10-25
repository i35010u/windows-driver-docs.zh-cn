---
title: WFP 层要求和限制
description: WFP 层要求和限制
ms.assetid: 3677cc12-3242-4fbd-809d-303b9d324139
keywords:
- 处理数据包 WDK Windows 筛选平台
- 包处理 WDK Windows 筛选平台
- 用于包处理 WDK Windows 筛选平台的层
ms.date: 01/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: dc91eb6c100226882bc4e6230e85281997947c2c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841698"
---
# <a name="wfp-layer-requirements-and-restrictions"></a>WFP 层要求和限制


以下要求和限制适用于 WFP 层。

<a href="" id="forwarding-layer-------"></a>**转发层**   
如果为来源为的数据包或目标为的数据包启用了 IP 转发，则 IP 数据包将传递到转发层; 如果为，则会将该地址发送到计算机，并在与 l已分配本地地址。 默认情况下，IP 转发处于禁用状态，并且可以通过使用适用于 IPv4 转发的**netsh 接口 ipv4 集接口**命令或用于 ipv6 转发的**netsh interface ipv6 set interface**命令启用。

转发层可以在到达时转发每个已接收的片段，也可以保留 IP 有效负载的片段，直到所有片段到达并转发它们为止。 这称为*片段分组*。 禁用片段分组后（默认情况下禁用它），转发的 IP 数据包段会指示到 WFP 一次。 启用片段分组后，会将一个片段指定为 WFP 两次：第一次为片段本身，并再次在由[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)链描述的分段组内。 WFP **\_会将 .fwp\_条件设置\_标志\_** 当它指示要转发的片段组时，\_组标志。 可以使用**netsh interface {ipv4 | ipv6} set global groupforwardedfragments = enabled**命令启用片段分组。 片段分组不同于重新组合，后者是目标主机上的原始 IP 数据包的重新构造。

在转发层指示的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构可以描述完整的 IP 数据包、ip 数据包片段或 ip 数据包片段组。 当 IP 数据包片段遍历转发层时，它将被指定两次标注：第一次为片段，并再次显示为片段组内的片段。

当指示分段组时， **\_\_标志的 .fwp 条件\_是\_片段\_组**标志作为传入值传递到标注驱动程序的[*classifyFn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) callout 函数。 在这种情况下， *NetBufferList*参数指向的[**net\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构是**网络\_\_缓冲区**的第一个节点，其中每个**net\_缓冲区\_列表**描述数据包片段。

正向注入的数据包将不会显示在任何 WFP 层上。 可以再次向标注驱动程序指示插入的数据包。 若要防止无限循环，驱动程序应首先调用[**FwpsQueryPacketInjectionState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsquerypacketinjectionstate0)函数，然后再调用*classifyFn* callout 函数，驱动程序应该允许具有注入状态[**的数据包FWPS\_数据包\_注入\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_packet_injection_state_)设置为**FWPS\_数据包\_通过**\_self 或**FWPS\_数据包\_注入\_** 如果未经过修改，则为。

你可以使用以下命令来查看 system： **netsh interface {ipv4 | ipv6} show global**的当前 "组转发片段" 设置。

<a href="" id="network-layer-------"></a>**网络层**   
仅为传入路径指示的 IP 数据包片段在此层上的三个点上指定：第一种是 IP 数据包，作为 IP 分段再次出现，第三次在重新组合 IP 数据包中。 WFP 会将 **.fwp\_条件设置\_标志\_** 当指示片段到网络层标注时\_片段标志。 

例如，如果单个 IP 数据包分为四个段，则此数据包的指示如下所示：

1. 为每个 "原始" IP 数据包（4个分类或对标注的分类函数的调用）提供一个指示
2. 每个 "原始片段" 的一个指示（4个分类）
3. 最终重新组合的 IP 数据包（1个分类）的一个指示

添加筛选条件时， **\_匹配\_标志\_NONE\_集**可与 **.fwp\_条件一起使用\_标志**\_\_片段标志，以避免第二次指示。 这些条件标志旨在防止标注驱动程序所关心的分类。 如果标注只需要检查完整的数据包（未进行碎片整理和重新组合），则必须分析 IP 标头以避免处理显示为 IP 数据包的片段。 标注可能执行以下步骤来实现此目的：

1. 通过检查是否设置了更多片段（MF）标志，并/或 "片段偏移量" 字段不为0，跳过第一个指示。
2. 编写允许在其中设置**FWP_CONDITION_FLAG_IS_FRAGMENT**的所有分类的筛选器。
3. 执行重新组合的数据包上所需的任何处理。

 或者，标注可以在传输层检查数据包。

<a href="" id="transport-layer-and-ale-------"></a>**传输层和 ALE**   
为了能够与 IPsec 处理共存，在传入传输层检查数据包的标注还必须在 ALE 接收和接受层进行注册。 此类标注可以在传输层检查/修改大多数流量，但它还必须允许分配给 ALE 接收/接受层的数据包。 此类标注还必须从 ALE 层检查或修改数据包。 WFP 会将 " **FWPS\_元数据"\_\_字段设置为 "ALE\_分类\_必需**的元数据" 标志，指示传输层需要 ALE 检查的数据包。 IPsec 处理会推迟，直到创建初始 "连接" 的数据包和重新授权连接所需的数据包到达 ALE 层。

传输层和 ALE 层标注必须在小于通用子层的子层上注册自身。 内置 IPsec/ALE 强制标注位于通用子层上。

下表显示了可以在 ALE 层指示的数据包类型。 请注意，某些 ALE 层并不总是有与其指示关联的数据包。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ALE 层</th>
<th align="left">TCP 数据包</th>
<th align="left">UDP 数据包</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>绑定（资源分配）</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="even">
<td align="left"><p>“连接”</p></td>
<td align="left"><p>无数据包</p></td>
<td align="left"><p>第一个 UDP 数据包（传出）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>接收/接受</p></td>
<td align="left"><p>SYN （传入）</p></td>
<td align="left"><p>第一个 UDP 数据包（传入）</p></td>
</tr>
<tr class="even">
<td align="left"><p>已建立流</p></td>
<td align="left"><p>最终确认（传入 & 传出）</p></td>
<td align="left"><p>第一个 UDP 数据包（传入 & 传出）</p></td>
</tr>
</tbody>
</table>

 

 

 





