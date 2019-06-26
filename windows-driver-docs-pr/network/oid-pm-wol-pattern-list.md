---
title: OID_PM_WOL_PATTERN_LIST
description: 为查询，过量驱动程序可用于 OID_PM_WOL_PATTERN_LIST OID 枚举基础的网络适配器设置的 LAN 模式唤醒。
ms.assetid: 7e5a65d8-39ec-4624-aede-97df945ef5e5
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_WOL_PATTERN_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 85fc196b3050aaf8dd20f7ce42d35003e418e254
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373343"
---
# <a name="oidpmwolpatternlist"></a>OID\_PM\_WOL\_模式\_列表


为查询，过量驱动程序可以使用 OID\_PM\_WOL\_模式\_列表 OID 枚举基础的网络适配器设置的 LAN 模式唤醒。 从查询中，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含指针到一系列[ **NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)描述了当前添加了各种 WOL 模式的结构。

<a name="remarks"></a>备注
-------

NDIS 处理查询的微型端口驱动程序。 NDIS 驱动程序可以使用 OID\_PM\_WOL\_模式\_列表 OID，若要获取上基础的网络适配器设置的 LAN 模式唤醒的列表。

每个[ **NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构在列表中，NDIS 集**NextWoLPatternOffset**成员添加到从 OID 信息缓冲区开头的偏移量 (即，缓冲区开头的**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构指向) 到下一步开头**NDIS\_PM\_WOL\_模式**列表中的结构。 中的偏移量**NextWoLPatternOffset**列表中的最后一个结构的成员为零。

中的偏移[ **NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构，而不**NextWoLPatternOffset** (例如， **NameBufferOffset**)，NDIS 提供相对于每个开始的偏移量**NDIS\_PM\_WOL\_模式**结构。

如果没有网络适配器设置的 WOL 模式，设置 NDIS**数据。查询\_信息。BytesWritten**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)为零，并返回结构**NDIS\_状态\_成功**请求。 中的数据**数据。查询\_INFORMATION.InformationBuffer** NDIS 不修改成员。

NDIS 返回请求的以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
请求已成功完成。 **InformationBuffer**如果任何包含 WOL 模式的列表的指针。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓冲区\_过\_短  
信息缓冲区太短。 NDIS 集**数据。查询\_信息。BytesNeeded** NDIS 中的成员\_OID\_结构到最小缓冲区大小的请求是必需的。

<a href="" id="ndis-status-failure"></a>NDIS\_状态\_失败  
请求失败，而原因并非前面的原因。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持 NDIS 6.20 及更高版本。 未请求的微型端口驱动程序。 （请参见备注部分。）</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_WOL\_PATTERN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)

[OID\_PM\_ADD\_WOL\_PATTERN](oid-pm-add-wol-pattern.md)

[OID\_PM\_REMOVE\_WOL\_PATTERN](oid-pm-remove-wol-pattern.md)

[OID\_PNP\_WAKE\_UP\_PATTERN\_LIST](oid-pnp-wake-up-pattern-list.md)

 

 




