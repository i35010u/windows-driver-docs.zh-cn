---
title: 使用 GPUView
description: 使用 GPUView
ms.assetid: 55f589fd-e3ea-4fd2-9e8d-c225c2c3dbb5
ms.date: 01/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4c4bc466f25c34b2066af7e4f7166469888f385c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524494"
---
# <a name="using-gpuview"></a>使用 GPUView


GPUView (*GPUView.exe*) 是用于确定性能的图形处理单元 (GPU) 的开发工具和 CPU。 它会查看直接内存访问 (DMA) 缓冲区处理和视频硬件上的所有其他视频处理方面的性能。 GPUView 可用于开发符合 Windows Vista 显示器驱动程序模型的显示驱动程序。 GPUView 引入了 Windows 7 操作系统的版本。

GPUView 和其他与之关联的文件的形式包含与 Windows 性能工具包 (WPT) WPT MSI 的可安装选项。 GPUView 二进制文件包括适用于基于 x86 的、 基于 x64 和基于 IA64 体系结构。 例如， *Wpt\_x86.msi*面向 x86 平台。 

此外可以下载 GPUView 作为 Windows 7 SDK 的一部分。 安装 SDK 之后，你将需要转到 C:\Program Files\Microsoft SDKs\Windows\v7.0\bin 并运行 wpt_x64.msi 或 wpt_x86.msi。 这将安装 Windows 性能工具包包含 GPUView。 

WPT MSI 包括下表中所述的文件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">文件</th>
<th align="left">用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>EULA.rtf</em></p></td>
<td align="left"><p>法律协议</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>GPUView.chm</em></p></td>
<td align="left"><p>GPUView 帮助文件</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Readme.txt</em></p></td>
<td align="left"><p>帮助文件中不包含任何其他信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>GPUView.exe</em></p></td>
<td align="left"><p>用于查看视频数据的 ETL 文件的程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>AEplugin.dll</em>， <em>DWMPlugin.dll</em>， <em>MFPlugin.dll</em>， <em>NTPlugin.dll</em>， <em>DxPlugin.dll</em>，和<em>DxgkPlugin.dll</em></p></td>
<td align="left"><p>要解释事件的插件</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>CoreTPlugin.dll</em></p></td>
<td align="left"><p>适用于统计选项对话框插件</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Log.cmd</em></p></td>
<td align="left"><p>若要打开和关闭日志记录的相应信息的脚本</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>SymbolSearchPath.txt</em></p></td>
<td align="left"><p>设置符号路径来解决 stackwalk 和其他事件的文本文件</p></td>
</tr>
</tbody>
</table>

若要使用 GPUView，转到命令行，然后运行 Log.cmd 开始事件日志记录。 然后，运行 Log.cmd 停止日志记录。 这将生成多个事件跟踪的 Windows (\*。ETL) 文件;这些各种流将所有合并在一起到单个文件调用 Merged.etl 即 GPUView 读取。 记录的事件的一些示例包括：

* 所有 CPU 上下文切换，包括堆栈跟踪和切换的原因。
* 所有内核模式进入和退出和堆栈跟踪。
* 所有 GPU 事件按 DirectX 图形内核，包括所有的命令缓冲区提交，并创建资源、 析构，记录锁定和绑定事件。
* 报告的图形驱动程序，如命令缓冲区开始和结束时间，以及针对每个适配器的垂直同步间隔事件。
* 许多其他系统事件可能会影响性能，例如页面错误。

此外可以读取 ETL 文件与 XPerf （这同样是 Windows SDK 的一部分），但是它不能理解的任何 GPU 特定事件。 由于这些日志文件可以是相对较大，您可以使用`Log m`命令这将跳过许多频率非常高的事件。

可以找到详细信息，包括如何下载和使用 GPUView，以便[此处](https://graphics.stanford.edu/~mdfisher/GPUView.html)。 

 

 





