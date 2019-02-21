---
title: 事件\_类型\_限定符
description: 事件\_类型\_限定符
ms.assetid: 528e5eaa-aaeb-4e5b-a4b2-0f518fcd79ee
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cc015ae40f9b2db851ebc16b0749d8b5d39c5a9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521506"
---
# <a name="eventtypesqualifiers"></a>事件\_类型\_限定符


## <span id="ddk_event_type_qualifiers_kr"></span><span id="DDK_EVENT_TYPE_QUALIFIERS_KR"></span>


事件\_类型\_限定符 WMI 类限定符包含一系列类型的事件报告的 HBA 微型端口驱动程序支持 T11 委员会*光纤通道 HBA API*规范。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HBA_EVENT_ADAPTER_UNKNOWN</p></td>
<td align="left"><p>指示适配器事件为未知。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_ADAPTER_ADD</p></td>
<td align="left"><p>指示 HBA，已添加到本地系统。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_ADAPTER_REMOVE</p></td>
<td align="left"><p>指示已从本地系统中删除 HBA。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_ADAPTER_CHANGE</p></td>
<td align="left"><p>指示已对本地系统上的 HBA 的配置更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_UNKNOWN</p></td>
<td align="left"><p>表示未知端口事件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_PORT_OFFLINE</p></td>
<td align="left"><p>表示本地端口已脱机。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_ONLINE</p></td>
<td align="left"><p>指示本地端口已联机。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_PORT_NEW_TARGETS</p></td>
<td align="left"><p>指示本地端口已添加到其已发现的远程端口的目标设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_FABRIC</p></td>
<td align="left"><p>指示本地端口已收到已注册的状态更改通知 (RSCN) 命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_PORT_STAT_THRESHOLD</p></td>
<td align="left"><p>指示统计计数器已达到已注册的级别。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_STAT_GROWTH</p></td>
<td align="left"><p>指示统计计数器已增加速率等于或超过已注册的速率。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_TARGET_UNKNOWN</p></td>
<td align="left"><p>表示未知目标事件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_TARGET_OFFLINE</p></td>
<td align="left"><p>表示操作的目标端口的使用变得不可能。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_TARGET_ONLINE</p></td>
<td align="left"><p>指示还原操作使用目标端口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_TARGET_REMOVED</p></td>
<td align="left"><p>指示目标端口已从结构中删除。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_LINK_UNKNOWN</p></td>
<td align="left"><p>指示链接事件为未知。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_LINK_INCIDENT</p></td>
<td align="left"><p>指示本地 HBA 已收到注册链接事件命令。</p></td>
</tr>
</tbody>
</table>

 

通过包括*Hbaapi.h*您的软件有权访问一系列的对应于上表中的类型名称的符号常量。 这些符号常量的定义中不包括*Hbapiwmi.h* （WMI 工具套件时对其进行编译，生成的文件）。

 

 





