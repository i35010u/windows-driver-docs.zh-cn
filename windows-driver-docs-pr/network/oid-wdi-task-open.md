---
title: OID_WDI_TASK_OPEN
description: OID_WDI_TASK_OPEN 请求 IHV 组件初始化适配器。
ms.assetid: f4a77e08-1a1e-4d75-a559-a5cb01d825ee
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_OPEN 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 23ec5cdaeb22bb08623cd47c9f313ba3830ad434
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383588"
---
# <a name="oidwditaskopen"></a>OID\_WDI\_任务\_打开


OID\_WDI\_任务\_打开请求 IHV 组件初始化适配器。

| Object  | 中止支持 | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|---------|---------------|---------------------------------------|---------------------------------|
| 适配器 | 否            | 1                                     | 2                               |

 

适配器初始化包括下载到该适配器的固件和设置中断和其他硬件资源。 在初始化期间，此任务将传递到 IHV 使用注册的 IHV OpenAdapterHandler 处理程序。 在从低功耗状态恢复，这将传递到 IHV 使用 OID\_WDI\_任务\_打开。

## <a name="task-parameters"></a>任务参数


无
## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_打开\_完成](ndis-status-wdi-indication-open-complete.md)

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

 

 




