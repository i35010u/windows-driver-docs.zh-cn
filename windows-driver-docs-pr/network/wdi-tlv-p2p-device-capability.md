---
title: WDI_TLV_P2P_DEVICE_CAPABILITY
description: WDI_TLV_P2P_DEVICE_CAPABILITY 是包含 Wi-Fi 直接设备功能的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_CAPABILITY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 33240a82f4c9be80acd9ac8342db671b496c57dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823731"
---
# <a name="wdi_tlv_p2p_device_capability"></a>WDI \_ TLV \_ P2P \_ 设备 \_ 功能


WDI \_ tlv \_ P2P \_ 设备 \_ 功能是包含 Wi-Fi 直接设备功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x84

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 描述                                                                                                                     |
|--------|---------------------------------------------------------------------------------------------------------------------------------|
| UINT8  | Wi-Fi 直接设备功能的位图，如 Wi-Fi 直接技术规范的表12中所定义。            |
| UINT8  | 上述设备功能位图中的 Wi-Fi 直接功能的位图，当前由操作系统设置。 |
| UINT32 | 一个位掩码，指示启用了哪些 WPS 版本。                                                                        |

 

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

 

 




