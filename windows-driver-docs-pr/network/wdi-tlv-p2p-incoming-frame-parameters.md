---
title: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS
description: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS 是包含传入 Wi-Fi Direct 操作帧参数 TLV。
ms.assetid: 8E530962-E4DC-4845-8A5F-87AC4E000DA8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 40bbfbf0b9f60090e1ba6cf1aa7256ec81388990
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540816"
---
# <a name="wditlvp2pincomingframeparameters"></a>WDI\_TLV\_P2P\_INCOMING\_FRAME\_PARAMETERS


WDI\_TLV\_P2P\_传入\_帧\_参数是包含传入 Wi-Fi Direct 操作帧参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0x7A

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                    | 描述                                        |
|-------------------------------------------------------------------------|----------------------------------------------------|
| [**WDI\_P2P\_ACTION\_FRAME\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/dn926086) | 传入操作框架的类型。             |
| [**WDI\_MAC\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/dn926071)                       | 远程对等方的 MAC 地址。                |
| UINT8                                                                   | Wi-Fi Direct 对话框中的标记的事务。 |

 

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

 

 




