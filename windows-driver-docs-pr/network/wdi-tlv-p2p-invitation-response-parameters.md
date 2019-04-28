---
title: WDI_TLV_P2P_INVITATION_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_INVITATION_RESPONSE_PARAMETERS 是 TLV 包含 Wi-Fi Direct 邀请响应参数。
ms.assetid: A242F40C-D062-4A62-8F47-E42E74EAEFE8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INVITATION_RESPONSE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f49c1abdd25504eaedd2eee10dec81f3d19dfffc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347240"
---
# <a name="wditlvp2pinvitationresponseparameters"></a>WDI\_TLV\_P2P\_邀请\_响应\_参数


WDI\_TLV\_P2P\_邀请\_响应\_参数是包含 Wi-Fi Direct 邀请响应参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0x80

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                    |
|--------|--------------------------------------------------------------------------------|
| UINT8  | Wi-Fi Direct 状态代码，指定 Wi-Fi Direct 规范的... |
| UINT16 | 转到配置超时，以毫秒为单位。                                 |
| UINT16 | 客户端配置超时，以毫秒为单位。                             |

 

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

 

 




