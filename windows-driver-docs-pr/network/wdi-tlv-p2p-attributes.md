---
title: WDI_TLV_P2P_ATTRIBUTES
description: WDI_TLV_P2P_ATTRIBUTES 是包含 Wi-Fi Direct 属性 TLV。
ms.assetid: 2EC99A30-3D2F-4552-A763-B77E030B5CE5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 757d6df8982cff18c5e7d556f9b41acd884d32a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563217"
---
# <a name="wditlvp2pattributes"></a>WDI\_TLV\_P2P\_ATTRIBUTES


WDI\_TLV\_P2P\_属性是包含 Wi-Fi Direct 属性 TLV。

## <a name="tlv-type"></a>TLV 类型


0x25

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                  | 允许多个 TLV 实例 | 可选 | 描述                                       |
|---------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------|
| [**WDI\_TLV\_P2P\_CAPABILITIES**](wdi-tlv-p2p-capabilities.md)                       |                                |          | Wi-Fi Direct 的功能。                    |
| [**WDI\_TLV\_P2P\_INTERFACE\_ADDRESS\_LIST**](wdi-tlv-p2p-interface-address-list.md) |                                |          | Wi-Fi Direct 接口的 MAC 地址的数组。 |

 

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

 

 




