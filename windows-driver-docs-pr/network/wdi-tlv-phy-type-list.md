---
title: WDI_TLV_PHY_TYPE_LIST
description: WDI_TLV_PHY_TYPE_LIST 是包含 PHY 类型数组的 TLV。
ms.assetid: 4066E4CE-D63E-4499-AE27-11F6BD57795D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_TYPE_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f64daedc932f9389ef357ff8b8b883462640186a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216502"
---
# <a name="wdi_tlv_phy_type_list"></a>WDI \_ TLV \_ PHY \_ 类型 \_ 列表


WDI \_ tlv \_ PHY \_ 类型 \_ 列表是包含 PHY 类型数组的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x19

## <a name="length"></a>Length


[**WDI \_ PHY \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type)值数组的大小 (以字节为单位) 。 数组必须包含1个或更多值。

## <a name="values"></a>值


| 类型                                            | 说明                  |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

