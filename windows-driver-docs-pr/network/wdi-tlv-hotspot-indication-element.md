---
title: WDI_TLV_HOTSPOT_INDICATION_ELEMENT
description: WDI_TLV_HOTSPOT_INDICATION_ELEMENT 是包含关联请求中使用的热点指示元素 TLV。
ms.assetid: 7A5B61B5-DFFF-4525-A6CD-2AC2822D8B86
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_HOTSPOT_INDICATION_ELEMENT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 401838ba9bdc70c879b351199d946700047d29cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324281"
---
# <a name="wditlvhotspotindicationelement"></a>WDI\_TLV\_热点\_指示\_元素


WDI\_TLV\_热点\_指示\_元素是包含关联请求中使用的热点指示元素 TLV。

## <a name="tlv-type"></a>TLV 类型


0x101

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                         |
|-----------|---------------------------------------------------------------------|
| UINT8\[\] | 关联请求中使用一个热点指示元素。 |

 

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

 

 




