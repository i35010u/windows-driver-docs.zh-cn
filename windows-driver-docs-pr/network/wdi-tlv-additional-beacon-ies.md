---
title: WDI_TLV_ADDITIONAL_BEACON_IES
description: WDI_TLV_ADDITIONAL_BEACON_IES 是一种 TLV，其中包含附加的信号。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADDITIONAL_BEACON_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 43c14957245a02ce40afa84f6944725571d7dcc6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822037"
---
# <a name="wdi_tlv_additional_beacon_ies"></a>WDI \_ TLV \_ 附加的 \_ 信标 \_


WDI \_ tlv \_ 附加的 \_ 信标 \_ 是包含其他信号的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x98

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                                                                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 信标的数组。 Wi-Fi 直接端口在作为组所有者时，必须将这些附加的添加到信号数据包中。 当 Wi-Fi 直接端口在设备或客户端模式下操作时，将忽略这些操作。 |

 

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

 

 




