---
title: WDI_TLV_HESSID
description: WDI_TLV_HESSID 是包含一系列 HESSIDs TLV。
ms.assetid: 630A1824-7722-4B03-8073-EFC44E142400
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_HESSID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6a7597ebe2a310ca39743944bad5e2123e3fa5da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358539"
---
# <a name="wditlvhessid"></a>WDI\_TLV\_HESSID


WDI\_TLV\_HESSID 是包含一系列 HESSIDs TLV。

## <a name="tlv-type"></a>TLV 类型


0xC8

## <a name="length"></a>长度


数组的大小 （以字节为单位） [ **WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构。 该数组必须包含一个或多个结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                  | 描述        |
|-------------------------------------------------------|--------------------|
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | HESSIDs 的列表。 |

 

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

 

 




