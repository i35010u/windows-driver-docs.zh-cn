---
title: OID_PM_WOL_PATTERN_LIST
description: 作为查询，过量驱动程序可以使用 OID_PM_WOL_PATTERN_LIST OID 来枚举基础网络适配器上设置的 LAN 唤醒模式。
ms.assetid: 7e5a65d8-39ec-4624-aede-97df945ef5e5
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_WOL_PATTERN_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 83d61dbd692327cc649b3af3326cfb20e6687d5e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844045"
---
# <a name="oid_pm_wol_pattern_list"></a>OID\_PM\_WOL\_模式\_列表


作为查询，过量驱动程序可以使用 OID\_PM\_WOL\_模式\_列表 OID 来枚举基础网络适配器上设置的 LAN 唤醒模式。 成功从查询返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**ndis\_PM 列表的指针\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构，用于描述当前添加的 WOL 模式。

<a name="remarks"></a>备注
-------

NDIS 处理微型端口驱动程序的查询。 NDIS 驱动程序可以使用 OID\_PM\_WOL\_模式\_列表 OID 来获取在基础网络适配器上设置的 LAN 唤醒模式的列表。

对于列表中的每个[**NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构，NDIS 将**NextWoLPatternOffset**成员设置为距 OID 信息缓冲区开头的偏移量（即，缓冲区**的开头** [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构指向）的 InformationBuffer 成员到下一个**NDIS\_PM\_WOL\_模式**结构在列表中的开头。 列表中最后一个结构的**NextWoLPatternOffset**成员中的偏移量为零。

对于 Ndis 中的偏移量[ **\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构，而不是**NextWoLPatternOffset** （例如， **NameBufferOffset**），NDIS 提供相对于每个**NDIS\_PM 的开头的偏移量。\_WOL\_模式**结构。

如果网络适配器上没有设置的 WOL 模式，NDIS 将设置**数据。查询\_信息。BytesWritten** [**NDIS\_OID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)的成员将\_请求结构恢复为零，并将**ndis\_状态返回\_请求成功**。 数据内的数据 **。查询\_InformationBuffer**成员不由 NDIS 修改。

NDIS 为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
请求已成功完成。 **InformationBuffer**包含指向 WOL 模式列表的指针（如果有）。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_挂起  
请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓存\_\_太短  
信息缓冲区太短。 NDIS 设置**数据。查询\_信息。** \_OID 中的 BytesNeeded 成员\_请求结构到所需的最小缓冲区大小。

<a href="" id="ndis-status-failure"></a>\_故障时的 NDIS\_状态  
由于上述原因之外的原因，导致请求失败。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.20 和更高版本中受支持。 未请求微型端口驱动程序。 （请参见 "备注" 部分。）</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)

[OID\_PM\_添加\_WOL\_模式](oid-pm-add-wol-pattern.md)

[OID\_PM\_删除\_WOL\_模式](oid-pm-remove-wol-pattern.md)

[OID\_PNP\_唤醒\_\_模式\_列表](oid-pnp-wake-up-pattern-list.md)

 

 




