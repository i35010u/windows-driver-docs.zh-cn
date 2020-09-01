---
title: OID_WDI_SET_TCP_OFFLOAD_PARAMETERS
description: 将 OID_WDI_SET_TCP_OFFLOAD_PARAMETERS 从操作系统发送到设备，以设置 TCP 卸载参数。
ms.assetid: B615066B-3871-4445-8397-B41CB66EEF35
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_TCP_OFFLOAD_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 370c86026e6698462a5be178da8453f99a0adaea
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213237"
---
# <a name="oid_wdi_set_tcp_offload_parameters"></a>OID \_ WDI \_ 设置 \_ TCP \_ 卸载 \_ 参数


OID \_ WDI \_ 将 \_ tcp \_ 卸载 \_ 参数从操作系统发送到设备，以设置 tcp 卸载参数。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

在某些情况下（如由于性能问题而需要关闭卸载时），会发送此命令。

下边缘驱动程序 (LE) 必须使用 [**WDI \_ TLV \_ tcp \_ 集 \_ 卸载 \_ 参数**](./wdi-tlv-tcp-set-offload-parameters.md) 的内容来更新当前报告的 tcp 卸载功能。 更新之后，该 LE 必须报告当前的任务卸载功能，并通过 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 任务 \_ 卸载 \_ 当前 \_ 配置](ndis-status-wdi-indication-task-offload-current-config.md)。 此状态指示可确保所有的过量协议驱动程序都用新功能信息进行更新。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                        | 允许多个 TLV 实例 | 可选 | 说明                           |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------|
| [**WDI \_ TLV \_ TCP \_ 设置 \_ 卸载 \_ 参数**](./wdi-tlv-tcp-set-offload-parameters.md) |                                |          | 要设置的 TCP 卸载参数。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

