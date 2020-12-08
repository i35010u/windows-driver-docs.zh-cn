---
title: WDI_TLV_P2P_GROUP_OWNER_CAPABILITY
description: WDI_TLV_P2P_GROUP_OWNER_CAPABILITY 是包含 Wi-Fi 直属组所有者功能信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GROUP_OWNER_CAPABILITY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 79d9a4b7698d5992e88c674171bd41ed2c2e3ca1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818271"
---
# <a name="wdi_tlv_p2p_group_owner_capability"></a>WDI \_ TLV \_ P2P \_ 组 \_ 所有者 \_ 功能


WDI \_ tlv \_ P2P \_ 组 \_ 所有者 \_ 功能是一个 tlv，其中包含 Wi-Fi 的直接组所有者功能信息。

## <a name="tlv-type"></a>TLV 类型


0x77

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 描述                                                                                                                                                                     |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8  | 指定 Wi-Fi 的直接分组功能位掩码。 位掩码与 Wi-Fi P2P 技术规范的表13组功能位图定义中定义的位掩码匹配。 |
| UINT8  | 指定操作系统在上述组功能位图中设置的位。                                                                                            |
| UINT32 | 此组所有者的最大客户端计数。                                                                                                                                      |

 

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

 

 




