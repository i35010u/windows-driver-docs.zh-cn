---
title: WDI_TLV_P2P_SERVICE_NAME
description: WDI_TLV_P2P_SERVICE_NAME 是 TLV，其中包含服务的名称。
ms.assetid: 6394F781-BFE7-4009-8F5E-72D7C8CCF036
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SERVICE_NAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: adaeec3ca664978df0c1e00677a75346e12389b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375650"
---
# <a name="wditlvp2pservicename"></a>WDI\_TLV\_P2P\_SERVICE\_NAME


WDI\_TLV\_P2P\_服务\_名称是 TLV，其中包含服务的名称。

## <a name="tlv-type"></a>TLV 类型


0xEC

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                         |
|-----------|-----------------------------------------------------|
| UINT8\[\] | 中-8，最多 255 个字节的服务的名称。 |

 

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

 

 




