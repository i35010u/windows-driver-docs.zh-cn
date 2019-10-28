---
title: Tracefmt
description: Tracefmt
ms.assetid: abf23d76-423d-4d1e-afde-83739015bbfd
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
ms.openlocfilehash: d06f7347e233e2a2dc17f162c1c98e6135bcdd69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839266"
---
# <a name="tracefmt"></a>Tracefmt


## <span id="ddk_tracefmt_tools"></span><span id="DDK_TRACEFMT_TOOLS"></span>


Tracefmt （Tracefmt）是一种命令行工具，用于设置和显示事件跟踪日志文件（.etl）或实时跟踪会话中的跟踪消息。 Tracefmt 可以在命令提示符窗口中显示消息或将其保存在文本文件中。

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
<td align="left"><p>安装 WDK、Visual Studio 和适用于桌面应用的 Windows SDK 时，将包含 Tracefmt （Tracefmt）。 有关下载套件的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows 硬件下载</a>。</p>
<p><strong>Windows 驱动程序工具包（WDK） 8.1</strong> （安装路径）</p>
<p>%WindowsSdkDir%\bin\x64\Tracefmt.exe</p>
<p>%WindowsSdkDir%\bin\x86\Tracefmt.exe</p>
<div class="alert">
<strong>请注意</strong>  Visual Studio 环境变量% WindowsSdkDir% 表示安装了包的 Windows 工具包目录的路径，例如，C:\Program Files （x86） \windows kits\8.1。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

Tracefmt 使用[跟踪消息格式（TMF）文件](trace-message-format-file.md)中的格式说明将二进制跟踪消息转换为可读格式。 你可以提供 TMF 文件或提供跟踪提供程序的图像文件，并 Tracefmt 创建 TMF 文件。

Tracefmt 可以设置**TraceEvent**函数生成的跟踪事件的格式，以及[**WmiTraceMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-wmitracemessage)、 **TraceMessage**函数或[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏生成的跟踪消息。 有关**TraceEvent**和**TraceMessage**函数的详细信息，请参阅 Windows SDK 文档。

本部分包括：

[了解 Tracefmt](understanding-tracefmt.md)

[Tracefmt 概念](tracefmt-concepts.md)

[**Tracefmt 命令**](tracefmt-commands.md)

[Tracefmt 示例](tracefmt-examples.md)

 

 





