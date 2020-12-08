---
title: WDI_TLV_P2P_DISCOVERY_CHANNEL_SETTINGS
description: WDI_TLV_P2P_DISCOVERY_CHANNEL_SETTINGS 是包含 Wi-Fi 直接发现通道设置的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DISCOVERY_CHANNEL_SETTINGS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4d3c13be2475c440b201713d53f60feda66679be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821217"
---
# <a name="wdi_tlv_p2p_discovery_channel_settings"></a>WDI \_ TLV \_ P2P \_ 发现 \_ 通道 \_ 设置


WDI \_ tlv \_ P2P \_ 发现 \_ 通道 \_ 设置是包含 Wi-Fi 直接发现通道设置的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xE8

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                   | 允许多个 TLV 实例 | 可选 | 说明                         |
|------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 侦听 \_ 持续时间**](wdi-tlv-p2p-listen-duration.md) |                                |          | 周期持续时间和侦听时间。 |
| [**WDI \_ TLV \_ 波段 \_ 通道**](wdi-tlv-band-channel.md)                | X                              |          | 要扫描的通道的列表。       |

 

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

 

 




