---
title: WDI_TLV_ETHERTYPE_ENCAP_TABLE
description: WDI_TLV_ETHERTYPE_ENCAP_TABLE 是包含关联 Ethertype 封装 TLV。
ms.assetid: BAAC7E5B-F13F-4AC8-A3F9-76197F92C7E3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ETHERTYPE_ENCAP_TABLE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 10a5c91693127604ab26407550b6ffdc03110564
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358552"
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
| [**WDI\_ETHERTYPE\_封装\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ns-wditypes-_wdi_ethertype_encapsulation_entry)\[\] | 一个数组[ **WDI\_ETHERTYPE\_封装\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ns-wditypes-_wdi_ethertype_encapsulation_entry)指定关联 Ethertype 封装的元素。 |

 

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

 

 




