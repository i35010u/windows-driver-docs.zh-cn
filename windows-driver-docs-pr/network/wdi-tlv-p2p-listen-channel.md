---
title: WDI_TLV_P2P_LISTEN_CHANNEL
description: WDI_TLV_P2P_LISTEN_CHANNEL 是包含 Wi-Fi 直接通道信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_LISTEN_CHANNEL 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bd140f670a084f1d4cad20c3b701cbc523c32a88
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818211"
---
# <a name="wdi_tlv_p2p_listen_channel"></a>WDI \_ TLV \_ P2P \_ 侦听 \_ 通道


WDI \_ tlv \_ P2P \_ 侦听 \_ 通道是包含 Wi-Fi 直接通道信息的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x114

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                          | 描述                                                                        |
|-------------------------------|------------------------------------------------------------------------------------|
| UINT8 \[ 3\]                    | 操作类和频道号有效的国家或地区代码。 |
| UINT8                         | 频道号的操作类/频带。                         |
| WDI \_ 信道 \_ 号 (UINT32)  | Wi-Fi 直接设备或组的频道号。                           |

 

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

 

 




