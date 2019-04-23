---
title: OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME
description: OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME 请求 IHV 组件发送的响应操作帧。
ms.assetid: DA2FF006-BA81-48B9-8AAD-694818E78AEF
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: cc192d0be64f2e9f4dcff799acd9f500b78d38c5
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902409"
---
# <a name="oidwditasksendresponseactionframe"></a>OID\_WDI\_TASK\_SEND\_RESPONSE\_ACTION\_FRAME


OID\_WDI\_任务\_发送\_响应\_操作\_帧请求 IHV 组件发送的响应操作帧。

| Object | 中止支持                                           | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是。 端口必须保持干净状态后中止。 | 3                                     | 5                               |

 

此任务是时间敏感，必须在接收此数据包的 100 毫秒内提供服务。

最大超时时间尚未过期，而该端口应重试将在帧发送到指定的通道上的远程设备。

任务已完成或者本地设备从远程设备操作帧发送接收确认时，在超时到期，或主机中止操作。 同一个通道停留时间过期后，设备可能表示任务完成。

主机可能会决定中止此操作并继续/重试操作帧 exchange，因此，必须在设备是能够快速中止此操作。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                                               | 允许多个 TLV 实例 | 可选 | 描述                                      |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------|
| [**WDI\_TLV\_SEND\_ACTION\_FRAME\_RESPONSE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn898054) |                                |          | 发送操作帧响应参数。 |
| [**WDI\_TLV\_操作\_帧\_正文**](https://msdn.microsoft.com/library/windows/hardware/dn926118)                                           |                                |          | 操作帧正文中。                           |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_发送\_响应\_操作\_帧\_完成](ndis-status-wdi-indication-send-response-action-frame-complete.md)

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

 

 




