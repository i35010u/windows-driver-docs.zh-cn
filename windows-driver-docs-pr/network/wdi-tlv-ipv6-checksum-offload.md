---
title: WDI_TLV_IPV6_CHECKSUM_OFFLOAD
description: WDI_TLV_IPV6_CHECKSUM_OFFLOAD 是包含 IPv6 校验和卸载功能的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IPV6_CHECKSUM_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b70b74f234908f3bd2871c50ba65b5c33faf9e4f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839213"
---
# <a name="wdi_tlv_ipv6_checksum_offload"></a>WDI \_ TLV \_ IPV6 \_ 校验和 \_ 卸载


WDI \_ tlv \_ ipv6 \_ 校验和 \_ 卸载是包含 IPV6 校验和卸载功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xD0

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                                 | 允许多个 TLV 实例 | 可选 | 说明                                  |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------|
| [**WDI \_ TLV \_ 校验和 \_ 卸载 \_ V6 \_ TX \_ 参数**](wdi-tlv-checksum-offload-v6-tx-parameters.md) |                                |          | IPv6 的 Tx 校验和卸载参数。 |
| [**WDI \_ TLV \_ 校验和 \_ 卸载 \_ V6 \_ RX \_ 参数**](wdi-tlv-checksum-offload-v6-rx-parameters.md) |                                |          | IPv6 的 Rx 校验和卸载参数。 |

 

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

 

 




