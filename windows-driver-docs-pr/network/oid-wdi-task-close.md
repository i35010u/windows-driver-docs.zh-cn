---
title: OID_WDI_TASK_CLOSE
description: OID_WDI_TASK_CLOSE 请求 IHV 组件关闭适配器。 这包括禁用中断和硬件正在关闭。 暂停工作，在此任务是通过传递给 IHV IHV 通过注册的 CloseAdapterHandler 处理程序。
ms.assetid: 407d1dfa-18f7-4e22-8f7e-51fd610210af
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_CLOSE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 5e48dd2af651173ba66ad26e030f2d03a18f0066
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348489"
---
# <a name="oidwditaskclose"></a>OID\_WDI\_TASK\_CLOSE


OID\_WDI\_任务\_关闭请求 IHV 组件关闭适配器。 这包括禁用中断和硬件正在关闭。 暂停工作，在此任务是通过传递给 IHV IHV 通过注册的 CloseAdapterHandler 处理程序。

| Object  | 中止支持 | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|---------|---------------|---------------------------------------|---------------------------------|
| 适配器 | 否            | 1                                     | 5                               |

 

## <a name="task-parameters"></a>任务参数


无
## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_关闭\_完成](ndis-status-wdi-indication-close-complete.md)

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

 

 




