---
title: WDI_TLV_IHV_NON_WDI_OIDS_LIST
description: WDI_TLV_IHV_NON_WDI_OIDS_LIST 是包含列表的非-WDI Oid 适配器要播发到操作系统 TLV。
ms.assetid: 84929276-F098-4C24-A499-E252D5FB71A6
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IHV_NON_WDI_OIDS_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3d031a2495a8cedf6195ac4ea9438862a3c8b029
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365386"
---
# <a name="wditlvihvnonwdioidslist"></a>WDI\_TLV\_IHV\_非\_WDI\_OID\_列表


WDI\_TLV\_IHV\_非\_WDI\_OID\_列表是包含列表的非-WDI Oid 适配器要播发到操作系统 TLV。

## <a name="tlv-type"></a>TLV 类型


0x104

## <a name="length"></a>长度


UINT32 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入       | 描述                                                                                                                                                                                       |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32\[\] | 列表的非-WDI Oid 适配器要播发到操作系统。 适配器不应假定操作系统已筛选非-WDI Oid 以匹配此列表。 |

 

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

 

 




