---
title: WDI_TLV_P2P_DISCOVERY_CHANNEL_SETTINGS
description: WDI_TLV_P2P_DISCOVERY_CHANNEL_SETTINGS 是包含 Wi-Fi Direct 发现通道设置 TLV。
ms.assetid: 50BD3F70-4C12-4984-8E3F-AEC9F5C3CDCA
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DISCOVERY_CHANNEL_SETTINGS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c2b2dbe8ebd052196883ddea5cbf1e3500129f10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362487"
---
# <a name="wditlvp2pdiscoverychannelsettings"></a>WDI\_TLV\_P2P\_发现\_通道\_设置


WDI\_TLV\_P2P\_发现\_通道\_设置是包含 Wi-Fi Direct 发现通道设置 TLV。

## <a name="tlv-type"></a>TLV 类型


0xE8

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                   | 允许多个 TLV 实例 | 可选 | 描述                         |
|------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_P2P\_侦听\_持续时间**](wdi-tlv-p2p-listen-duration.md) |                                |          | 周期持续时间和侦听时间。 |
| [**WDI\_TLV\_BAND\_CHANNEL**](wdi-tlv-band-channel.md)                | X                              |          | 要扫描的频道的列表。       |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




