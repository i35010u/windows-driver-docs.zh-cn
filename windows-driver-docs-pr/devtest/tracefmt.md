---
title: Tracefmt
description: Tracefmt
keywords:
- Tracefmt WDK
- 软件跟踪 WDK，Tracefmt
- 显示跟踪消息
- 格式化跟踪消息 WDK Tracefmt
- 跟踪消息格式 WDK Tracefmt
- 软件跟踪 WDK，设置消息格式
- 跟踪 WDK，Tracefmt
- 跟踪消息格式化文件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 885e9e7aa0139e9af57e440ef7cb3a40c54cfb56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836839"
---
# <a name="tracefmt"></a>Tracefmt


## <span id="ddk_tracefmt_tools"></span><span id="DDK_TRACEFMT_TOOLS"></span>


Tracefmt ( # A0) 是一种命令行工具，用于设置和显示事件跟踪日志文件 ( .etl) 或实时跟踪会话的跟踪消息。 Tracefmt 可以在命令提示符窗口中显示消息或将其保存在文本文件中。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在哪里可以获得 Tracefmt？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>安装 WDK、Visual Studio 和桌面应用的 Windows SDK 时，将包含 Tracefmt ( # A0) 。 有关下载工具包的信息，请参阅 <a href="/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Hardware Downloads](../download-the-wdk.md)">Windows 硬件下载</a>。</p>
<p><strong>Windows 驱动程序工具包 (WDK) 8.1</strong> (安装路径) </p>
<p>% WindowsSdkDir% \bin\x64\Tracefmt.exe</p>
<p>% WindowsSdkDir% \bin\x86\Tracefmt.exe</p>
<div class="alert">
<strong>注意</strong>  Visual Studio 环境变量（%WindowsSdkDir%）表示安装了工具包的 Windows 工具包目录的路径，例如 C:\Program Files (x86)\Windows Kits\8.1。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

Tracefmt 使用 [跟踪消息格式 (TMF) 文件](trace-message-format-file.md) 格式说明，将二进制跟踪消息转换为可读格式。 你可以提供 TMF 文件或提供跟踪提供程序的图像文件，并 Tracefmt 创建 TMF 文件。

Tracefmt 可以设置 **TraceEvent** 函数生成的跟踪事件的格式，以及 [**WmiTraceMessage**](/windows-hardware/drivers/ddi/wdm/nf-wdm-wmitracemessage)、 **TraceMessage** 函数或 [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)) 宏生成的跟踪消息。 有关 **TraceEvent** 和 **TraceMessage** 函数的详细信息，请参阅 Windows SDK 文档。

本节包括：

[了解 Tracefmt](understanding-tracefmt.md)

[Tracefmt 的概念](tracefmt-concepts.md)

[**Tracefmt 命令**](tracefmt-commands.md)

[Tracefmt 示例](tracefmt-examples.md)

