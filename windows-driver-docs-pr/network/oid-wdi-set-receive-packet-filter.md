---
title: OID_WDI_SET_RECEIVE_PACKET_FILTER
description: OID_WDI_SET_RECEIVE_PACKET_FILTER 定义指示针对给定的虚拟化端口的数据包的位掩码筛选器。
ms.assetid: 180efda5-3ca2-40f8-89d1-098a53f33844
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_RECEIVE_PACKET_FILTER 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 71174eab83b2c0593cbd49dc2bf81b62731a6a6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359182"
---
# <a name="oidwdisetreceivepacketfilter"></a>OID\_WDI\_SET\_RECEIVE\_PACKET\_FILTER


OID\_WDI\_设置\_接收\_数据包\_筛选器定义来指示给定的虚拟化端口的数据包的位掩码筛选器。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 是                      | 1                               |

 

如果设置，该端口应仅通知宿主的数据包匹配提供的筛选器。 这些筛选器是与提供给需要 802.11 筛选器类似[OID\_代\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                   | 允许多个 TLV 实例 | 可选 | 描述                          |
|---------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------|
| [**WDI\_TLV\_PACKET\_FILTER\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-packet-filter-parameters) |                                |          | 数据包的位掩码筛选器。 |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。

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

 

 




