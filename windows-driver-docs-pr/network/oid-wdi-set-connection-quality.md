---
title: OID_WDI_SET_CONNECTION_QUALITY
description: OID_WDI_SET_CONNECTION_QUALITY 提供到 IHV 组件强制实施虚拟化的给定端口的连接质量的提示。 此提示允许优化在不同方案中的通道使用的端口。
ms.assetid: 753e25c5-44b5-4afa-8769-49f693472aa9
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_CONNECTION_QUALITY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 298e7431ea5e9b150f243a7781a1da62994dbad4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533756"
---
# <a name="oidwdisetconnectionquality"></a>OID\_WDI\_设置\_连接\_质量


OID\_WDI\_设置\_连接\_质量提供到 IHV 组件强制实施虚拟化的给定端口的连接质量的提示。 此提示允许优化在不同方案中的通道使用的端口。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

**请注意**  此属性指定的服务的提示，这可能与其他属性或颁发给适配器的任务导致冲突的数据路径质量。

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                                       | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_连接\_质量\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn926259)                           |                                |          | 所需的 Wi-fi 连接质量提示。                                                                                                                                                     |
| [**WDI\_TLV\_低\_延迟\_连接\_质量\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn897843) |                                | X        | 低延迟连接质量的行为。 这只是所需的连接质量如果设置为[ **WDI\_连接\_质量\_低\_延迟**](https://msdn.microsoft.com/library/windows/hardware/dn897807)。 |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。
要求
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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




