---
title: WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY
description: WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY 是包含 Wi-Fi 直接播发前缀项的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bfdaba8b430f66a3f5f0377334fb0432a5a444cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823795"
---
# <a name="wdi_tlv_p2p_advertised_prefix_entry"></a>WDI \_ TLV \_ P2P \_ 播发 \_ 前缀 \_ 条目


WDI \_ tlv \_ P2P \_ 播发 \_ 前缀 \_ 条目是包含 Wi-Fi 直接播发前缀条目的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x110

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                        | 允许多个 TLV 实例 | 可选 | 说明                                                      |
|-----------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 名称**](wdi-tlv-p2p-service-name.md)            |                                |          | 以 UTF-8 表示的服务名称，最大大小为255字节。 |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 名称 \_ 哈希**](wdi-tlv-p2p-service-name-hash.md) |                                |          | 服务名称哈希。                                            |

 

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

 

 




