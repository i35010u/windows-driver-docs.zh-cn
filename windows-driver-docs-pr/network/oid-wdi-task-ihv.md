---
title: OID_WDI_TASK_IHV
description: OID_WDI_TASK_IHV 用于启动 IHV 启动的任务。
ms.assetid: 2F18A92D-D658-4454-874F-7DC3B6F8F453
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_IHV 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c41f1f68bdaa39bc0c2d57d499cbc007767cac73
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387238"
---
# <a name="oidwditaskihv"></a>OID\_WDI\_TASK\_IHV


OID\_WDI\_任务\_IHV 用于启动 IHV 启动的任务。

| Object | 中止支持                                           | 默认优先级 （主机驱动程序策略）       | 正常执行时间 （秒） |
|--------|---------------------------------------------------------|---------------------------------------------|---------------------------------|
| Port   | 是。 端口必须保持干净状态后中止。 | 优先级取决于 IHV 请求设置。 | 10                              |

 

由发送启动任务[NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求](ndis-status-wdi-indication-ihv-task-request.md)，并已根据的值请求的 IHV。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                  | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                   |
|--------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_IHV\_TASK\_DEVICE\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ihv-task-device-context) |                                | X        | IHV 组件提供的上下文数据。 这从转发[NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求](ndis-status-wdi-indication-ihv-task-request.md)。 |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_IHV\_任务\_完成](ndis-status-wdi-indication-ihv-task-complete.md)

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

 

 




