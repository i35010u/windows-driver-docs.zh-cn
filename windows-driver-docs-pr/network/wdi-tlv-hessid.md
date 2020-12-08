---
title: WDI_TLV_HESSID
description: WDI_TLV_HESSID 为 TLV，其中包含 HESSIDs 的列表。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_HESSID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a7fb5039b7bbd91120d7403f9ea5b9561d93d6e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791309"
---
# <a name="wdi_tlv_hessid"></a>WDI \_ TLV \_ HESSID


WDI \_ tlv \_ HESSID 是包含 HESSIDs 列表的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xC8

## <a name="length"></a>长度


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构数组的大小 (以字节为单位) 。 数组必须包含1个或多个结构。

## <a name="values"></a>值


| 类型                                                  | 描述        |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

