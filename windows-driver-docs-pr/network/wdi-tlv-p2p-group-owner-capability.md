---
title: WDI_TLV_P2P_GROUP_OWNER_CAPABILITY
description: WDI_TLV_P2P_GROUP_OWNER_CAPABILITY 是 TLV 包含 Wi-Fi Direct 组所有者功能信息。
ms.assetid: 3F07665C-0212-465C-9118-CC213198EFB7
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GROUP_OWNER_CAPABILITY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2e2589209ff877e890b2b403206f6ac65b013c68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392186"
---
# <a name="wditlvp2pgroupownercapability"></a>WDI\_TLV\_P2P\_组\_所有者\_功能


WDI\_TLV\_P2P\_组\_所有者\_功能是包含 Wi-Fi Direct 组所有者功能信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x77

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                                     |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8  | 指定 Wi-Fi Direct 组功能位掩码。 位掩码相匹配的 Wi-fi P2P 技术规范的表 13 组功能位图定义中定义。 |
| UINT8  | 指定上述组功能位图中的操作系统设置的位。                                                                                            |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




