---
title: WDI_TLV_STATION_ATTRIBUTES
description: WDI_TLV_STATION_ATTRIBUTES 是工作站的包含特性 TLV。
ms.assetid: CB15D3A4-5B42-44ED-A8A8-3E7F09B65F8B
ms.date: 02/14/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_STATION_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 078cb0e1b477d5ac64b6b0df6a016f4f93a69bca
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902793"
---
# <a name="wditlvstationattributes"></a>WDI\_TLV\_工作站\_属性


WDI\_TLV\_工作站\_属性是包含特性的工作站 TLV。

## <a name="tlv-type"></a>TLV 类型

0x22

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
|--- | --- | --- | --- |
| [**WDI\_TLV\_工作站\_功能**](wdi-tlv-station-capabilities.md) |   |   | 工作站的功能。 |
| [**WDI\_TLV\_UNICAST\_ALGORITHM\_LIST**](wdi-tlv-unicast-algorithm-list.md) |   | X | 支持的单播算法中。 |
| [**WDI\_TLV\_MULTICAST\_DATA\_ALGORITHM\_LIST**](wdi-tlv-multicast-data-algorithm-list.md) |   | X  | 支持多播的数据的算法。 |
| [**WDI\_TLV\_MULTICAST\_MGMT\_ALGORITHM\_LIST**](wdi-tlv-multicast-mgmt-algorithm-list.md) |   | X  | 支持多播的管理算法中。 |

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

 

 




