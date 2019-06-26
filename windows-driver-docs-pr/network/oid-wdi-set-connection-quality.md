---
title: OID_WDI_SET_CONNECTION_QUALITY
description: OID_WDI_SET_CONNECTION_QUALITY 提供到 IHV 组件强制实施虚拟化的给定端口的连接质量的提示。 此提示允许优化在不同方案中的通道使用的端口。
ms.assetid: 753e25c5-44b5-4afa-8769-49f693472aa9
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_CONNECTION_QUALITY 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e96aabf2a7b13522639d042f016a5aab50852aff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353648"
---
# <a name="oidwdisetconnectionquality"></a>OID\_WDI\_设置\_连接\_质量


OID\_WDI\_设置\_连接\_质量提供到 IHV 组件强制实施虚拟化的给定端口的连接质量的提示。 此提示允许优化在不同方案中的通道使用的端口。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 是                      | 1                               |

 

**请注意**  此属性指定的服务的提示，这可能与其他属性或颁发给适配器的任务导致冲突的数据路径质量。

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                                       | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_连接\_质量\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connection-quality-parameters)                           |                                |          | 所需的 Wi-fi 连接质量提示。                                                                                                                                                     |
| [**WDI\_TLV\_低\_延迟\_连接\_质量\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-low-latency-connection-quality-parameters) |                                | X        | 低延迟连接质量的行为。 这只是所需的连接质量如果设置为[ **WDI\_连接\_质量\_低\_延迟**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_connection_quality_hint)。 |

 

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

 

 




