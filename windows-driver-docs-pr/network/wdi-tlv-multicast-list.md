---
title: WDI_TLV_MULTICAST_LIST
description: WDI_TLV_MULTICAST_LIST 是包含多播 MAC 地址数组的 TLV。
ms.assetid: 5023557A-1BC5-4A4E-A77C-20353C0CA3FD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_MULTICAST_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a3d3bef7a78e9f81f15fd123650d908d3056fd74
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212691"
---
# <a name="wdi_tlv_multicast_list"></a>WDI \_ TLV \_ 多播 \_ 列表


WDI \_ tlv \_ 多播 \_ 列表是一个 tlv，其中包含多播 MAC 地址的数组。

## <a name="tlv-type"></a>TLV 类型


0x6A

## <a name="length"></a>Length


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构数组的大小 (以字节为单位) 。 数组必须包含1个或多个结构。

## <a name="values"></a>值


| 类型                                                  | 说明                          |
|-------------------------------------------------------|--------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | 多播 MAC 地址的数组。 |

 

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

 

