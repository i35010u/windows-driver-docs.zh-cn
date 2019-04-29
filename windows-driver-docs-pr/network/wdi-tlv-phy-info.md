---
title: WDI_TLV_PHY_INFO
description: WDI_TLV_PHY_INFO 是包含 PHY 信息 TLV。
ms.assetid: 3A363FDC-FE79-42C4-AD19-A6B960857CBD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e767a3e1dae77b38c8de8fdadca51c576e82f181
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360587"
---
# <a name="wditlvphyinfo"></a>WDI\_TLV\_PHY\_信息


WDI\_TLV\_PHY\_信息是包含 PHY 信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x26

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                             | 允许多个 TLV 实例 | 可选 | 描述                |
|----------------------------------------------------------------------------------|--------------------------------|----------|----------------------------|
| [**WDI\_TLV\_PHY\_功能**](wdi-tlv-phy-capabilities.md)                  |                                |          | 物理功能中。      |
| [**WDI\_TLV\_PHY\_TX\_POWER\_LEVEL\_LIST**](wdi-tlv-phy-tx-power-level-list.md) |                                |          | TX 电源级别的列表。 |
| [**WDI\_TLV\_PHY\_DATA\_RATE\_LIST**](wdi-tlv-phy-data-rate-list.md)            |                                |          | 数据速率的列表。      |

 

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

 

 




