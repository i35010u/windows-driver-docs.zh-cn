---
title: OID_WDI_SET_ENCAPSULATION_OFFLOAD
description: 操作系统将发送 OID_WDI_SET_ENCAPSULATION_OFFLOAD，以指示下边缘驱动程序 (LE) 应开始执行 TCP 校验和/LSO 卸载。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ENCAPSULATION_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 414d5cfa43599b5623e0e73ac0475937401c8064
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829385"
---
# <a name="oid_wdi_set_encapsulation_offload"></a>OID \_ WDI \_ 集 \_ 封装 \_ 卸载


OID \_ WDI \_ 将 \_ \_ 由 OS 发送封装卸载，以指示 (LE) 下边缘驱动程序应开始执行 TCP 校验和/LSO 卸载。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

收到此消息时，该 LE 应指示其当前的封装卸载配置，其中 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 任务 \_ 卸载 \_ 当前 \_ 配置](ndis-status-wdi-indication-task-offload-current-config.md)。 对于接收操作，该 LE 不应在其收到 OID \_ WDI \_ SET \_ 封装 \_ 卸载消息之后启动校验和卸载。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                                   | 允许多个 TLV 实例 | 可选 | 说明                                     |
|-----------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------|
| [**WDI \_ TLV \_ 设置 \_ 封装 \_ 卸载 \_ V4 \_ 参数**](./wdi-tlv-set-encapsulation-offload-v4-parameters.md) |                                |          | 指定是否应启动 IPv4 卸载。 |
| [**WDI \_ TLV \_ 设置 \_ 封装 \_ 卸载 \_ V6 \_ 参数**](./wdi-tlv-set-encapsulation-offload-v6-parameters.md) |                                |          | 指定是否应启动 IPv6 卸载。 |

 

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

 

