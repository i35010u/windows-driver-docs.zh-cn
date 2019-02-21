---
title: WDI_TLV_VENDOR_SPECIFIC_IE
description: WDI_TLV_VENDOR_SPECIFIC_IE 是包含一系列特定于供应商 IEs TLV。
ms.assetid: 66995086-329A-49F1-B531-2AD2383473CF
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_VENDOR_SPECIFIC_IE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3e6e3edc17f29e77ffd2592746fa2409b6ecca5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524293"
---
# <a name="wditlvvendorspecificie"></a>WDI\_TLV\_供应商\_特定\_IE


WDI\_TLV\_供应商\_特定\_IE 是包含一系列特定于供应商 IEs TLV。

## <a name="tlv-type"></a>TLV 类型


0x5

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                        |
|-----------|--------------------------------------------------------------------|
| UINT8\[\] | 指定特定于供应商 IEs UINT8 元素的数组。 |

 

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

 

 




