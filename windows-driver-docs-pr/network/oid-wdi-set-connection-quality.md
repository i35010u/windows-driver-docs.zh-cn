---
title: OID_WDI_SET_CONNECTION_QUALITY
description: OID_WDI_SET_CONNECTION_QUALITY 向 IHV 组件提供了对给定虚拟化端口强制实现连接质量的提示。 此提示允许端口优化不同方案中的通道使用情况。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_CONNECTION_QUALITY 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d8bf45fa12fc0730e6b18377c312a8b1dd82610e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829399"
---
# <a name="oid_wdi_set_connection_quality"></a>OID \_ WDI \_ 设置 \_ 连接 \_ 质量


OID \_ WDI \_ 设置 \_ 连接 \_ 质量向 IHV 组件提供提示，以强制实施给定虚拟化端口的连接质量。 此提示允许端口优化不同方案中的通道使用情况。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

**注意**  此属性指定了服务提示的数据路径质量，这可能会导致与颁发给适配器的其他属性或任务冲突。

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                                       | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 连接 \_ 质量 \_ 参数**](./wdi-tlv-connection-quality-parameters.md)                           |                                |          | 所需的 Wi-Fi 连接质量提示。                                                                                                                                                     |
| [**WDI \_ TLV \_ 低 \_ 延迟 \_ 连接 \_ 质量 \_ 参数**](./wdi-tlv-low-latency-connection-quality-parameters.md) |                                | X        | 低延迟连接质量的行为。 仅当连接质量设置为 [**WDI \_ 连接 \_ 质量 \_ 低 \_ 延迟**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_connection_quality_hint)时，才需要此设置。 |

 

## <a name="set-property-results"></a>设置属性结果


无其他数据。 标头中的数据足够了。

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

 

