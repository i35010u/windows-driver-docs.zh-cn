---
title: OID_WDI_SET_MULTICAST_LIST
description: OID_WDI_SET_MULTICAST_LIST 指定给定的端口的多播的地址列表。 此命令可以在任何时间设置。
ms.assetid: dee41a49-2be2-4364-877c-b2b3bf29e78d
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_MULTICAST_LIST 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e75b6985c2ddb8def25b852cc2f1f4ac39fc4e71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359215"
---
# <a name="oidwdisetmulticastlist"></a>OID\_WDI\_SET\_MULTICAST\_LIST


OID\_WDI\_设置\_多播\_列表指定给定的端口的多播的地址列表。 此命令可以在任何时间设置。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 是                      | 1                               |

 

如果列表的大小超过中指定的限制，IHV 组件仅应失败命令[ **WDI\_TLV\_接口\_特性**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-interface-attributes)。

主机启用多路广播的数据包上端口使用筛选后[OID\_WDI\_设置\_接收\_数据包\_筛选器](oid-wdi-set-receive-packet-filter.md)，设备必须指示接收使用的端口到主机的多路广播列表中的地址相匹配的目标地址的多路广播的帧。 设备必须在处理过程的清除多播的列表[OID\_WDI\_任务\_DOT11\_重置](oid-wdi-task-dot11-reset.md)。 该命令发送与指定没有多播列表后，驱动程序必须清除其多播的列表。 在这种情况下，没有数据包应该指出了除非 OID\_WDI\_设置\_接收\_数据包\_筛选器具有 WDI\_数据包\_筛选器\_所有\_多播位集。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                              | 允许多个 TLV 实例 | 可选 | 描述                                                  |
|------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------|
| [**WDI\_TLV\_MULTICAST\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-multicast-list) |                                | X        | 多播 MAC 地址列表。 列表不能为空。 |

 

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

 

 




