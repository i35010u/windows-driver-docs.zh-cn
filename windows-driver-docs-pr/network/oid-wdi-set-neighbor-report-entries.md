---
title: OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES
description: OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES 发送邻居报表从 AP 接收到 LE 的列表。 这是发送只要 UE 接收从当前连接的 AP 邻居报表。
ms.assetid: F77FDA4A-3029-4F6E-A82E-B318543484FF
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 583432f989fe79c2eacafc8bf486f4912ea5134a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330168"
---
# <a name="oidwdisetneighborreportentries"></a>OID\_WDI\_设置\_邻居\_报表\_条目


OID\_WDI\_设置\_邻居\_报表\_条目发送的邻居报表从 AP 接收到 LE 列表。 这是发送只要 UE 接收从当前连接的 AP 邻居报表。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 否                       | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                             | 允许多个 TLV 实例 | 可选 | 描述                   |
|---------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------|
| [**WDI\_TLV\_邻居\_报表\_条目**](https://msdn.microsoft.com/library/windows/hardware/mt269133) | X                              |          | 相邻的报表的列表。 |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




