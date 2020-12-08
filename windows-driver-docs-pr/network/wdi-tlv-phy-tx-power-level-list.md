---
title: WDI_TLV_PHY_TX_POWER_LEVEL_LIST
description: WDI_TLV_PHY_TX_POWER_LEVEL_LIST 是包含电源级别列表的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_TX_POWER_LEVEL_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 32534e88cbed49368aac27b2b63b1dc49df7134b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818071"
---
# <a name="wdi_tlv_phy_tx_power_level_list"></a>WDI \_ TLV \_ PHY \_ TX \_ 电源 \_ 级别 \_ 列表


WDI \_ tlv \_ PHY \_ TX \_ power \_ LEVEL \_ list 是包含电源级别列表的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x1C

## <a name="length"></a>长度


UINT32 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型       | 描述                                              |
|------------|----------------------------------------------------------|
| UINT32\[\] | 指定电源级别的 UINT32 元素数组。 |

 

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

 

 




