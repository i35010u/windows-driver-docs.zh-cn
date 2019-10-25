---
title: WDI_TLV_ETHERTYPE_ENCAP_TABLE
description: WDI_TLV_ETHERTYPE_ENCAP_TABLE 是一个 TLV，其中包含关联的 Ethertype 封装。
ms.assetid: BAAC7E5B-F13F-4AC8-A3F9-76197F92C7E3
ms.date: 07/18/2017
keywords:
- WDI_TLV_ETHERTYPE_ENCAP_TABLE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a41a61477b4aea91e1270444d3fcdfe078aa55cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834090"
---
# <a name="wdi_tlv_ethertype_encap_table"></a>WDI\_TLV\_ETHERTYPE\_ENCAP\_表


WDI\_TLV\_ETHERTYPE\_ENCAP\_表是一个 TLV，其中包含关联的 Ethertype 封装。

## <a name="tlv-type"></a>TLV 类型


0x31

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                       | 描述                                                                                                                                                                  |
|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_ETHERTYPE\_封装\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_ethertype_encapsulation_entry)\[\] | [**WDI\_ETHERTYPE\_的数组封装\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_ethertype_encapsulation_entry)元素，这些元素指定关联的 ETHERTYPE 封装。 |

 

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
<td><p>Windows 10</p></td>
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

 

 




