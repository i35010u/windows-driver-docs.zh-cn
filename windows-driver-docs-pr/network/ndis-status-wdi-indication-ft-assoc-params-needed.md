---
title: NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED 802.11r 漫游到请求参数。ObjectPort。
ms.assetid: AB745908-AA7B-416A-9C97-B376293F3DEE
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b636ac0f613a4f5b10e2e51338709e4708db3e90
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354944"
---
# <a name="ndisstatuswdiindicationftassocparamsneeded"></a>NDIS\_状态\_WDI\_指示\_FT\_ASSOC\_PARAMS\_需执行


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_FT\_ASSOC\_PARAMS\_需执行到 802.11r 漫游的请求参数。

| Object |
|--------|
| Port   |

 

期间[OID\_WDI\_任务\_漫游](oid-wdi-task-roam.md)，WDI 提供要发送 802.11 身份验证请求 （PmkR0Name，R0KH ID、 SNonce，MDIE） 的参数。 一旦收到身份验证响应，LE 请求其他所需的参数重新关联请求，如 PMKR1Name 和 R1KH id。 LE 还会发送在身份验证响应 （ANonce、 SNonce 和 R1KHID） 时收到的参数。

对于其中初始移动域已成功完成的连接，LE 仅应执行 11r 漫游时 （快速漫游）。 LE 可以使用由操作系统提供的候选项列表或对漫游时使用他们自己。 如果 LE 使用自己的候选项列表，它必须使用提供的任意一种由操作系统建议的候选项的参数 （MDE、 FTE、 和 PMKR0Name） 来进行 11r 漫游。 处于 FIPS 模式下连接时，11r 处于禁用状态。 11r 快速漫游目前仅支持 FT 超过 1 个身份验证类型。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                  | 允许多个 TLV 实例 | 可选 | 描述                            |
|-----------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI\_TLV\_BSSID**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bssid)                         |                                |          | AP BSSID。                   |
| [**WDI\_TLV\_FT\_AUTH\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ft-auth-request)   |                                |          | 身份验证请求的字节 blob。  |
| [**WDI\_TLV\_FT\_AUTH\_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ft-auth-response) |                                |          | 身份验证响应字节 blob。 |

 

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

 

 




