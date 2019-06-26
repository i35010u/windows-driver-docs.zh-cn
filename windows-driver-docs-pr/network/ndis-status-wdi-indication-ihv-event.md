---
title: NDIS_STATUS_WDI_INDICATION_IHV_EVENT
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_IHV_EVENT IHV 特定信息传递给 IHV 扩展性模块。
ms.assetid: 767f15cd-456f-4d91-9b78-58f8f8b7a465
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_IHV_EVENT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 545d309c79dffabcdc90e19b4a333ea2bf56d6fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354956"
---
# <a name="ndisstatuswdiindicationihvevent"></a>NDIS\_状态\_WDI\_指示\_IHV\_事件


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_IHV\_事件将传递给 IHV 扩展性模块 IHV 特定信息。

| Object |
|--------|
| Port   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                 | 允许多个 TLV 实例 | 可选 | 描述                                           |
|------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------|
| [**WDI\_TLV\_IHV\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ihv-data) |                                | X        | 要发送到 IHV 扩展性模块的事件。 |

 

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

 

 




