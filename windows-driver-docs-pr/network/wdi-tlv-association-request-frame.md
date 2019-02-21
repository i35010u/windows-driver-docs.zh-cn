---
title: WDI_TLV_ASSOCIATION_REQUEST_FRAME
description: WDI_TLV_ASSOCIATION_REQUEST_FRAME 是包含关联请求所用的关联 TLV。
ms.assetid: C2323DFE-2B13-4E35-BF9B-4A0B5F3B2076
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_REQUEST_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3ed020c91b3dafcd8490f1a86f850a4d7f21b207
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540500"
---
# <a name="wditlvassociationrequestframe"></a>WDI\_TLV\_ASSOCIATION\_REQUEST\_FRAME


WDI\_TLV\_关联\_请求\_帧是包含关联请求所用的关联 TLV。

## <a name="tlv-type"></a>TLV 类型


0x2E

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                                                                       |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 指定用于关联的关联请求 UINT8 元素的数组。 这不包括 802.11 MAC 报头。 |

 

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

 

 




