---
title: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS
description: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS 是一个 TLV，其中包含 NDIS_STATUS_WDI_INDICATION_DISASSOCIATION 的解除其指示参数。
ms.assetid: AD799DAA-B89D-4015-8DC5-53057C4DA43E
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d1bdd2e7f2b3350da6be78c9d92c2449ba0d016b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834139"
---
# <a name="wdi_tlv_disassociation_indication_parameters"></a>WDI\_TLV\_解除\_指示\_参数


WDI\_TLV\_解除\_指示\_参数是一个 TLV，其中包含 NDIS 的解除指示参数\_[状态\_WDI\_指示\_](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-disassociation)解除。

## <a name="tlv-type"></a>TLV 类型


0xBC

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                         | 描述                                                                |
|--------------------------------------------------------------|----------------------------------------------------------------------------|
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)            | 与解除关联的指示关联的对等方的 MAC 地址。 |
| [**WDI\_ASSOC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status)（UINT32） | 解除解除的指示的触发器。                             |

 

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

 

 




