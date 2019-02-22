---
title: OID_WDI_TASK_CLOSE
description: OID_WDI_TASK_CLOSE 请求 IHV 组件关闭适配器。 这包括禁用中断和硬件正在关闭。 暂停工作，在此任务是通过传递给 IHV IHV 通过注册的 CloseAdapterHandler 处理程序。
ms.assetid: 407d1dfa-18f7-4e22-8f7e-51fd610210af
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_CLOSE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a8ce742a66a3bc6fee4d8d1d7e3f95f1e3944ba4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554752"
---
# <a name="oidwditaskclose"></a>OID\_WDI\_TASK\_CLOSE


OID\_WDI\_任务\_关闭请求 IHV 组件关闭适配器。 这包括禁用中断和硬件正在关闭。 暂停工作，在此任务是通过传递给 IHV IHV 通过注册的 CloseAdapterHandler 处理程序。

| 对象  | 中止支持 | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|---------|---------------|---------------------------------------|---------------------------------|
| 适配器 | 否            | 1                                     | 5                               |

 

## <a name="task-parameters"></a>任务参数


无
## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_关闭\_完成](ndis-status-wdi-indication-close-complete.md)要求
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

 

 




