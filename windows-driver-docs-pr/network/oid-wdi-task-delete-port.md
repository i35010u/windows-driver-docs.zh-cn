---
title: OID_WDI_TASK_DELETE_PORT
description: OID_WDI_TASK_DELETE_PORT 请求 IHV 组件释放所有资源 (包括 MAC 和 PHY) 分配给指定的端口）。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_DELETE_PORT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e9cf3851c9ed0057ff1dc5ae647edaadd95bf115
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829283"
---
# <a name="oid_wdi_task_delete_port"></a>OID \_ WDI \_ 任务 \_ 删除 \_ 端口


OID \_ WDI \_ 任务 \_ 删除 \_ 端口请求 IHV 组件释放所有资源 (包括 MAC 和 PHY) 分配给指定的端口）。

| 对象  | 支持中止 | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|---------|---------------|---------------------------------------|---------------------------------|
| 适配器 | 否            | 6                                     | 1                               |

 

## <a name="task-parameters"></a>任务参数


| TLV                                                                               | 允许多个 TLV 实例 | 可选 | 说明                 |
|-----------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI \_ TLV \_ 删除 \_ 端口 \_ 参数**](./wdi-tlv-delete-port-parameters.md) |                                |          | Delete 端口参数。 |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 删除 \_ 端口 \_ 完成](ndis-status-wdi-indication-delete-port-complete.md)

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

 

