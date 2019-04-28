---
title: 示例 3 典型 Start 命令
description: 示例 3 典型 Start 命令
ms.assetid: a0e8580d-b841-4077-82f5-6aaef57b0ff7
keywords:
- 跟踪会话 WDK，启动
- 启动命令
- -启动命令
- 启动跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d05d4f395db9c6f86c1b98cf8837d35f4af301a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344684"
---
# <a name="example-3-typical-start-command"></a>示例 3：典型启动命令

## <span id="ddk_typical_start_command_tools"></span><span id="DDK_TYPICAL_START_COMMAND_TOOLS"></span>

以下命令格式通常用于启动跟踪会话：

```
tracelog -start MyTrace -guid MyProvider.guid -f d:\traces\testtrace.etl -flag 2 -level 0xFFFF
```

该命令启动名为"MyTrace"的跟踪会话。

它使用**guid**参数来指示 MyProvider.guid 文件，不包含任何内容，但提供程序的简单文本文件控制 GUID。 此外可以使用[控制 GUID 文件](control-guid-file.md)，如 Tracedrv.ctl，与**guid**参数。 中包含 Tracedrv.ctl [TraceDrv](https://go.microsoft.com/fwlink/p/?linkid=256197)示例。

该命令包含 **-f**参数指定的名称和事件跟踪日志文件的位置。 它包括 **-标志**参数指定的标志集并 **-级别**参数指定的级别设置。 可以省略这些参数，但除非设置了标志或级别，否则某些跟踪提供程序不生成任何跟踪消息。
