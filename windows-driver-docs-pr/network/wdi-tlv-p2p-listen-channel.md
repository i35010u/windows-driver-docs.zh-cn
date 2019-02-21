---
title: WDI_TLV_P2P_LISTEN_CHANNEL
description: WDI_TLV_P2P_LISTEN_CHANNEL 是 TLV 包含 Wi-Fi Direct 通道信息。
ms.assetid: 45D1B507-C02B-432B-A552-78F2539ECE68
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_LISTEN_CHANNEL 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c341847563c60271e10069bc971dccf9039d1dde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544570"
---
# <a name="wditlvp2plistenchannel"></a>WDI\_TLV\_P2P\_侦听\_通道


WDI\_TLV\_P2P\_侦听\_通道是 TLV 包含 Wi-Fi Direct 通道信息。

## <a name="tlv-type"></a>TLV 类型


0x114

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                          | 描述                                                                        |
|-------------------------------|------------------------------------------------------------------------------------|
| UINT8\[3\]                    | 国家 / 地区代码的操作的类和频道号都有效。 |
| UINT8                         | 表示频道号的运行频率类/带区。                         |
| WDI\_通道\_数 (UINT32) | 为 Wi-Fi Direct 设备或组频道号。                           |

 

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
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




