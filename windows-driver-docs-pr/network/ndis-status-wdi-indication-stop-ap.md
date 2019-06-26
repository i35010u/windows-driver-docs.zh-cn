---
title: NDIS_STATUS_WDI_INDICATION_STOP_AP
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_STOP_AP 指示适配器无法承受任何 PHYs 802.11 访问点 (AP) 功能。
ms.assetid: EF129BD3-6AA2-4F38-BECD-E9D526314A27
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_STOP_AP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d634be86928ccb383763dbb4195cc98c492c01ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375211"
---
# <a name="ndisstatuswdiindicationstopap"></a>NDIS\_状态\_WDI\_指示\_停止\_亚太


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_停止\_AP 以指示该适配器无法承受任何 PHYs 802.11 访问点 (AP) 功能。 只有在 NIC 上可用 PHYs 已停止运行任何 APs 后，适配器应发送此指示。 主机阻止所有[OID\_WDI\_任务\_启动\_AP](oid-wdi-task-start-ap.md)请求，直到适配器发送为止[NDIS\_状态\_WDI\_指示\_可以\_SUSTAIN\_AP](ndis-status-wdi-indication-can-sustain-ap.md)。

| Object |
|--------|
| Port   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                      | 允许多个 TLV 实例 | 可选 | 描述                                                                       |
|---------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------|
| [**WDI\_TLV\_INDICATION\_STOP\_AP**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-indication-stop-ap) |                                |          | 该适配器的原因无法承受任何 PHYs 802.11 AP 功能。 |

 

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


[OID\_WDI\_TASK\_START\_AP](oid-wdi-task-start-ap.md)

[NDIS\_状态\_WDI\_指示\_可以\_SUSTAIN\_亚太](ndis-status-wdi-indication-can-sustain-ap.md)

 

 




