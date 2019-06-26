---
title: NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED 来指示已收到操作帧。
ms.assetid: C1F6EB50-C11F-428F-BF51-5C89A59CBF76
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 436a98f43fbb5e91aa736d5ff3b490cb8704aa04
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382204"
---
# <a name="ndisstatuswdiindicationactionframereceived"></a>NDIS\_状态\_WDI\_指示\_操作\_帧\_接收时间


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_操作\_帧\_接收时间以指示已收到操作帧。

| Object |
|--------|
| Port   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                               | 允许多个 TLV 实例 | 可选 | 描述                                               |
|------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bssid)                                      |                                |          | 源的 BSSID。                                  |
| [**WDI\_TLV\_BSS\_条目\_通道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bss-entry-channel-info) |                                |          | BSS 项的逻辑的通道数量和带区 ID。 |
| [**WDI\_TLV\_操作\_帧\_正文**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-action-frame-body)            |                                |          | 传入操作帧正文。                           |

 

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

 

 




