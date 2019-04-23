---
title: OID_WDI_TASK_STOP_AP
description: OID_WDI_TASK_STOP_AP 请求 IHV 组件断开连接指定端口上的所有连接的客户端，并停止信标和响应探测请求。 亚太配置和 MIB 属性会保留。
ms.assetid: b7df1d2f-fed4-4079-8a2d-3f691a52ad52
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_STOP_AP 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: efae7d2c8c681ab42c1aeaeb02466677a9f67368
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902563"
---
# <a name="oidwditaskstopap"></a>OID\_WDI\_TASK\_STOP\_AP


OID\_WDI\_任务\_停止\_AP 请求 IHV 组件断开连接指定端口上的所有已连接客户端，并停止信标和响应探测请求。 亚太配置和 MIB 属性会保留。

| Object | 中止支持 | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------|---------------------------------------|---------------------------------|
| 端口   | 否            | 2                                     | 1                               |

 

## <a name="task-parameters"></a>任务参数


无
## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_停止\_AP\_完成](ndis-status-wdi-indication-stop-ap-complete.md)

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

 

 




