---
title: WDI_TLV_DISCONNECT_DEAUTH_FRAME
description: WDI_TLV_DISCONNECT_DEAUTH_FRAME 是包含接收的 deauthentication 帧 TLV。
ms.assetid: 394B83C7-D001-4816-BC38-42325469863C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DISCONNECT_DEAUTH_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: df28846ec9b8025079dfb1bde63eb7dfa2000f16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522277"
---
# <a name="wditlvdisconnectdeauthframe"></a>WDI\_TLV\_断开连接\_DEAUTH\_帧


WDI\_TLV\_断开连接\_DEAUTH\_帧是包含接收的 deauthentication 帧 TLV。

## <a name="tlv-type"></a>TLV 类型


0x37

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                   |
|-----------|-------------------------------------------------------------------------------|
| UINT8\[\] | 包含接收的 deauthentication 帧 UINT8 元素的数组。 |

 

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

 

 




