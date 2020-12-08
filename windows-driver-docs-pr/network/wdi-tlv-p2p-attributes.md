---
title: WDI_TLV_P2P_ATTRIBUTES
description: WDI_TLV_P2P_ATTRIBUTES 是包含 Wi-Fi 直接属性的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4e7973fa5ff05981a5a21640c93310b4cfc30914
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823765"
---
# <a name="wdi_tlv_p2p_attributes"></a>WDI \_ TLV \_ P2P \_ 属性


WDI \_ tlv \_ P2P \_ 属性是包含 Wi-Fi 直接属性的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x25

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                  | 允许多个 TLV 实例 | 可选 | 说明                                       |
|---------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 功能**](wdi-tlv-p2p-capabilities.md)                       |                                |          | Wi-Fi 直接功能。                    |
| [**WDI \_ TLV \_ P2P \_ INTERFACE \_ ADDRESS \_ LIST**](wdi-tlv-p2p-interface-address-list.md) |                                |          | Wi-Fi 直接接口 MAC 地址的数组。 |

 

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

 

 




