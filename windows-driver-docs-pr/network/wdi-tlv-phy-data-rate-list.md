---
title: WDI_TLV_PHY_DATA_RATE_LIST
description: WDI_TLV_PHY_DATA_RATE_LIST 是包含数据速率列表的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_DATA_RATE_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: aea5b08f86234118f76ded399dc2cd3380b3fee5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818097"
---
# <a name="wdi_tlv_phy_data_rate_list"></a>WDI \_ TLV \_ PHY \_ 数据 \_ 速率 \_ 列表


WDI \_ tlv \_ PHY \_ 数据 \_ 速率 \_ 列表是包含数据速率列表的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x13

## <a name="length"></a>长度


WDI \_ 数据 \_ 速率列表元素数组的大小，以字节为单位)  (\_ 。 数组必须包含1个或多个元素。

**注意**  WDI \_ 数据 \_ 速率 \_ 列表不是 WDI 结构。 它在 WDI TLV 分析程序生成器中定义，仅用于文档目的。

 

## <a name="values"></a>值


| 类型                      | 描述                                                                                             |
|---------------------------|---------------------------------------------------------------------------------------------------------|
| WDI \_ 数据 \_ 速率 \_ 列表\[\] | 数据速率的数组。 数组中的每个数据速率必须包含数据速率标志和数据速率值。 |

 

WDI \_ 数据 \_ 速率 \_ 列表由以下元素组成。

| 类型   | 描述                                                                                   |
|--------|-----------------------------------------------------------------------------------------------|
| UINT8  | [**WDI \_ 数据 \_ 速率 \_ 标志**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_data_rate_flags)中定义的数据速率标志。 |
| UINT16 | 数据速率值。                                                                          |

 

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

 

