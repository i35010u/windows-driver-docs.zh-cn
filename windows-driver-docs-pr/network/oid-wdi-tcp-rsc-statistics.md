---
title: OID_WDI_TCP_RSC_STATISTICS
description: OID_WDI_TCP_RSC_STATISTICS 是查询硬件的 RSC 统计信息的 get 命令。
ms.assetid: 9079DD03-597D-4B6D-8515-ECF5DAC2A41A
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TCP_RSC_STATISTICS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 846685e243184bacd5875080ece94f4062d3bb3f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362881"
---
# <a name="oidwditcprscstatistics"></a>OID\_WDI\_TCP\_RSC\_STATISTICS


OID\_WDI\_TCP\_RSC\_统计信息是一个 get 命令，查询硬件的 RSC 统计信息。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 否                       | 1                               |

 

## <a name="get-property-parameters"></a>获取属性参数


任何其他参数。 标头中的数据就足够了。
## <a name="get-property-results"></a>获取属性的结果


| TLV                                                                                              | 允许多个 TLV 实例 | 可选 | 描述                         |
|--------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_TCP\_RSC\_STATISTICS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-tcp-rsc-statistics-parameters) |                                |          | TCP RSC 的硬件的统计信息。 |

 

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

 

 




