---
title: OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE
description: OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE 请求 IHV 组件将关联响应发送到最近发送了关联请求的对等设备。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6fef160d5b19ddfe9ab24a0465f5652952ac091b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829233"
---
# <a name="oid_wdi_task_send_ap_association_response"></a>OID \_ WDI \_ TASK \_ 发送 \_ AP \_ 关联 \_ 响应


OID \_ WDI \_ TASK \_ 发送 \_ AP \_ 关联 \_ 响应请求 IHV 组件将关联响应发送到最近发送了关联请求的对等设备。

| 对象 | 支持中止                                           | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是的。 中止后，端口必须处于干净状态。 | 3                                     | 1                               |

 

如果由于任何原因而导致发送失败，则应为空 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 发送 \_ AP \_ 关联 \_ 响应的 \_ 完成](ndis-status-wdi-indication-send-ap-association-response-complete.md) ，其状态应包括在填充的标头中。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                                      | 允许多个 TLV 实例 | 可选 | 说明                                                                                                      |
|----------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 关联 \_ 响应 \_ 参数**](./wdi-tlv-association-response-parameters.md)      |                                |          | 关联响应参数。                                                                                 |
| [**WDI \_ TLV \_ 供应商 \_ 特定 \_ IE**](./wdi-tlv-vendor-specific-ie.md)                                |                                | X        | 在将响应发送到对等适配器之前，端口必须附加到关联响应 IE 集的附加请求。 |
| [**WDI \_ TLV \_ 传入 \_ 关联 \_ 请求 \_ 信息**](./wdi-tlv-incoming-association-request-info.md) |                                |          | 有关传入关联请求的信息。                                                              |
| [**WDI \_ TLV \_ WFD \_ 关联 \_ 状态**](./wdi-tlv-wfd-association-status.md)                        |                                | X        | 拒绝关联请求时要设置的状态值。                                                  |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 发送 \_ AP \_ 关联 \_ 响应 \_ 完成](ndis-status-wdi-indication-send-ap-association-response-complete.md)

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

 

