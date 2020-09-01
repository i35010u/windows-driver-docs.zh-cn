---
title: WDI_TLV_ROAMING_NEEDED_PARAMETERS
description: WDI_TLV_ROAMING_NEEDED_PARAMETERS 是包含漫游触发器原因的 TLV。 此项用于 NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED 负载。
ms.assetid: 152F923C-ECAE-4D50-A7B4-4B2309D5A3B5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ROAMING_NEEDED_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9ac94372cb53336b7613478d1d39c36bd967d919
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206705"
---
# <a name="wdi_tlv_roaming_needed_parameters"></a>WDI \_ TLV \_ \_ 需要 \_ 参数


WDI \_ tlv \_ \_ 需要 \_ 参数是包含漫游触发器原因的 tlv。 这用于 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 漫游 \_ 所需](./ndis-status-wdi-indication-roaming-needed.md) 的负载。

## <a name="tlv-type"></a>TLV 类型


0x55

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                | 说明                                                                                                                                      |
|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ ASSOC \_ 状态**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status) | 指定漫游触发器的原因。 当触发 [OID \_ WDI \_ 任务 \_ 漫游](./oid-wdi-task-roam.md) 时，此原因将转发给它。 |

 

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
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

