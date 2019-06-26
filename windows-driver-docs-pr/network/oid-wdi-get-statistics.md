---
title: OID_WDI_GET_STATISTICS
description: OID_WDI_GET_STATISTICS 请求 IHV 组件返回 MAC 和物理层统计信息。
ms.assetid: 55c36869-ce85-42fe-877b-07aefb669b56
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_STATISTICS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c141b531a070cac0f892077061caaaa1f742ca62
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387266"
---
# <a name="oidwdigetstatistics"></a>OID\_WDI\_GET\_STATISTICS


OID\_WDI\_获取\_统计信息请求 IHV 组件返回 MAC 和物理层的统计信息。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 不支持 set 语句        | 1                               |

 

MAC 统计信息必须所有维护每个端口。 除非被免除，还必须给每个端口维护物理统计信息。 如果每个端口 （如允许的例外） 不能维护物理统计信息，可以每个"通道"维护统计信息 （可组合在同一个通道上运行的两个端口的物理统计信息）。

## <a name="get-property-parameters"></a>获取属性参数


任何其他参数。 标头中的数据就足够了。
## <a name="get-property-results"></a>获取属性的结果


| TLV                                                              | 允许多个 TLV 实例 | 可选 | 描述              |
|------------------------------------------------------------------|--------------------------------|----------|--------------------------|
| [**WDI\_TLV\_MAC\_STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-mac-statistics) | X                              |          | 每个对等的 MAC 统计信息。 |
| [**WDI\_TLV\_PHY\_STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-phy-statistics) | X                              |          | 每个端口的物理统计信息。 |

 

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

 

 




