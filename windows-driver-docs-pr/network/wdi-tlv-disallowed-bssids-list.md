---
title: WDI_TLV_DISALLOWED_BSSIDS_LIST
description: WDI_TLV_DISALLOWED_BSSIDS_LIST 是一种 TLV，其中包含不允许用于关联的 BSSIDs 的列表。
ms.assetid: A65A6C05-C4E1-4880-BF83-48B62D0C2FD3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DISALLOWED_BSSIDS_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 73208f8f1f461fb3899c69886d949a1ac33ec6e6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216807"
---
# <a name="wdi_tlv_disallowed_bssids_list"></a>WDI \_ TLV 不 \_ 允许 \_ BSSIDS \_ 列表


WDI \_ tlv 不 \_ 允许 \_ BSSIDS \_ 列表是一个 TLV，其中包含不允许用于关联的 BSSIDS 列表。

## <a name="tlv-type"></a>TLV 类型


0xC3

## <a name="length"></a>Length


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构数组的大小 (以字节为单位) 。 数组必须包含1个或多个结构。

## <a name="values"></a>值


| 类型                                                  | 说明                                                                                                                                               |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | 不允许用于关联的 BSSIDs 的列表。 如果指定此项，则适配器不得关联到不在此列表中的任何 AP |

 

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

 

