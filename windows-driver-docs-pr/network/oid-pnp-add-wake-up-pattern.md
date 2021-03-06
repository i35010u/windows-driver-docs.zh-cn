---
title: OID_PNP_ADD_WAKE_UP_PATTERN
description: OID_PNP_ADD_WAKE_UP_PATTERN
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_ADD_WAKE_UP_PATTERN 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f4816dd76e65949420d1ff1cfdb3e318f8e3fe61
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248209"
---
# <a name="oid_pnp_add_wake_up_pattern"></a>OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式





OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式 OID 由协议驱动程序发送到微型端口驱动程序以指定唤醒模式。 唤醒模式连同其掩码，由 [**NDIS \_ PM \_ 数据包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern) 结构描述。

一种协议，用于启用微型端口驱动程序的模式匹配唤醒 (参阅 [oid \_ pnp \_ ENABLE \_ 唤醒 \_ ](oid-pnp-enable-wake-up.md)) 使用 oid \_ pnp \_ 添加 \_ 唤醒 \_ \_ 模式来指定唤醒模式。 唤醒模式可以存储在主机内存或网络适配器上，具体取决于网络适配器的功能。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含以下内容：

-   提供有关模式及其掩码的信息的 [**NDIS \_ PM \_ 包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern) 结构。

-   一个掩码，用于指示应将传入数据包的哪些字节与模式中的相应字节进行比较。 掩码以数据包的第一个字节开始。 掩码紧跟 *InformationBuffer* 中的 [**NDIS \_ PM \_ 数据包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构。 有关此掩码如何工作的详细信息，请参阅 [网络设备类电源管理参考规范](https://go.microsoft.com/fwlink/p/?linkid=27255)。

-   唤醒模式，从 *InformationBuffer* 的开头开始 **PatternOffset** 字节。 有关唤醒模式的详细信息，请参阅 [网络设备类电源管理参考规范](https://go.microsoft.com/fwlink/p/?linkid=27255)。

微型端口驱动程序可以接受的唤醒模式数可能取决于资源的可用性，例如，小型端口驱动程序为此类模式分配的主机内存或网络适配器中的可用存储。 如果微型端口驱动程序无法添加唤醒模式，原因是资源不足，微型端口驱动程序会返回 **NDIS \_ 状态 \_ 资源** 以响应 OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式。

如果协议驱动程序尝试添加重复模式，微型端口驱动程序应返回 **NDIS \_ 状态 \_ 无效 \_ 数据** 以响应 OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式。

在其中，上边缘接收此 OID 请求的中间驱动程序必须始终通过调用 [**NdisRequest**](/previous-versions/windows/hardware/network/ff554681(v=vs.85)) 或 [**NdisCoRequest**](/previous-versions/windows/hardware/network/ff551877(v=vs.85))将该请求传播到基础微型端口驱动程序。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 NDIS 6.0 和 NDIS 6.1 中受支持。 对于 NDIS 6.20 和更高版本，请改用 <a href="oid-pm-add-wol-pattern.md" data-raw-source="[OID_PM_ADD_WOL_PATTERN](oid-pm-add-wol-pattern.md)">OID_PM_ADD_WOL_PATTERN</a> 。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ PM \_ 数据包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[OID \_ PM \_ 添加 \_ WOL \_ 模式](oid-pm-add-wol-pattern.md)

 

