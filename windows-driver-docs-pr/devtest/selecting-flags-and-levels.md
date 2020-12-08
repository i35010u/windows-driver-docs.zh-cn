---
title: 选择标志和级别
description: 选择标志和级别
keywords:
- 跟踪标志 WDK
- 标志 WDK 软件跟踪
- 跟踪级别 WDK
- 级别 WDK 软件跟踪
- 跟踪会话 WDK，标志
- 跟踪会话 WDK，级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 652ee4fcef9a544b65555e2f0145b0b9952e30c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793985"
---
# <a name="selecting-flags-and-levels"></a>选择标志和级别


" **跟踪标志和级别选择** " 对话框允许您为跟踪会话中的每个提供程序选择 [跟踪标志](trace-flags.md) 和 [跟踪级别](trace-level.md) 。 " **跟踪标志和级别选择** " 对话框可方便地显示提供程序提供的所有标志和级别，因此无需记住它们。

或者，可以在 "**高级日志会话选项**" 对话框中手动设置 **标志** 和 **级别** 值。 有关信息，请参阅 [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

本节包括：

[打开跟踪标志和级别选择对话框](opening-the-tracing-flags-and-level-selection-dialog-box.md)

[使用跟踪标志和级别选择对话框](using-the-tracing-flags-and-level-selection-dialog-box.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

仅当 TraceView 可以找到提供程序的 [PDB 符号文件](pdb-symbol-files.md)或在 TMF 路径中 ( 找到该提供程序的 [) 文件](trace-message-control-file.md)时，才会启用 "**跟踪标志和级别选择**" 对话框， () 中使用 "**设置 TMF 搜索路径**" 选项指定。 否则，将禁用打开 **跟踪标志和级别选择** 对话框的 "**设置标志和级别**" 按钮。 使用 " **选择 TMF 文件** " 选项时，始终禁用对话框。

如果 " **跟踪标志和级别选择** " 对话框处于禁用状态，则可以在 " **高级跟踪会话选项** " 对话框中手动设置跟踪标志和该提供程序的级别。 有关说明，请参阅 [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

标志和级别是跟踪提供程序的属性。 通常，标志表示越来越详细的报表级别，它们表示事件的严重性 (信息、警告或错误) 。

 

 





