---
title: WDI_TLV_LSO_V2_CAPABILITIES
description: WDI_TLV_LSO_V2_CAPABILITIES 是包含大量发送卸载 V2 功能的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_LSO_V2_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 70d4553ca086eddd9bb08a62533b4084d2ad880a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809873"
---
# <a name="wdi_tlv_lso_v2_capabilities"></a>WDI \_ TLV \_ LSO \_ V2 \_ 功能


WDI \_ tlv \_ LSO \_ v2 \_ 功能是包含大量发送卸载 V2 功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xCD

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                   | 允许多个 TLV 实例 | 可选 | 说明                                  |
|--------------------------------------------------------|--------------------------------|----------|----------------------------------------------|
| [**WDI \_ TLV \_ IPV4 \_ LSO \_ V2**](wdi-tlv-ipv4-lso-v2.md) |                                |          | 适用于 IPv4 的大型发送卸载 V2 功能。 |
| [**WDI \_ TLV \_ IPV6 \_ LSO \_ V2**](wdi-tlv-ipv6-lso-v2.md) |                                |          | IPv6 的大型发送卸载 V2 功能。 |

 

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

 

 




