---
title: WDI_TLV_EXTRA_ASSOCIATION_REQUEST_IES
description: WDI_TLV_EXTRA_ASSOCIATION_REQUEST_IES 是包含的信息必须包括在发送端口关联请求的元素 (IEs) TLV。
ms.assetid: 2275B8F2-1FE4-4518-AD67-E9A65F2F37DA
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_EXTRA_ASSOCIATION_REQUEST_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e79a43bf6c1f1c8c5e3b93b9039252e90e581f4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566811"
---
# <a name="wditlvextraassociationrequesties"></a>WDI\_TLV\_EXTRA\_ASSOCIATION\_REQUEST\_IES


WDI\_TLV\_额外\_关联\_请求\_导致浏览器是包含的信息必须包括在发送端口关联请求的元素 (IEs) TLV。

## <a name="tlv-type"></a>TLV 类型


0x40

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                                                                                                                                                                               |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素数组，其中包含必须包括在发送端口关联请求导致浏览器。 这些是适用于任何设备相关联的 BSSID。 它们应使用除常见和 BSSID 特定导致浏览器。 |

 

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

 

 




