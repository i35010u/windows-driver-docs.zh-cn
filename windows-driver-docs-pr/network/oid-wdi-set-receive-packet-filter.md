---
title: OID_WDI_SET_RECEIVE_PACKET_FILTER
description: OID_WDI_SET_RECEIVE_PACKET_FILTER 定义指示针对给定的虚拟化端口的数据包的位掩码筛选器。
ms.assetid: 180efda5-3ca2-40f8-89d1-098a53f33844
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_RECEIVE_PACKET_FILTER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c3689ef12a32c38a5ae424b28a1d3b0357778eed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576720"
---
# <a name="oidwdisetreceivepacketfilter"></a>OID\_WDI\_SET\_RECEIVE\_PACKET\_FILTER


OID\_WDI\_设置\_接收\_数据包\_筛选器定义来指示给定的虚拟化端口的数据包的位掩码筛选器。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

如果设置，该端口应仅通知宿主的数据包匹配提供的筛选器。 这些筛选器是与提供给需要 802.11 筛选器类似[OID\_代\_当前\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569575)。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                   | 允许多个 TLV 实例 | 可选 | 描述                          |
|---------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------|
| [**WDI\_TLV\_PACKET\_FILTER\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn898019) |                                |          | 数据包的位掩码筛选器。 |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。
要求
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

 

 




