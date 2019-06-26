---
title: 在注册表中启用智能卡事件日志记录
description: 在注册表中启用智能卡事件日志记录
ms.assetid: b07ff2d7-9025-424e-a57e-eb37ae4091f4
keywords:
- 智能卡驱动程序 WDK、 注册表
- 注册表 WDK 智能卡
- 日志 WDK 智能卡
- 事件 WDK 智能卡
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3d3916d0dfe7527f174ac37b5a54ca1242c6c23
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356720"
---
# <a name="enabling-smart-card-event-logging-in-the-registry"></a>在注册表中启用智能卡事件日志记录


## <span id="_ntovr_enabling_smart_card_event_logging_in_the_registry"></span><span id="_NTOVR_ENABLING_SMART_CARD_EVENT_LOGGING_IN_THE_REGISTRY"></span>


智能卡读卡器驱动程序应在系统事件日志中记录错误，以便系统管理员可以使用日志来帮助诊断驱动程序失败的原因。

若要启用日志记录的事件，必须将多个值添加到注册表项下的以下项：

**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\EventLog\\System\\** *SmartCardDriver*

下表列出了启用事件日志记录注册表值。

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
<td align="left"><p><em>%SystemRoot%\System32\Drivers\SmartCardDriver.sys</em></p>
<div class="alert">
<strong>重要</strong>  中必须包括文件扩展名<strong>EventMessageFile</strong>值的名称，但它必须永远不会显示在注册表路径的任何其他部分。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p><strong>TypesSupported</strong></p></td>
<td align="left"><p><strong>DWORD:0x00000007</strong></p></td>
</tr>
</tbody>
</table>

 

有关指定这些注册表项的详细信息，请参阅[ **INF AddService 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)。

 

 





