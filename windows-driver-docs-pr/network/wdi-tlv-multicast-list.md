---
title: WDI_TLV_MULTICAST_LIST
description: WDI_TLV_MULTICAST_LIST 是包含多播 MAC 地址数组的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_MULTICAST_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8dbe621cb9a8c2d9117c28d687a022273c6613f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803655"
---
# <a name="wdi_tlv_multicast_list"></a>WDI \_ TLV \_ 多播 \_ 列表


WDI \_ tlv \_ 多播 \_ 列表是一个 tlv，其中包含多播 MAC 地址的数组。

## <a name="tlv-type"></a>TLV 类型


0x6A

## <a name="length"></a>长度


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构数组的大小 (以字节为单位) 。 数组必须包含1个或多个结构。

## <a name="values"></a>值


| 类型                                                  | 描述                          |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

