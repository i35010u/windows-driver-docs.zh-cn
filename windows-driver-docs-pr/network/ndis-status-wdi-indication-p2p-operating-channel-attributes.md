---
title: NDIS_STATUS_WDI_INDICATION_P2P_OPERATING_CHANNEL_ATTRIBUTES
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_P2P_OPERATING_CHANNEL_ATTRIBUTES 指示首选的操作通道启动 GO、 首选侦听通道要求输入侦听状态，如果和完整的集支持在任何时间点的通道. 指示适配器初始化时，发送一次，然后每次发送一个事件由于这些参数更改如漫游或连接或断开与访问点的连接。
ms.assetid: F7D27328-99B3-4EB5-9F48-864338EF8D8A
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_P2P_OPERATING_CHANNEL_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bc85dc2b7ad550306b13d1d656d5e08300b8fe03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566177"
---
# <a name="ndisstatuswdiindicationp2poperatingchannelattributes"></a>NDIS\_状态\_WDI\_指示\_P2P\_OPERATING\_通道\_属性


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_P2P\_OPERATING\_通道\_属性，指示首选操作通道启动 GO首选如果要求输入侦听状态和受支持的通道在任何时间点的完整集侦听通道。 指示适配器初始化时，发送一次，然后每次发送一个事件由于这些参数更改如漫游或连接或断开与访问点的连接。

| 对象 |
|--------|
| 端口   |

 

操作通道和通道列表值是本地设置，不考虑实际通道协商期间 GO 协商/邀请。 该驱动程序仍需要执行 GO 协商/邀请时协商的通道。

应遵循由驱动程序报告的侦听通道，如果启用侦听状态。 如果主机配置不同于通过此指示以前报告过的首选的侦听通道的侦听通道，触发此指示应。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                       | 允许多个 TLV 实例 | 可选 | 描述                                              |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------|
| [**WDI\_TLV\_P2P\_CHANNEL\_NUMBER**](https://msdn.microsoft.com/library/windows/hardware/dn897869)                  |                                |          | Wi-Fi Direct 操作通道属性。            |
| [**WDI\_TLV\_P2P\_CHANNEL\_LIST\_ATTRIBUTE**](https://msdn.microsoft.com/library/windows/hardware/dn897868) |                                |          | 一组完整的本地适配器支持的通道。 |
| [**WDI\_TLV\_P2P\_LISTEN\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/mt269138)                  |                                |          | Wi-Fi Direct 侦听通道属性。               |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




