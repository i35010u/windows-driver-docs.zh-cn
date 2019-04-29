---
title: WDI_TLV_PHY_DATA_RATE_LIST
description: WDI_TLV_PHY_DATA_RATE_LIST 是包含一系列数据速率 TLV。
ms.assetid: FFD28866-4983-4C0B-A74D-4EF9A819571E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_DATA_RATE_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2b22840cac4183b268d79bbba4de7a84e72b2a72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377215"
---
# <a name="wditlvphydataratelist"></a>WDI\_TLV\_PHY\_数据\_速率\_列表


WDI\_TLV\_PHY\_数据\_速率\_列表是包含一系列数据速率 TLV。

## <a name="tlv-type"></a>TLV 类型


0x13

## <a name="length"></a>长度


WDI 的数组的大小 （以字节为单位）\_数据\_速率\_列表元素。 该数组必须包含一个或多个元素。

**请注意**  WDI\_数据\_速率\_列表不是 WDI 结构。 它定义在 WDI TLV 分析器生成器，并仅供文档使用。

 

## <a name="values"></a>值


| 在任务栏的搜索框中键入                      | 描述                                                                                             |
|---------------------------|---------------------------------------------------------------------------------------------------------|
| WDI\_DATA\_RATE\_LIST\[\] | 数据速率数组。 数据速率标志和数据速率值必须包含每个数组中的数据速率。 |

 

WDI\_数据\_速率\_列表包含下列元素。

| 在任务栏的搜索框中键入   | 描述                                                                                   |
|--------|-----------------------------------------------------------------------------------------------|
| UINT8  | 数据速率标志中定义[ **WDI\_数据\_速率\_标志**](https://msdn.microsoft.com/library/windows/hardware/dn897811)。 |
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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




