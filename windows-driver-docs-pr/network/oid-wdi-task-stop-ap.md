---
title: OID_WDI_TASK_STOP_AP
description: OID_WDI_TASK_STOP_AP 请求 IHV 组件断开指定端口上所有连接的客户端的连接，并停止引导并响应探测请求。 将保留 AP 配置和 MIB 属性。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_STOP_AP 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: df3054fe5a9cc015119699ad4bdddb86599745c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829211"
---
# <a name="oid_wdi_task_stop_ap"></a>OID \_ WDI \_ TASK \_ 停止 \_ AP


OID \_ WDI \_ TASK \_ 停止 \_ AP 请求 IHV 组件断开指定端口上的所有已连接客户端，并停止信标并响应探测请求。 将保留 AP 配置和 MIB 属性。

| 对象 | 支持中止 | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------|---------------------------------------|---------------------------------|
| 端口   | 否            | 2                                     | 1                               |

 

## <a name="task-parameters"></a>任务参数


无
## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 停止 \_ AP \_ 完成](ndis-status-wdi-indication-stop-ap-complete.md)

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

 

 




