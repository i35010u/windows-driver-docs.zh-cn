---
title: WDI_TLV_PHY_DATA_RATE_LIST
description: WDI_TLV_PHY_DATA_RATE_LIST 是包含数据速率列表的 TLV。
ms.assetid: FFD28866-4983-4C0B-A74D-4EF9A819571E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_DATA_RATE_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0b91d79caa6614493e4a67f2f6b530a6e6bdcd60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838015"
---
# <a name="wdi_tlv_phy_data_rate_list"></a>WDI\_TLV\_PHY\_数据\_速率\_列表


WDI\_TLV\_PHY\_数据\_速率\_列表是包含数据速率列表的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x13

## <a name="length"></a>长度


WDI 数组的大小（以字节为单位）\_数据\_速率\_列表元素。 数组必须包含1个或多个元素。

**请注意**  WDI\_DATA\_RATE\_列表不是 WDI 结构。 它在 WDI TLV 分析程序生成器中定义，仅用于文档目的。

 

## <a name="values"></a>值


| 在任务栏的搜索框中键入                      | 描述                                                                                             |
|---------------------------|---------------------------------------------------------------------------------------------------------|
| WDI\_数据\_速率\_列表\[\] | 数据速率的数组。 数组中的每个数据速率必须包含数据速率标志和数据速率值。 |

 

WDI\_数据\_速率\_列表包含以下元素。

| 在任务栏的搜索框中键入   | 描述                                                                                   |
|--------|-----------------------------------------------------------------------------------------------|
| UINT8  | WDI 中定义的数据速率标志[ **\_数据\_速率\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_data_rate_flags)。 |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




