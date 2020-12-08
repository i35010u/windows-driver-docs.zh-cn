---
title: OID_WDI_TCP_RSC_STATISTICS
description: OID_WDI_TCP_RSC_STATISTICS 是一种用于查询硬件的 RSC 统计信息的 get 命令。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TCP_RSC_STATISTICS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 92648deaef1bb04e38bf8c0398758131625fd0b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797993"
---
# <a name="oid_wdi_tcp_rsc_statistics"></a>OID \_ WDI \_ TCP \_ RSC \_ 统计信息


OID \_ WDI \_ TCP \_ RSC \_ statistics 是查询硬件的 RSC 统计信息的 get 命令。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 否                       | 1                               |

 

## <a name="get-property-parameters"></a>获取属性参数


无其他参数。 标头中的数据足够了。
## <a name="get-property-results"></a>获取属性结果


| TLV                                                                                              | 允许多个 TLV 实例 | 可选 | 说明                         |
|--------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI \_ TLV \_ TCP \_ RSC \_ STATISTICS \_ 参数**](./wdi-tlv-tcp-rsc-statistics-parameters.md) |                                |          | 硬件的 TCP RSC 统计信息。 |

 

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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

