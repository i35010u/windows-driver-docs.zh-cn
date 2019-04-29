---
title: NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED 来指示已收到操作帧。
ms.assetid: C1F6EB50-C11F-428F-BF51-5C89A59CBF76
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f096bdf33487c34bbe8156b72421502c9093ea9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366423"
---
# <a name="ndisstatuswdiindicationactionframereceived"></a>NDIS\_状态\_WDI\_指示\_操作\_帧\_接收时间


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_操作\_帧\_接收时间以指示已收到操作帧。

| Object |
|--------|
| 端口   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                               | 允许多个 TLV 实例 | 可选 | 描述                                               |
|------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](https://msdn.microsoft.com/library/windows/hardware/dn926153)                                      |                                |          | 源的 BSSID。                                  |
| [**WDI\_TLV\_BSS\_条目\_通道\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn926155) |                                |          | BSS 项的逻辑的通道数量和带区 ID。 |
| [**WDI\_TLV\_操作\_帧\_正文**](https://msdn.microsoft.com/library/windows/hardware/dn926118)            |                                |          | 传入操作帧正文。                           |

 

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

## <a name="see-also"></a>请参阅


[OID\_WDI\_设置\_播发\_信息](oid-wdi-set-advertisement-information.md)

 

 




