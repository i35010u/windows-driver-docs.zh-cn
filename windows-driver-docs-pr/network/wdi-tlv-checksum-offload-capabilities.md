---
title: WDI_TLV_CHECKSUM_OFFLOAD_CAPABILITIES
description: WDI_TLV_CHECKSUM_OFFLOAD_CAPABILITIES 是包含 IPv4 和 IPv6 校验和卸载功能的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CHECKSUM_OFFLOAD_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0b8840168cf029652ee676d09266d18c642bf880
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818285"
---
# <a name="wdi_tlv_checksum_offload_capabilities"></a>WDI \_ TLV \_ 校验和 \_ 卸载 \_ 功能


WDI \_ tlv \_ 校验和 \_ 卸载 \_ 功能是一个 tlv，其中包含针对 IPv4 和 IPv6 的校验和卸载功能。

## <a name="tlv-type"></a>TLV 类型


0xCB

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                       | 允许多个 TLV 实例 | 可选 | 说明                           |
|----------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------|
| [**WDI \_ TLV \_ IPV4 \_ 校验和 \_ 卸载**](wdi-tlv-ipv4-checksum-offload.md) |                                |          | 用于卸载 IPv4 校验和的参数。 |
| [**WDI \_ TLV \_ IPV6 \_ 校验和 \_ 卸载**](wdi-tlv-ipv6-checksum-offload.md) |                                |          | 用于 IPv6 校验和卸载的参数。 |

 

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

 

 




