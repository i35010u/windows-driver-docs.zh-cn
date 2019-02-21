---
title: WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_PARAMETERS
description: WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_PARAMETERS 是包含传入转协商确认参数 TLV。
ms.assetid: 69A20B64-C2B9-4C96-8119-EE64E80201EB
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 47fd457168544483d2c25da2cfe1c38b02a4d0ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519402"
---
# <a name="wditlvp2pgonegotiationconfirmationparameters"></a>WDI\_TLV\_P2P\_转\_协商\_确认\_参数


WDI\_TLV\_P2P\_转\_协商\_确认\_参数是包含传入转协商确认参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0xAA

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入  | 描述                                                                                                                                                          |
|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | Wi-Fi Direct 状态代码，如 Wi-Fi Direct 规范所定义。                                                                                          |
| UINT8 | Wi-Fi Direct 组功能位掩码。 位掩码匹配那些在 Wi-Fi Direct 技术规范的表 13 组功能位图定义中定义。 |
| UINT8 | 在上面的组功能位图位将设置由操作系统中。                                                                                  |

 

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

 

 




