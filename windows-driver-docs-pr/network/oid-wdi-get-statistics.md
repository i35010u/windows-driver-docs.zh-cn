---
title: OID_WDI_GET_STATISTICS
description: OID_WDI_GET_STATISTICS 请求 IHV 组件返回 MAC 和 PHY 层统计信息。
ms.assetid: 55c36869-ce85-42fe-877b-07aefb669b56
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_STATISTICS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f407ec33f6c5c695b3f6cefcce4434edd21b15ca
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215839"
---
# <a name="oid_wdi_get_statistics"></a>OID \_ WDI \_ 获取 \_ 统计信息


OID \_ WDI \_ 获取 \_ IHV 组件返回 MAC 和 PHY 层统计信息请求的统计信息。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 不支持的设置        | 1                               |

 

MAC 统计信息必须全部按端口维护。 还必须按端口维护 PHY 统计信息，除非免除。 如果在免除) 允许的情况下按端口 (维护 PHY 统计信息，则可以按 "通道" 来维护统计信息，在同一通道上操作的两个端口的每个端口都可以进行维护)  (。

## <a name="get-property-parameters"></a>获取属性参数


无其他参数。 标头中的数据足够了。
## <a name="get-property-results"></a>获取属性结果


| TLV                                                              | 允许多个 TLV 实例 | 可选 | 说明              |
|------------------------------------------------------------------|--------------------------------|----------|--------------------------|
| [**WDI \_ TLV \_ MAC \_ 统计信息**](./wdi-tlv-mac-statistics.md) | X                              |          | 每对等 MAC 统计信息。 |
| [**WDI \_ TLV \_ PHY \_ 统计信息**](./wdi-tlv-phy-statistics.md) | X                              |          | 每端口 PHY 统计信息。 |

 

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

 

