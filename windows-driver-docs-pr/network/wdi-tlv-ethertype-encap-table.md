---
title: WDI_TLV_ETHERTYPE_ENCAP_TABLE
description: WDI_TLV_ETHERTYPE_ENCAP_TABLE 是包含关联 Ethertype 封装 TLV。
ms.assetid: BAAC7E5B-F13F-4AC8-A3F9-76197F92C7E3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ETHERTYPE_ENCAP_TABLE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 09984b650f05b0c6b455ac3a308f1bc7a8cc1e5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380869"
---
# <a name="wditlvethertypeencaptable"></a>WDI\_TLV\_ETHERTYPE\_ENCAP\_TABLE


WDI\_TLV\_ETHERTYPE\_封闭\_表是包含关联 Ethertype 封装 TLV。

## <a name="tlv-type"></a>TLV 类型


0x31

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                       | 描述                                                                                                                                                                  |
|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_ETHERTYPE\_封装\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn897818)\[\] | 一个数组[ **WDI\_ETHERTYPE\_封装\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn897818)指定关联 Ethertype 封装的元素。 |

 

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

 

 




