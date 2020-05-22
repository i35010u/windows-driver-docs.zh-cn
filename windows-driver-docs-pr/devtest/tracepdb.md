---
title: Tracepdb
description: Tracepdb
ms.assetid: da7658a8-5fc3-409c-8a34-2aa134b9823b
keywords:
- 软件跟踪 WDK，Tracepdb
- Tracepdb WDK
- TMF 文件 WDK，Tracepdb
- 跟踪 WDK，Tracepdb
- 跟踪消息格式化文件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d559734dd426890d3e88abdeb3d192dc3ba62f0
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769447"
---
# <a name="tracepdb"></a>Tracepdb


## <span id="ddk_tracepdb_tools"></span><span id="DDK_TRACEPDB_TOOLS"></span>


Tracepdb （Tracepdb）是一种命令行工具，它通过从使用 WPP 软件跟踪宏的[跟踪提供程序](trace-provider.md)的完整或专用[PDB 符号文件](pdb-symbol-files.md)中提取跟踪消息格式说明来创建[跟踪消息格式（. tmf）文件](trace-message-format-file.md)。

您可以为跟踪提供程序提供私有 PDB 符号文件，或 Tracepdb 可以在目录中找到该提供程序的私有 PDB 符号文件或使用内部符号服务器。 Tracepdb 在 windows 2000 和更高版本的 Windows 上运行。

**请注意**  [Tracefmt](tracefmt.md)（一种格式和显示跟踪消息的工具）还可以从 PDB 符号文件创建 TMF 文件。 有关信息，请参阅 Tracefmt。

 

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在哪里可以获得 Tracepdb？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>安装 WDK、Visual Studio 和适用于桌面应用的 Windows SDK 时，将包含 Tracepdb （Tracepdb）。 有关下载套件的信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Hardware Downloads](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)">Windows 硬件下载</a>。</p>
<p><strong>Windows 驱动程序工具包（WDK） 8.1</strong> （安装路径）</p>
<p>%WindowsSdkDir%\bin\x64\Tracepdb.exe</p>
<p>%WindowsSdkDir%\bin\x86\Tracepdb.exe</p>
<div class="alert">
<strong>注意</strong>   Visual Studio 环境变量% WindowsSdkDir% 表示安装包的 Windows 工具包目录的路径，例如，C:\Program Files （x86） \Windows Kits\8.1。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

本节包括下列主题：

[Tracepdb 概述](tracepdb-overview.md)

[**Tracepdb 命令**](tracepdb-commands.md)
