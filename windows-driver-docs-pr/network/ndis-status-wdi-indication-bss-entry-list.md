---
title: NDIS_STATUS_WDI_INDICATION_BSS_ENTRY_LIST
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_BSS_ENTRY_LIST 通知主机有关 BSS 条目的更新。 这是未经请求的指示，可以在任何时候发送。
ms.assetid: 5b9fd7b1-0817-4b86-9acc-b4f99cb7ae9a
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_BSS_ENTRY_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4f06036f2716971c29a146de10a0d128161f8d18
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360253"
---
# <a name="ndisstatuswdiindicationbssentrylist"></a>NDIS\_状态\_WDI\_指示\_BSS\_条目\_列表


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_BSS\_条目\_列表以通知主机有关 BSS 条目的更新。 这是未经请求的指示，可以在任何时候发送。

| Object |
|--------|
| Port   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                   | 允许多个 TLV 实例 | 可选 | 描述                 |
|--------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI\_TLV\_BSS\_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bss-entry) | X                              | X        | 更新 BSSIDs 的列表。 |

 

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


[OID\_WDI\_TASK\_SCAN](oid-wdi-task-scan.md)

[OID\_WDI\_TASK\_P2P\_DISCOVER](oid-wdi-task-p2p-discover.md)

[OID\_WDI\_设置\_P2P\_启动\_背景\_发现](oid-wdi-set-p2p-start-background-discovery.md)

 

 




