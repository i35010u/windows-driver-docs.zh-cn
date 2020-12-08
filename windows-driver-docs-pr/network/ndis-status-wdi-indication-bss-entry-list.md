---
title: NDIS_STATUS_WDI_INDICATION_BSS_ENTRY_LIST
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_BSS_ENTRY_LIST 通知主机有关 BSS 项的更新。 这是一个未经请求的指示，随时可以发送。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_BSS_ENTRY_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ec7894401993af3742d1bf5a4f85cd15265bd6b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837148"
---
# <a name="ndis_status_wdi_indication_bss_entry_list"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ BSS \_ 条目 \_ 列表


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ bss \_ 条目 \_ 列表，通知主机有关 BSS 项的更新。 这是一个未经请求的指示，随时可以发送。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                   | 允许多个 TLV 实例 | 可选 | 说明                 |
|--------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI \_ TLV \_ BSS \_ 条目**](./wdi-tlv-bss-entry.md) | X                              | X        | 已更新的 BSSIDs 的列表。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WDI \_ 任务 \_ 扫描](oid-wdi-task-scan.md)

[OID \_ WDI \_ 任务 \_ P2P \_ 发现](oid-wdi-task-p2p-discover.md)

[OID \_ WDI \_ 设置 \_ P2P \_ 开始 \_ 后台 \_ 发现](oid-wdi-set-p2p-start-background-discovery.md)

 

