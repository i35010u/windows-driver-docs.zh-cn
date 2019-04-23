---
title: OID_WDI_TASK_IHV
description: OID_WDI_TASK_IHV 用于启动 IHV 启动的任务。
ms.assetid: 2F18A92D-D658-4454-874F-7DC3B6F8F453
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_IHV 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3ae840719a3548a72662acb49cdd74991787fc82
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903293"
---
# <a name="oidwditaskihv"></a>OID\_WDI\_TASK\_IHV


OID\_WDI\_任务\_IHV 用于启动 IHV 启动的任务。

| Object | 中止支持                                           | 默认优先级 （主机驱动程序策略）       | 正常执行时间 （秒） |
|--------|---------------------------------------------------------|---------------------------------------------|---------------------------------|
| 端口   | 是。 端口必须保持干净状态后中止。 | 优先级取决于 IHV 请求设置。 | 10                              |

 

由发送启动任务[NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求](ndis-status-wdi-indication-ihv-task-request.md)，并已根据的值请求的 IHV。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                  | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                   |
|--------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_IHV\_TASK\_DEVICE\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/dn926313) |                                | X        | IHV 组件提供的上下文数据。 这从转发[NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求](ndis-status-wdi-indication-ihv-task-request.md)。 |

 

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

 

 




