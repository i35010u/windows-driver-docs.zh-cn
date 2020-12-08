---
title: WDI_TLV_P2P_CHANNEL_NUMBER
description: WDI_TLV_P2P_CHANNEL_NUMBER 是包含 Wi-Fi 直接通道号码信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CHANNEL_NUMBER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1940ca89999426c8faa067b52079956cab488fef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823743"
---
# <a name="wdi_tlv_p2p_channel_number"></a>WDI \_ TLV \_ P2P \_ 信道 \_ 号


WDI \_ tlv \_ P2P \_ 信道 \_ 号是一个 tlv，其中包含 Wi-Fi 直接通道号码信息。

## <a name="tlv-type"></a>TLV 类型


0x82

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

 

 




