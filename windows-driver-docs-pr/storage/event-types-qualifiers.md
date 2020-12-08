---
title: 事件 \_ 类型 \_ 限定符
description: 事件 \_ 类型 \_ 限定符
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9a86ee0bac3905954daff84ca79b37c79143b49e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811713"
---
# <a name="event_types_qualifiers"></a>事件 \_ 类型 \_ 限定符


## <span id="ddk_event_type_qualifiers_kr"></span><span id="DDK_EVENT_TYPE_QUALIFIERS_KR"></span>


事件 \_ 类型 \_ 限定符 WMI 类限定符包含 hba 微型端口驱动程序报告的事件类型的列表，该驱动程序支持 T11 委员会 *光纤通道 HBA API* 规范。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HBA_EVENT_ADAPTER_UNKNOWN</p></td>
<td align="left"><p>指示适配器事件未知。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_ADAPTER_ADD</p></td>
<td align="left"><p>指示已将 HBA 添加到了本地系统。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_ADAPTER_REMOVE</p></td>
<td align="left"><p>指示 HBA 已从本地系统中删除。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_ADAPTER_CHANGE</p></td>
<td align="left"><p>指示本地系统上的某个 HBA 发生了配置更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_UNKNOWN</p></td>
<td align="left"><p>指示端口事件未知。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_PORT_OFFLINE</p></td>
<td align="left"><p>指示本地端口已脱机。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_ONLINE</p></td>
<td align="left"><p>指示本地端口已经联机。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_PORT_NEW_TARGETS</p></td>
<td align="left"><p>指示本地端口已将目标设备添加到其发现的远程端口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_FABRIC</p></td>
<td align="left"><p>指示本地端口已接收到 (RSCN) 命令的已注册状态更改通知。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_PORT_STAT_THRESHOLD</p></td>
<td align="left"><p>指示统计计数器已达到注册级别。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_STAT_GROWTH</p></td>
<td align="left"><p>指示统计计数器的增加速率为等于或超出注册速率。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_TARGET_UNKNOWN</p></td>
<td align="left"><p>指示目标事件未知。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_TARGET_OFFLINE</p></td>
<td align="left"><p>指示不能使用目标端口。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_TARGET_ONLINE</p></td>
<td align="left"><p>指示已还原目标端口的操作使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_TARGET_REMOVED</p></td>
<td align="left"><p>指示已从构造中删除目标端口。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_LINK_UNKNOWN</p></td>
<td align="left"><p>指示链接事件未知。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_LINK_INCIDENT</p></td>
<td align="left"><p>指示本地 HBA 已收到 register link 事件命令。</p></td>
</tr>
</tbody>
</table>

 

通过包含 *Hbaapi* ，你的软件将有权访问与上表中的类型名称对应的一系列符号常量。 这些符号常量的定义不包含在 *Hbapiwmi* 中， (WMI 工具套件编译) 时生成的文件。

 

 





