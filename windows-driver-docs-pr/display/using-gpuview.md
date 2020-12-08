---
title: 使用 GPUView
description: 使用 GPUView
ms.date: 01/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: fb751e236099d2f38325401895ba7a4a7d1348ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803893"
---
# <a name="using-gpuview"></a>使用 GPUView

GPUView (*GPUView.exe*) 是一个开发工具，用于确定图形处理单元 (GPU) 和 CPU 的性能。 它在 (DMA) 缓冲区处理以及视频硬件上的所有其他视频处理方面了解有关直接内存访问的性能。 GPUView 适用于开发符合 Windows Vista 显示器驱动程序模型的显示驱动程序。 Windows 7 操作系统的发行版中引入了 GPUView。

Windows 性能工具包附带了与之相关联的 GPUView 和其他文件 (WPT) 为 WPT MSI 的可安装选项。 GPUView 二进制文件可用于基于 x86、基于 x64 和基于 x86 的体系结构。 例如， *Wpt \_x86.msi* 适用于 x86 平台。 

你还可以将 GPUView 下载为 Windows 7 SDK 的一部分。 安装 SDK 后，你将需要中转到 C:\Program Files\Microsoft SDKs\Windows\v7.0\bin 并运行 wpt_x64.msi 或 wpt_x86.msi。 这将安装 Windows 性能工具包，其中包含 GPUView。 

WPT MSI 包括下表中所述的文件。

|文件|目的|
|----|----|
|EULA.rtf|法律协议|
|GPUView|GPUView 帮助文件|
|Readme.txt|帮助文件中未包含的任何其他信息|
|GPUView.exe|用于查看具有视频数据的 ETL 文件的程序|
|AEplugin.dll、DWMPlugin.dll、MFPlugin.dll、NTPlugin.dll、DxPlugin.dll 和 DxgkPlugin.dll|用于解释事件的插件|
|CoreTPlugin.dll|"统计选项" 对话框的插件|
|Log .cmd|用于打开和关闭日志记录的适当信息的脚本|
|SymbolSearchPath.txt|一个文本文件，该文件设置用于解析 stackwalk 和其他事件的符号路径|

若要使用 GPUView，请切换到命令行并运行 Log .cmd，开始事件日志记录。 然后再次运行 Log .cmd 以停止日志记录。 这将为 Windows (生成多个事件跟踪 \* 。ETL) 文件;这些不同的流将全部合并到一个名为 GPUView 的文件中。 记录的事件的一些示例包括：

* 所有 CPU 上下文切换，包括堆栈跟踪和切换的原因。
* 所有内核模式进入和退出，并具有堆栈跟踪。
* DirectX 图形内核记录的所有 GPU 事件，包括所有命令缓冲区提交和资源创建、破坏、锁定和绑定事件。
* 图形驱动程序报告的事件，例如每个适配器的命令缓冲区开始和结束时间以及垂直同步间隔。
* 可能影响性能的其他许多系统事件，如页错误。

你还可以读取具有 XPerf (的 ETL 文件，该文件与 Windows SDK) 的一部分类似，但它不会了解特定于 GPU 的任何事件。 由于这些日志文件可能相对较大，因此你可以使用 `Log m` 命令，而不是将跳过许多非常高的频率事件。

有关如何下载和使用 GPUView 的详细信息，请参阅 Matthew 费舍尔的 site， [Matt 的 Webcorner](https://graphics.stanford.edu/~mdfisher/GPUView.html)，他讨论了如何创建 GPUView。
