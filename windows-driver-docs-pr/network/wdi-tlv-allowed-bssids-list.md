---
title: WDI_TLV_ALLOWED_BSSIDS_LIST
description: WDI_TLV_ALLOWED_BSSIDS_LIST 是包含一系列允许关联所使用的 BSSIDs TLV。
ms.assetid: A53C5EB2-1D77-4380-86C7-291D2BF4FCFC
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ALLOWED_BSSIDS_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: aa222b0cd05be2ae522a9467116816cb1481aff3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533810"
---
# <a name="wditlvallowedbssidslist"></a>WDI\_TLV\_ALLOWED\_BSSIDS\_LIST


WDI\_TLV\_允许\_BSSIDS\_列表是包含一系列允许关联所使用的 BSSIDs TLV。

## <a name="tlv-type"></a>TLV 类型


0xC2

## <a name="length"></a>长度


数组的大小 （以字节为单位） [ **WDI\_MAC\_地址**](https://msdn.microsoft.com/library/windows/hardware/dn926071)结构。 该数组必须包含一个或多个结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                  | 描述                                                   |
|-------------------------------------------------------|---------------------------------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/dn926071)\[\] | BSSIDs 允许关联所使用的列表。 |

 

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

 

 




