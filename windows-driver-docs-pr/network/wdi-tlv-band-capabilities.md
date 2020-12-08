---
title: WDI_TLV_BAND_CAPABILITIES
description: WDI_TLV_BAND_CAPABILITIES 是包含带区功能的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BAND_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: aaa88d1095318306264088bac5b8b77fb4d750b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818311"
---
# <a name="wdi_tlv_band_capabilities"></a>WDI \_ TLV \_ 波段 \_ 功能


WDI \_ tlv \_ 波段 \_ 功能是包含带区功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x1A

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 描述                                   |
|--------|-----------------------------------------------|
| UINT32 | 带区的标识符。                  |
| UINT8  | 指定是否启用带区。 |

 

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

 

 




