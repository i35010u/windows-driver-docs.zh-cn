---
title: WDI_TLV_ROAMING_NEEDED_PARAMETERS
description: WDI_TLV_ROAMING_NEEDED_PARAMETERS 是包含漫游触发器原因的 TLV。 这用于 NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED 负载。
ms.assetid: 152F923C-ECAE-4D50-A7B4-4B2309D5A3B5
ms.date: 07/18/2017
keywords:
- WDI_TLV_ROAMING_NEEDED_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0a982c9b75a30ca8dfd5da73845f90f506ebc480
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842270"
---
# <a name="wdi_tlv_roaming_needed_parameters"></a>WDI\_TLV\_漫游\_需要\_参数


WDI\_TLV\_漫游\_需要\_参数是包含漫游触发器原因的 TLV。 这用于[NDIS\_状态\_WDI\_指示\_漫游\_所需](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)负载。

## <a name="tlv-type"></a>TLV 类型


0x55

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                | 描述                                                                                                                                      |
|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_ASSOC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status) | 指定漫游触发器的原因。 当[WDI\_TASK\_漫游](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-roam)时，将会将此原因转发到 OID\_。 |

 

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
<td><p>Windows 10</p></td>
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

 

 




