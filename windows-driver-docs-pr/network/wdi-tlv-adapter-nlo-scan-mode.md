---
title: WDI_TLV_ADAPTER_NLO_SCAN_MODE
description: WDI_TLV_ADAPTER_NLO_SCAN_MODE 是一种 TLV，用于指示是在主动还是被动模式下执行扫描。
ms.assetid: 4294AF4D-587E-4978-9C54-E11D7368FBB8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADAPTER_NLO_SCAN_MODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: be8cd30a92924f013717708c650b53da962bb8f1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213126"
---
# <a name="wdi_tlv_adapter_nlo_scan_mode"></a>WDI \_ TLV \_ 适配器 \_ NLO \_ 扫描 \_ 模式


WDI \_ tlv \_ 适配器 \_ NLO \_ SCAN \_ 模式是一种 tlv，用于指示是在主动还是被动模式下执行扫描。

## <a name="tlv-type"></a>TLV 类型


0x125

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                                                                                                                     |
|--------|---------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI \_指示 \_ **](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_scan_type) 是否应在主动或被动模式下执行扫描的扫描类型值。 |

 

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

 

