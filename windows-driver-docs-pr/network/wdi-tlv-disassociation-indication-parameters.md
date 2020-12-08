---
title: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS
description: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS 是包含 NDIS_STATUS_WDI_INDICATION_DISASSOCIATION 的解除对应参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a20652a8c9a6c3ef3e8165a1eb870498da5c680b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803479"
---
# <a name="wdi_tlv_disassociation_indication_parameters"></a>WDI \_ TLV \_ 解除 \_ 指示 \_ 参数


WDI \_ tlv \_ 解除 \_ \_ 对应的参数是一个 Tlv，其中包含 [NDIS \_ 状态 \_ WDI \_ 指示 \_ ](./ndis-status-wdi-indication-disassociation.md)解除与的解除对应的解除指示参数。

## <a name="tlv-type"></a>TLV 类型


0xBC

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                         | 描述                                                                |
|--------------------------------------------------------------|----------------------------------------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)            | 与解除关联的指示关联的对等方的 MAC 地址。 |
| [**WDI \_ASSOC \_ 状态**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status) (UINT32)  | 解除解除的指示的触发器。                             |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

