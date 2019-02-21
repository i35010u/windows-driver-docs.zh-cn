---
title: OID_WDI_TASK_IHV
description: OID_WDI_TASK_IHV 用于启动 IHV 启动的任务。
ms.assetid: 2F18A92D-D658-4454-874F-7DC3B6F8F453
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_IHV 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d89f1dc037544b32047d64d6c35249e97e7a590d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526509"
---
# <a name="oidwditaskihv"></a>OID\_WDI\_TASK\_IHV


OID\_WDI\_任务\_IHV 用于启动 IHV 启动的任务。

| 对象 | 中止支持                                           | 默认优先级 （主机驱动程序策略）       | 正常执行时间 （秒） |
|--------|---------------------------------------------------------|---------------------------------------------|---------------------------------|
| 端口   | 是。 端口必须保持干净状态后中止。 | 优先级取决于 IHV 请求设置。 | 10                              |

 

由发送启动任务[NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求](ndis-status-wdi-indication-ihv-task-request.md)，并已根据的值请求的 IHV。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                  | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                   |
|--------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_IHV\_TASK\_DEVICE\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/dn926313) |                                | X        | IHV 组件提供的上下文数据。 这从转发[NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求](ndis-status-wdi-indication-ihv-task-request.md)。 |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_IHV\_任务\_完成](ndis-status-wdi-indication-ihv-task-complete.md)要求
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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




