---
title: WFP 层要求和限制
description: WFP 层要求和限制
ms.assetid: 3677cc12-3242-4fbd-809d-303b9d324139
keywords:
- 处理数据包 WDK Windows 筛选平台
- 数据包处理 WDK Windows 筛选平台
- 对于处理 WDK Windows 筛选平台数据包层
ms.date: 01/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: e4db65596a45510cc9722fb025367ccef437bce2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365684"
---
# <a name="wfp-layer-requirements-and-restrictions"></a>WFP 层要求和限制


以下要求和限制适用于 WFP 层。

<a href="" id="forwarding-layer-------"></a>**转发层**   
如果源自，或为分配给计算机的地址发送到某个数据包启用 IP 转发和发送或比其上的接口不同接口上接收数据包的 IP 数据包将传递到转发层 l分配本地地址。 默认情况下，IP 转发已禁用，并且可以通过启用**netsh interface ipv4 设置接口**命令为 IPv4 转发或**netsh 接口 ipv6 设置接口**命令获取 IPv6转发。

转发层可以转发收到的每个片段到达时，或保留的 IP 有效负载的片段，直到所有片段已推出，然后将其转发。 这称为*片段分组*。 如果片段分组是已禁用 （默认情况下禁用），转发 IP 数据包指示片段到 WFP 一次。 启用片段分组后，片段指定给 WFP 两次-首先如片段本身，并再次在片段组描述[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)链。 WFP 集**FWP\_条件\_标志\_IS\_片段\_组**标志时，它指示片段到转发层调出的组。 可以使用启用片段分组**netsh 接口 {ipv4 | ipv6} 设置全局 groupforwardedfragments = 启用**命令。 片段分组是不同于重组，这是在目标主机上的原始 IP 数据包的重新构造。

[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，它指示在转发层可描述 IP 数据包分段，还是 IP 数据包片段组的完整的 IP 数据包。 虽然 IP 数据包分段遍历转发层，将进行说明两次到标注： 第一次用作片断形式，以及同样，片段组内的一个片段。

如果指示片段组， **FWP\_条件\_标志\_IS\_片段\_组**标志作为传入值传递给标注驱动[*classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)标注函数。 在这种情况下， [ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)指向结构*NetBufferList*参数是的第一个节点**NET\_缓冲区\_列表**链与每个**NET\_缓冲区\_列表**描述数据包片段。

向前插入的数据包不会呈现给任何 WFP 层中。 插入的数据包可以再次指定给标注驱动程序。 若要防止无限循环，该驱动程序应首先调用[ **FwpsQueryPacketInjectionState0** ](https://msdn.microsoft.com/library/windows/hardware/ff551202)函数才能继续执行调用*classifyFn*标注函数，因此，驱动程序应允许将注入状态的数据包[ **FWPS\_数据包\_注入\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff552408)设置为**FWPS\_数据包\_INJECTED\_BY\_自助**或者**FWPS\_数据包\_以前\_INJECTED\_BY\_自助**通过不变。

可以使用以下命令以查看系统的当前"组转发片段"设置： **netsh 接口 {ipv4 | ipv6} 显示全局**。

<a href="" id="network-layer-------"></a>**网络层**   
IP 数据包分段，指示仅对传入的路径，指示在此层上的三个点： 首先为 IP 数据包，再次作为 IP 分段，并且第三次重新组合的 IP 数据包的一部分。 WFP 集**FWP\_条件\_标志\_IS\_片段**标志时指示网络层标注的片段。 

例如，如果单个 IP 数据包分为四个片段，此数据包指示将按如下所示发生：

1. 一个指示为每个"原始"的 IP 数据包 （4 个分类或调用标注的分类函数） 的
2. 一个表示每个"原始 fragment"（4 个分类）
3. 一个表示最终重新组合 IP 数据包 （1 分类）

添加筛选条件时**FWP\_匹配\_标志\_NONE\_设置**可一起使用**FWP\_条件\_标志\_IS\_片段**标志，以避免第二个 indication(s)。 这些条件标志是为了防止标注驱动程序并不关心的分类。 如果标注必须检查只能使用完整的数据包 （那些尚未分段和重组），它必须解析要避免处理片段表示为 IP 数据包的 IP 标头。 标注可能会执行以下步骤来实现此目的：

1. 跳过第一个 indication(s) 检查是否已设置的更多片段 (MF) 标志和/或片段的偏移量字段不是 0。
2. 编写筛选器，允许所有分类其中**FWP_CONDITION_FLAG_IS_FRAGMENT**设置。
3. 执行任何处理需要重新组合的数据包。

 或者，标注可以检查数据包在传输层。

<a href="" id="transport-layer-and-ale-------"></a>**传输层和 ALE**   
若要能够与 IPsec 处理共存，检查在传入的传输层的数据包的标注还必须注册在 ALE 接收和接受层。 此类标注可以检查/修改大部分在传输层流量，但它还必须允许分配给 ALE 接收/接受层的数据包。 此类标注还必须检查或修改从 ALE 层数据包。 WFP 集**FWPS\_元数据\_字段\_ALE\_分类\_必需**元数据的标志时，它指示在传输层需要 ALE 这些数据包检查。 IPsec 处理会推迟到创建初始的"连接"，以及进行重新授权连接所需的这些数据包到达 ALE 层。

传输层和 ALE 层标注必须自行注册在较低的权重比通用子图层的一个子图层。 内置的 IPsec/ALE 强制标注驻留在通用子图层。

下表显示可以指示 ALE 层的数据包类型。 请注意，某些 ALE 层并不总是有其指示与关联的数据包。

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
<td align="left"><p>绑定 （资源分配）</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="even">
<td align="left"><p>连接</p></td>
<td align="left"><p>没有与数据包</p></td>
<td align="left"><p>第一个 UDP 数据包 （传出）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>接收接受</p></td>
<td align="left"><p>SYN （传入）</p></td>
<td align="left"><p>第一个 UDP 数据包 （传入）</p></td>
</tr>
<tr class="even">
<td align="left"><p>建立的流</p></td>
<td align="left"><p>最后的 ACK (传入&amp;传出)</p></td>
<td align="left"><p>第一个 UDP 数据包 (传入&amp;传出)</p></td>
</tr>
</tbody>
</table>

 

 

 





