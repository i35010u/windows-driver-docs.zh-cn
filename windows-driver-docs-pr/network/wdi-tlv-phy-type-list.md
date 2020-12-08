---
title: WDI_TLV_PHY_TYPE_LIST
description: WDI_TLV_PHY_TYPE_LIST 是包含 PHY 类型数组的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_TYPE_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 55f8e294b8e9ad2bb403bfb62bc5e02669e0f9af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818073"
---
# <a name="wdi_tlv_phy_type_list"></a>WDI \_ TLV \_ PHY \_ 类型 \_ 列表


WDI \_ tlv \_ PHY \_ 类型 \_ 列表是包含 PHY 类型数组的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x19

## <a name="length"></a>长度


[**WDI \_ PHY \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type)值数组的大小 (以字节为单位) 。 数组必须包含1个或更多值。

## <a name="values"></a>值


| 类型                                            | 描述                  |
|-------------------------------------------------|------------------------------|
| [**WDI \_ PHY \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type)\[\] | PHY 类型值的数组。 |

 

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

 

