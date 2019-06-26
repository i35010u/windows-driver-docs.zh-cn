---
title: WDI_TLV_AUTH_ALGO_LIST
description: WDI_TLV_AUTH_ALGO_LIST 是 TLV 包含身份验证算法的列表。
ms.assetid: 6F5EC21B-C923-45ED-B62E-302D916AABE5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_AUTH_ALGO_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b8043fceaf8e6ce8b59d05eaf2a43580b9387b3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386959"
---
# <a name="wditlvauthalgolist"></a>WDI\_TLV\_AUTH\_ALGO\_LIST


WDI\_TLV\_身份验证\_ALGO\_列表是 TLV 包含身份验证算法的列表。

## <a name="tlv-type"></a>TLV 类型


0x3C

## <a name="length"></a>长度


数组的大小 （以字节为单位） [ **WDI\_身份验证\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm)结构。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                        | 描述                            |
|-------------------------------------------------------------|----------------------------------------|
| [**WDI\_身份验证\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm)\[\] | 身份验证算法的数组。 |

 

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

 

 




