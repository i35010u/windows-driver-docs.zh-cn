---
title: WDI_TLV_ADDITIONAL_PROBE_RESPONSE_IES
description: WDI_TLV_ADDITIONAL_PROBE_RESPONSE_IES 是包含探测响应的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADDITIONAL_PROBE_RESPONSE_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b4dc00ec07ebe5ad1dd5f4b7e06e9a815fcd5cf0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822015"
---
# <a name="wdi_tlv_additional_probe_response_ies"></a>WDI \_ TLV \_ 附加的 \_ 探测 \_ 响应 \_


WDI \_ tlv \_ 额外的 \_ 探测 \_ 响应 \_ 是包含探测响应的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x93

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                                                                                                                                                                                                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 发出的探测响应的数组。 Wi-Fi 直接端口在 Wi-Fi 充当直接设备或组所有者时，必须将这些附加包添加到探测响应数据包中。 当 Wi-Fi 直接端口在客户端模式下操作时，将忽略此成员。 |

 

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

 

 




