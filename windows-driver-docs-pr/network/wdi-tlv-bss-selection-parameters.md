---
title: WDI_TLV_BSS_SELECTION_PARAMETERS
description: WDI_TLV_BSS_SELECTION_PARAMETERS 是一个 TLV，其中包含主机用于 BSS 选择的 WDI_BSS_SELECTION_FLAGS。
ms.assetid: 5EDA0FAC-DF2E-437B-BB4F-F69468CE856E
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSS_SELECTION_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 48d03a8c68a97df6c7c5a2a441f0ae197807d465
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844490"
---
# <a name="wdi_tlv_bss_selection_parameters"></a>WDI\_TLV\_BSS\_选择\_参数


WDI\_TLV\_BSS\_选择 "\_参数是一个 TLV，其中包含由主机用于 BSS 选择[ **\_标志\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_bss_selection_flags)。\_

## <a name="tlv-type"></a>TLV 类型


0x10F

## <a name="length"></a>Length


UINT32 的大小（以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                                                                                                     |
|--------|-----------------------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI\_bss\_选择\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_bss_selection_flags)了主机用于 BSS 选择的标志。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>支持的最低客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>支持的最低服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




