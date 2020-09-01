---
title: OID_WDI_TASK_IHV
description: OID_WDI_TASK_IHV 用于启动 IHV 启动的任务。
ms.assetid: 2F18A92D-D658-4454-874F-7DC3B6F8F453
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_IHV 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 05f8707a3f9ccc72f7edab5bd48f5aa42dfb01bb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216148"
---
# <a name="oid_wdi_task_ihv"></a>OID \_ WDI \_ 任务 \_ IHV


OID \_ WDI \_ 任务 \_ IHV 用于启动 IHV 启动的任务。

| 对象 | 支持中止                                           | 主机驱动程序策略 (默认优先级)        | 正常执行时间 (秒)  |
|--------|---------------------------------------------------------|---------------------------------------------|---------------------------------|
| 端口   | 是。 中止后，端口必须处于干净状态。 | 优先级取决于 IHV 请求的设置。 | 10                              |

 

任务由发送 [NDIS \_ 状态 \_ WDI \_ 指示 \_ ihv \_ 任务 \_ 请求](ndis-status-wdi-indication-ihv-task-request.md)启动，并根据 IHV 请求的值确定优先级。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                  | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                   |
|--------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ IHV \_ 任务 \_ 设备 \_ 上下文**](./wdi-tlv-ihv-task-device-context.md) |                                | X        | IHV 组件提供的上下文数据。 这将从 [NDIS \_ STATUS \_ WDI \_ 指示 \_ IHV \_ 任务 \_ 请求](ndis-status-wdi-indication-ihv-task-request.md)转发。 |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ IHV \_ 任务 \_ 完成](ndis-status-wdi-indication-ihv-task-complete.md)

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

 

