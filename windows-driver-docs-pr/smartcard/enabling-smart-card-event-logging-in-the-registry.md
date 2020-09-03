---
title: 在注册表中启用智能卡事件日志记录
description: 在注册表中启用智能卡事件日志记录
ms.assetid: b07ff2d7-9025-424e-a57e-eb37ae4091f4
keywords:
- 智能卡驱动程序 WDK，注册表
- 注册表 WDK 智能卡
- 记录 WDK 智能卡
- 事件 WDK 智能卡
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7e29273f9cd8053cb54c5b6eac4906ddfcdfa0f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384199"
---
# <a name="enabling-smart-card-event-logging-in-the-registry"></a>在注册表中启用智能卡事件日志记录


## <span id="_ntovr_enabling_smart_card_event_logging_in_the_registry"></span><span id="_NTOVR_ENABLING_SMART_CARD_EVENT_LOGGING_IN_THE_REGISTRY"></span>


智能卡读卡器驱动程序应记录系统事件日志中的错误，以便系统管理员可以使用日志来帮助诊断驱动程序出现故障的原因。

若要启用事件日志记录，必须在以下注册表项下向注册表添加几个值：

**HKEY \_LOCAL \_ MACHINE \\ system \\ CurrentControlSet \\ Services \\ EventLog \\ System \\ ** *SmartCardDriver*

下表列出了启用事件日志记录的注册表值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">注册表值名称</th>
<th align="left">注册表值的内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>EventMessageFile</strong></p></td>
<td align="left"><p><em>% SystemRoot% \System32\Drivers\SmartCardDriver.sys</em></p>
<div class="alert">
<strong>重要提示</strong>   文件扩展名必须包含在<strong>EventMessageFile</strong>值名称中，但它不能出现在注册表路径的任何其他部分。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p><strong>TypesSupported</strong></p></td>
<td align="left"><p><strong>DWORD：0x00000007</strong></p></td>
</tr>
</tbody>
</table>

 

有关指定这些注册表项的详细信息，请参阅 [**INF AddService 指令**](../install/inf-addservice-directive.md)。

 

