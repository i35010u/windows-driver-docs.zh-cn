---
title: OID_WDI_TCP_RSC_STATISTICS
description: OID_WDI_TCP_RSC_STATISTICS 是一种用于查询硬件的 RSC 统计信息的 get 命令。
ms.assetid: 9079DD03-597D-4B6D-8515-ECF5DAC2A41A
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TCP_RSC_STATISTICS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fb3635c8b0999b97dd8afa3674574ae8b9abff54
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217245"
---
# <a name="oid_wdi_tcp_rsc_statistics"></a>OID \_ WDI \_ TCP \_ RSC \_ 统计信息


OID \_ WDI \_ TCP \_ RSC \_ statistics 是查询硬件的 RSC 统计信息的 get 命令。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

