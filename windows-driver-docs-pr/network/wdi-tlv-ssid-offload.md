---
title: WDI_TLV_SSID_OFFLOAD
description: WDI_TLV_SSID_OFFLOAD 是一种 TLV，其中包含有关 SSID 的 SSID 和提示。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SSID_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 93dd7075f2156def950a9eedcafb01fa659f0171
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821969"
---
# <a name="wdi_tlv_ssid_offload"></a>WDI \_ TLV \_ SSID \_ 卸载


WDI \_ tlv \_ ssid \_ 卸载是一个 tlv，其中包含有关 ssid 的 ssid 和提示。

## <a name="tlv-type"></a>TLV 类型


0x9E

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                         | 允许多个 TLV 实例 | 可选 | 说明                 |
|------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI \_ TLV \_ SSID**](wdi-tlv-ssid.md)                                       |                                |          | SSID。                   |
| [**WDI \_ TLV \_ 单播 \_ 算法 \_ 列表**](wdi-tlv-unicast-algorithm-list.md) |                                |          | 单播算法列表。 |
| [**WDI \_ TLV \_ 通道 \_ 列表**](wdi-tlv-channel-list.md)                      |                                |          | 通道列表。           |

 

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

 

 




