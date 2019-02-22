---
title: OID_WDI_SET_MULTICAST_LIST
description: OID_WDI_SET_MULTICAST_LIST 指定给定的端口的多播的地址列表。 此命令可以在任何时间设置。
ms.assetid: dee41a49-2be2-4364-877c-b2b3bf29e78d
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_MULTICAST_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f82501e01636fc6ec5f6be436dbd6abd15a59003
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533804"
---
# <a name="oidwdisetmulticastlist"></a>OID\_WDI\_SET\_MULTICAST\_LIST


OID\_WDI\_设置\_多播\_列表指定给定的端口的多播的地址列表。 此命令可以在任何时间设置。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

如果列表的大小超过中指定的限制，IHV 组件仅应失败命令[ **WDI\_TLV\_接口\_特性**](https://msdn.microsoft.com/library/windows/hardware/dn897835)。

主机启用多路广播的数据包上端口使用筛选后[OID\_WDI\_设置\_接收\_数据包\_筛选器](oid-wdi-set-receive-packet-filter.md)，设备必须指示接收使用的端口到主机的多路广播列表中的地址相匹配的目标地址的多路广播的帧。 设备必须在处理过程的清除多播的列表[OID\_WDI\_任务\_DOT11\_重置](oid-wdi-task-dot11-reset.md)。 该命令发送与指定没有多播列表后，驱动程序必须清除其多播的列表。 在这种情况下，没有数据包应该指出了除非 OID\_WDI\_设置\_接收\_数据包\_筛选器具有 WDI\_数据包\_筛选器\_所有\_多播位集。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                              | 允许多个 TLV 实例 | 可选 | 描述                                                  |
|------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------|
| [**WDI\_TLV\_MULTICAST\_LIST**](https://msdn.microsoft.com/library/windows/hardware/dn897849) |                                | X        | 多播 MAC 地址列表。 列表不能为空。 |

 

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

 

 




