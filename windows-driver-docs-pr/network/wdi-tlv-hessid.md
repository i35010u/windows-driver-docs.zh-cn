---
title: WDI_TLV_HESSID
description: WDI_TLV_HESSID 为 TLV，其中包含 HESSIDs 的列表。
ms.assetid: 630A1824-7722-4B03-8073-EFC44E142400
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_HESSID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 269ef52f39d1fd542feb0570ea86eccac394594b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209609"
---
# <a name="wdi_tlv_hessid"></a>WDI \_ TLV \_ HESSID


WDI \_ tlv \_ HESSID 是包含 HESSIDs 列表的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xC8

## <a name="length"></a>Length


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构数组的大小 (以字节为单位) 。 数组必须包含1个或多个结构。

## <a name="values"></a>值


| 类型                                                  | 说明        |
|-------------------------------------------------------|--------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | HESSIDs 的列表。 |

 

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

 

