---
title: 示例3典型启动命令
description: 示例3典型启动命令
keywords:
- 跟踪会话 WDK，开始
- 开始命令
- -start 命令
- 启动跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 528ede17a25fdacde36b16354fb9ec3d3c2d64f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839141"
---
# <a name="example-3-typical-start-command"></a>示例 3：典型启动命令

## <span id="ddk_typical_start_command_tools"></span><span id="DDK_TYPICAL_START_COMMAND_TOOLS"></span>

以下命令格式通常用于启动跟踪会话：

```
tracelog -start MyTrace -guid MyProvider.guid -f d:\traces\testtrace.etl -flag 2 -level 0xFFFF
```

命令启动一个名为 "MyTrace" 的跟踪会话。

它使用 **-guid** 参数来指示 MyProvider 文件，这是一个简单的文本文件，该文件只包含提供程序的控件 guid。 还可以将 [控件 GUID 文件](control-guid-file.md)（如 Tracedrv）与 **-GUID** 参数一起使用。 Tracedrv 包含在 [Tracedrv](/samples/microsoft/windows-driver-samples/tracedrv/) 示例中。

该命令包括 **-f** 参数，用于指定事件跟踪日志文件的名称和位置。 它包括 **-标志** 参数，用于指定标志集和 **级别** 参数以指定级别设置。 您可以省略这些参数，但某些跟踪提供程序不会生成任何跟踪消息，除非您设置了标志或级别。
