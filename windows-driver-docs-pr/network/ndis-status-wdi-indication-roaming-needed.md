---
title: NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_DISASSOCIATION 指示主机应该尝试查找要连接到的更好地对等方。
ms.assetid: 25f920e9-af87-48ad-be64-aa3ebfe2db5f
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9bcc1603c3832a0c9d1cd95e91b830bf49ec712b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375219"
---
# <a name="ndisstatuswdiindicationroamingneeded"></a>NDIS\_状态\_WDI\_指示\_漫游\_需执行


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_解除关联以指示应尝试找到更好的对等方连接到主机。 链接质量与当前连接的对等方低于特定阈值时，使用此通知。 在发送此通知，主机可能会触发漫游扫描和/或漫游操作。 开始漫游操作之前，Microsoft 组件不执行断开连接。

| Object |
|--------|
| Port   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                    | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                         |
|-----------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_ROAMING\_NEEDED\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-roaming-needed-parameters) |                                |          | 漫游触发器的原因。 当[OID\_WDI\_任务\_漫游](oid-wdi-task-roam.md)是触发，因此转发给它。 |

 

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


[OID\_WDI\_TASK\_ROAM](oid-wdi-task-roam.md)

 

 




