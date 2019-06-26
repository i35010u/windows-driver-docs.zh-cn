---
title: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS
description: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS 是包含解除关联指示参数用于 NDIS_STATUS_WDI_INDICATION_DISASSOCIATION TLV。
ms.assetid: AD799DAA-B89D-4015-8DC5-53057C4DA43E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 346b0005a76203a8b9c68a8b61feba0394650055
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360236"
---
# <a name="wditlvdisassociationindicationparameters"></a>WDI\_TLV\_解除关联\_指示\_参数


WDI\_TLV\_解除关联\_指示\_参数是包含解除关联指示参数 TLV [NDIS\_状态\_WDI\_指示\_解除关联](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-disassociation)。

## <a name="tlv-type"></a>TLV 类型


0xBC

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                         | 描述                                                                |
|--------------------------------------------------------------|----------------------------------------------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)            | 解除关联指示与关联的对等方的 MAC 地址。 |
| [**WDI\_ASSOC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_assoc_status) (UINT32) | 解除关联指示该触发器。                             |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




