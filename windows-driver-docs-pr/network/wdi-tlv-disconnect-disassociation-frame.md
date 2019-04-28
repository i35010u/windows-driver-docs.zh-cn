---
title: WDI_TLV_DISCONNECT_DISASSOCIATION_FRAME
description: WDI_TLV_DISCONNECT_DISASSOCIATION_FRAME 是包含接收解除关联帧 TLV。
ms.assetid: 0AE2A543-DA01-4CFB-853D-2511AB18F92C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DISCONNECT_DISASSOCIATION_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 481e698fb094ee5364f700417c9b2f20bf3be22a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347277"
---
# <a name="wditlvdisconnectdisassociationframe"></a>WDI\_TLV\_断开连接\_解除关联\_帧


WDI\_TLV\_断开连接\_解除关联\_帧是包含接收解除关联帧 TLV。

## <a name="tlv-type"></a>TLV 类型


0x38

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                                              |
|-----------|--------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 包含接收解除关联框架 UINT8 元素的数组。 这不包括 802.11 MAC 报头。 |

 

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

 

 




