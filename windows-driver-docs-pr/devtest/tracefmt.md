---
title: Tracefmt
description: Tracefmt
ms.assetid: abf23d76-423d-4d1e-afde-83739015bbfd
keywords:
- Tracefmt WDK
- 跟踪 WDK，Tracefmt 软件
- 显示跟踪消息
- 格式设置的跟踪消息 WDK Tracefmt
- 跟踪消息格式 WDK Tracefmt
- 软件跟踪 WDK、 设置消息格式
- 跟踪 WDK Tracefmt
- 跟踪消息格式文件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c333d40e72be15337bf41e1beaf434403fcf6bc8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391817"
---
# <a name="tracefmt"></a>Tracefmt


## <span id="ddk_tracefmt_tools"></span><span id="DDK_TRACEFMT_TOOLS"></span>


Tracefmt (Tracefmt.exe) 是一个命令行工具，设置格式并显示从事件跟踪日志文件 (.etl) 或实时跟踪会话的跟踪消息。 Tracefmt 可以在命令提示符窗口中显示的消息或将它们保存在文本文件中。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">哪里可以获得 Tracefmt？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>在安装 WDK、 Visual Studio 和适用于桌面应用程序的 Windows SDK 时 Tracefmt (Tracefmt.exe) 包含。 有关下载工具包的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">下载 Windows 硬件</a>。</p>
<p><strong>Windows Driver Kit (WDK) 8.1</strong> （安装路径）</p>
<p>%WindowsSdkDir%\bin\x64\Tracefmt.exe</p>
<p>%WindowsSdkDir%\bin\x86\Tracefmt.exe</p>
<div class="alert">
<strong>请注意</strong>  Visual Studio 环境变量，%windowssdkdir%，表示 Windows 工具包工具包安装的目录，例如，C:\Program Files (x86) \Windows Kits\8.1 的路径。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

Tracefmt 使用中的格式设置说明[跟踪消息格式 (TMF) 文件](trace-message-format-file.md)将转换为人工可读格式的二进制跟踪消息。 可以提供 TMF 文件或跟踪提供程序提供的图像文件并具有 Tracefmt 创建 TMF 文件。

Tracefmt 可以设置生成的跟踪事件的格式**TraceEvent**函数，并且生成的跟踪消息[ **WmiTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff565836)，则**TraceMessage**函数，或[ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)宏。 有关详细信息**TraceEvent**并**TraceMessage**函数，请参阅 Windows SDK 文档。

本部分包括：

[了解 Tracefmt](understanding-tracefmt.md)

[Tracefmt 概念](tracefmt-concepts.md)

[**Tracefmt 命令**](tracefmt-commands.md)

[Tracefmt 示例](tracefmt-examples.md)

 

 





