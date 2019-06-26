---
title: NDIS_STATUS_WDI_INDICATION_TKIP_MIC_FAILURE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_TKIP_MIC_FAILURE 来指示当接收的数据包已成功解密 TKIP 密码算法的失败消息完整性代码 (MIC) 验证。
ms.assetid: ab9d3109-72af-457e-9e65-456613cea32f
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_TKIP_MIC_FAILURE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 135f8fcdefa4d66c1026a4df8abb8733d67f7cfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375193"
---
# <a name="ndisstatuswdiindicationtkipmicfailure"></a>NDIS\_状态\_WDI\_指示\_TKIP\_MIC\_失败


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_TKIP\_MIC\_故障指示时接收的数据包已成功解密的 TKIP 密码算法消息完整性代码 (MIC) 验证失败。

| Object |
|--------|
| Port   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                             | 允许多个 TLV 实例 | 可选 | 描述                       |
|----------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------|
| [**WDI\_TLV\_TKIP\_MIC\_FAILURE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-tkip-mic-failure-info) |                                |          | TKIP MIC 失败信息。 |

 

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

 

 




