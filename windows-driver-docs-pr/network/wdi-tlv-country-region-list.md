---
title: WDI_TLV_COUNTRY_REGION_LIST
description: WDI_TLV_COUNTRY_REGION_LIST 是 TLV 所在国家或地区代码的列表。
ms.assetid: 675C176F-EE7A-41E0-9770-4D810F29E7BF
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_COUNTRY_REGION_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: defc626f88ee4d9ba0d14e0f0e1a7107c784bf78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544105"
---
# <a name="wditlvcountryregionlist"></a>WDI\_TLV\_国家/地区\_区域\_列表


WDI\_TLV\_国家/地区\_区域\_列表是 TLV 所在国家或地区代码的列表。

## <a name="tlv-type"></a>TLV 类型


0x12

## <a name="length"></a>长度


WDI 的数组的大小 （以字节为单位）\_国家/地区\_区域\_列表元素。 该数组必须包含一个或多个元素。

**请注意**  WDI\_国家/地区\_区域\_列表不是 WDI 结构。 它定义在 WDI TLV 分析器生成器，并仅供文档使用。

 

## <a name="values"></a>值


| 在任务栏的搜索框中键入                           | 描述                          |
|--------------------------------|--------------------------------------|
| WDI\_国家/地区\_区域\_列表\[\] | 国家/地区或区域代码的数组。 |

 

WDI\_国家/地区\_区域\_列表包含下列元素。

| 在任务栏的搜索框中键入       | 描述               |
|------------|---------------------------|
| UINT8\[3\] | 一个国家或地区代码。 |

 

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

 

 




