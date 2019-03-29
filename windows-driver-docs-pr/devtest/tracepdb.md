---
title: Tracepdb
description: Tracepdb
ms.assetid: da7658a8-5fc3-409c-8a34-2aa134b9823b
keywords:
- 跟踪 WDK，Tracepdb 软件
- Tracepdb WDK
- TMF 文件 WDK Tracepdb
- 跟踪 WDK Tracepdb
- 跟踪消息格式文件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8715acbeb626c7efb7915aa683902214593b0285
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565044"
---
# <a name="tracepdb"></a>Tracepdb


## <span id="ddk_tracepdb_tools"></span><span id="DDK_TRACEPDB_TOOLS"></span>


Tracepdb (Tracepdb.exe) 是一个命令行工具，创建[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)通过提取跟踪消息格式设置说明从完整或私有[PDB 符号文件](pdb-symbol-files.md)为[跟踪提供程序](trace-provider.md)使用 WPP 软件跟踪宏。

您可以跟踪提供程序提供专用的 PDB 符号文件也 Tracepdb 可以找到提供程序的专用 PDB 符号文件的目录中或通过使用内部符号服务器。 Tracepdb 在 Windows 2000 和更高版本的 Windows 上运行。

**请注意**  [Tracefmt](tracefmt.md)，一个工具，设置格式并显示跟踪消息，还可以从 PDB 符号文件创建 TMF 文件。 有关信息，请参阅 Tracefmt。

 

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">哪里可以获得 Tracepdb？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>在安装 WDK、 Visual Studio 和适用于桌面应用程序的 Windows SDK 时 Tracepdb (Tracepdb.exe) 包含。 有关下载工具包的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">下载 Windows 硬件</a>。</p>
<p><strong>Windows Driver Kit (WDK) 8.1</strong> （安装路径）</p>
<p>%WindowsSdkDir%\bin\x64\Tracepdb.exe</p>
<p>%WindowsSdkDir%\bin\x86\Tracepdb.exe</p>
<div class="alert">
<strong>请注意</strong>  Visual Studio 环境变量，%windowssdkdir%，表示 Windows 工具包工具包安装的目录，例如，C:\Program Files (x86) \Windows Kits\8.1 的路径。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

本部分包括以下主题：

[Tracepdb 概述](tracepdb-overview.md)

[**Tracepdb 命令**](tracepdb-commands.md)
