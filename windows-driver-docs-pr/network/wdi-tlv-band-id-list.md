---
title: WDI_TLV_BAND_ID_LIST
description: WDI_TLV_BAND_ID_LIST 是包含一系列外 Id TLV。
ms.assetid: 415EF9E3-9441-420D-AC8A-0F819369E20E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BAND_ID_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ea968a46b67a86d57aaf695cd63c7aa959870f2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575466"
---
# <a name="wditlvbandidlist"></a>WDI\_TLV\_BAND\_ID\_LIST


WDI\_TLV\_外\_ID\_列表是包含一系列外 Id TLV。

## <a name="tlv-type"></a>TLV 类型


0xB6

## <a name="length"></a>长度


WDI 的数组的大小 （以字节为单位）\_外\_ID (UINT32) 元素。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入              | 描述           |
|-------------------|-----------------------|
| WDI\_BAND\_ID\[\] | 带区 Id 数组。 |

 

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

 

 




