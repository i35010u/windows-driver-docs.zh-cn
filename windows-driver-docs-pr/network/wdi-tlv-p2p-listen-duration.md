---
title: WDI_TLV_P2P_LISTEN_DURATION
description: WDI_TLV_P2P_LISTEN_DURATION 是包含 Wi-Fi 直接侦听持续时间信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_LISTEN_DURATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 28eecbc37407e4a5be86a659e7011c48a8212650
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818203"
---
# <a name="wdi_tlv_p2p_listen_duration"></a>WDI \_ TLV \_ P2P \_ 侦听 \_ 持续时间


WDI \_ tlv \_ P2P \_ 侦听 \_ 持续时间是一个 tlv，其中包含 Wi-Fi 的直接侦听持续时间信息。

## <a name="tlv-type"></a>TLV 类型


0xE9

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 描述                                                                                                                                                    |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 侦听周期的持续时间（以毫秒为单位）。 此适配器在此期间处于侦听状态。                                                           |
| UINT32 | 适配器预计在侦听周期内主动侦听的持续时间（以毫秒为单位）。 此持续时间必须小于侦听周期持续时间。 |

 

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

 

 




