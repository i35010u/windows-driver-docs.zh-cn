---
title: WDI_TLV_BSS_SELECTION_PARAMETERS
description: WDI_TLV_BSS_SELECTION_PARAMETERS 是一种 TLV，其中包含主机用于 BSS 选择的 WDI_BSS_SELECTION_FLAGS。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_SELECTION_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 023f15c07aecfda80a0f5949e68abe1b7d037097
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827477"
---
# <a name="wdi_tlv_bss_selection_parameters"></a>WDI \_ TLV \_ TLV \_ 选择 \_ 参数


WDI \_ tlv \_ BSS \_ 选择 \_ 参数是一个 TLV，其中包含主机用于 BSS 选择的 [**WDI \_ BSS \_ 选择 \_ 标志**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_bss_selection_flags) 。

## <a name="tlv-type"></a>TLV 类型


0x10F

## <a name="length"></a>长度


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 描述                                                                                                     |
|--------|-----------------------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI \_主机用于 BSS 选择的 BSS \_ 选择 \_ 标志**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_bss_selection_flags) 。 |

 

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

 

