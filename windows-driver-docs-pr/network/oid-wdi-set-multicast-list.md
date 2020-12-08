---
title: OID_WDI_SET_MULTICAST_LIST
description: OID_WDI_SET_MULTICAST_LIST 指定给定端口的多播地址列表。 此命令可随时设置。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_MULTICAST_LIST 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e5925b484eda4c97815b041e1e402aa5cd7ecb60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829367"
---
# <a name="oid_wdi_set_multicast_list"></a>OID \_ WDI \_ SET \_ 多播 \_ 列表


OID \_ WDI \_ SET \_ 多播 \_ list 指定给定端口的多播地址列表。 此命令可随时设置。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

如果列表大小超过 [**WDI \_ TLV \_ INTERFACE \_ 属性**](./wdi-tlv-interface-attributes.md)中指定的限制，则 IHV 组件只应使命令失败。

主机使用 [OID \_ WDI \_ 设置 \_ 接收 \_ 数据包 \_ 筛选器](oid-wdi-set-receive-packet-filter.md)在端口上启用多播数据包筛选后，设备必须指示接收到的多播帧，其目标地址与端口的多播列表中的某个地址匹配。 在处理 [OID \_ WDI \_ 任务 \_ DOT11 \_ 重置](oid-wdi-task-dot11-reset.md)过程中，设备必须清除多播列表。 如果在未指定多播列表的情况下发送命令，驱动程序必须清除其多播列表。 在这种情况下，除非 OID \_ WDI \_ set \_ 接收 \_ 数据包 \_ 筛选器已设置了 WDI \_ 数据包 \_ 筛选器 \_ \_ ，否则不会指示数据包。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                              | 允许多个 TLV 实例 | 可选 | 说明                                                  |
|------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------|
| [**WDI \_ TLV \_ 多播 \_ 列表**](./wdi-tlv-multicast-list.md) |                                | X        | 多播 MAC 地址的列表。 列表不得为空。 |

 

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

 

