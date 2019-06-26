---
title: OID_WDI_TASK_CHANGE_OPERATION_MODE
description: OID_WDI_TASK_CHANGE_OPERATION_MODE 配置端口的操作模式。
ms.assetid: 84be0658-104d-4336-bc2f-6f2624f33857
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_CHANGE_OPERATION_MODE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f31cc86fe32c2a65f85c8b0abe8a3f45feb357e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386528"
---
# <a name="oidwditaskchangeoperationmode"></a>OID\_WDI\_任务\_更改\_操作\_模式


OID\_WDI\_任务\_更改\_操作\_模式配置的端口的操作模式。

| Object | 中止支持 | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------|---------------------------------------|---------------------------------|
| Port   | 否            | 4                                     | 1                               |

 

## <a name="task-parameters"></a>任务参数


| TLV                                                              | 允许多个 TLV 实例 | 可选 | 描述                 |
|------------------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI\_TLV\_操作\_模式**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-operation-mode) |                                |          | 所需的操作模式。 |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_更改\_操作\_模式\_完成](ndis-status-wdi-indication-change-operation-mode-complete.md)

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

 

 




