---
title: MSBuild 的 WDK 任务
description: Windows 驱动程序工具包 (WDK) 包含通常在生成过程中使用的工具，但通常不会与 Visual Studio 一起分发。
ms.assetid: 53A5AAC2-A608-4153-9482-D8EF3D05EF04
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7add39e8815917b9024bfbd7cde9c71528911dd5
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382761"
---
# <a name="wdk-tasks-for-msbuild"></a>MSBuild 的 WDK 任务


Windows 驱动程序工具包 (WDK) 包含通常在生成过程中使用的工具，但通常不会与 Visual Studio 一起分发。 这些工具用于签署驱动程序或驱动程序包，实现软件跟踪，或者处理和编译资源或消息文件 ( # A0、mc.exe、tracewpp.exe、binplace.exe 等 ) 。 需要将这些命令行工具公开给 MSBuild，作为 (包含在目标) 中的任务，使其可以在生成过程中运行。 WDK 提供必要的组件，以便在构建驱动程序时可以将这些工具作为 MSBuild 任务运行。

**注意**   此处所列的 WDK 工具通常在生成过程中使用，并包含 MSBuild 任务，有关可用于驱动程序开发的 WDK 和工具中包含的工具的完整列表，请参阅[Windows 驱动程序工具包工具的索引](index-of-windows-driver-kit-tools.md)。

 

WDK 命令行工具支持大量选项。 每个选项都作为任务参数公开。 当任务运行时，它们还可以从项目文件接收输入。 MSBuild 会在执行任务之前立即设置这些属性。 每个单独的 WDK 任务包装器类创建可用作项目文件中这些任务的输入和输出参数的 .NET 属性。

## <a name="span-idtools_that__have_wdk_tasksspanspan-idtools_that__have_wdk_tasksspanspan-idtools_that__have_wdk_tasksspantools-that-have-wdk-tasks"></a><span id="Tools_that__have_WDK_Tasks"></span><span id="tools_that__have_wdk_tasks"></span><span id="TOOLS_THAT__HAVE_WDK_TASKS"></span>包含 WDK 任务的工具


下表列出了这些工具及其相应的任务、目标和项的名称。

| 工具名称    | 任务名称 | 目标名称    | 项名称      |
|--------------|-----------|----------------|----------------|
| Tracewpp.exe | Wpp       | RunWpp         | ClCompile      |
| StampInf.exe | StampInf  | StampInf       | 遵从            |
| Mofcomp.exe  | Mofcomp.exe   | Mofcomp.exe        | Mofcomp.exe        |
| Wmimofck.exe | Wmimofck  | Wmimofck       | Wmimofck       |
| mc.exe       | Mc        | MessageCompile | MessageCompile |
| Ctrpp.exe    | Ctrpp     | Ctrpp          | Ctrpp          |

 

下面的示例演示如何调用工具。

```XML
<ItemGroup>
    <ClCompile Include="a.c" />
    <ClCompile Include="b.c">
        <WppEnabled>true</WppEnabled>
    </ClCompile>
</ItemGroup>
```

上面的示例将在文件**b.** 上调用**tracewpp.exe** ，就像你向发出命令**tracewpp.exe b.**。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="tracewpp-task.md" data-raw-source="[TraceWPP task](tracewpp-task.md)">TraceWPP 任务</a></p></td>
<td align="left"><p>WDK 提供 TraceWPP 任务，以便在使用 MSBuild 构建驱动程序时可以运行 tracewpp.exe 工具。 tracewpp.exe 工具用于实现 <a href="wpp-software-tracing.md" data-raw-source="[WPP Software Tracing](wpp-software-tracing.md)">WPP 软件跟踪</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="stampinf-task.md" data-raw-source="[Stampinf task](stampinf-task.md)">Stampinf 任务</a></p></td>
<td align="left"><p>WDK 提供 StampInf 任务，以便在使用 MSBuild 构建驱动程序时可以运行 stampinf.exe 工具。 有关 stampinf.exe 工具的信息，请参阅 <a href="stampinf.md" data-raw-source="[Stampinf](stampinf.md)">Stampinf</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wmimofck-task.md" data-raw-source="[Wmimofck task](wmimofck-task.md)">Wmimofck 任务</a></p></td>
<td align="left"><p>WDK 提供 Wmimofck 任务，因此，在使用 MSBuild 构建驱动程序时，可以运行 wmimofck.exe 工具。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="mofcomp-task.md" data-raw-source="[Mofcomp task](mofcomp-task.md)">Mofcomp 任务</a></p></td>
<td align="left"><p>WDK 提供 Mofcomp.exe 任务，以便在使用 MSBuld 构建驱动程序时可以运行 Mofcomp.exe 工具。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="message-compiler-task.md" data-raw-source="[Message compiler task](message-compiler-task.md)">消息编译器任务</a></p></td>
<td align="left"><p>WDK 提供 MessageCompiler 任务，以便在使用 MSBuild 构建驱动程序时可以运行 MC.exe 工具。 有关使用 MC.exe 的信息，请参阅 <a href="https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-" data-raw-source="[&lt;strong&gt;Message Compiler (MC.exe)&lt;/strong&gt;](/windows/desktop/WES/message-compiler--mc-exe-)"><strong>Message 编译器 ( # A1) </strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ctrpp-task.md" data-raw-source="[Ctrpp task](ctrpp-task.md)">Ctrpp 任务</a></p></td>
<td align="left"><p>WDK 提供 Ctrpp 任务，以便在使用 MSBuild 构建驱动程序时可以运行 ctrpp.exe 工具。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**CTRPP**](/windows/desktop/PerfCtrs/ctrpp)

[使用 Wmimofck.exe](../kernel/using-wmimofck-exe.md)

[**消息编译器 (MC.exe)**](/windows/desktop/WES/message-compiler--mc-exe-)

[**mofcomp**](/windows/desktop/WmiSdk/mofcomp)

[Stampinf](stampinf.md)

[WPP 预处理器](wpp-preprocessor.md)

 

