---
title: MSBuild 的 WDK 任务
description: Windows Driver Kit (WDK) 包括在生成过程中通常使用，但通过 Visual Studio 通常不分发的工具。
ms.assetid: 53A5AAC2-A608-4153-9482-D8EF3D05EF04
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c41a5ae6821997fef5d49809758b4105b929236
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358083"
---
# <a name="wdk-tasks-for-msbuild"></a>MSBuild 的 WDK 任务


Windows Driver Kit (WDK) 包括在生成过程中通常使用，但通过 Visual Studio 通常不分发的工具。 使用这些工具登录驱动程序或驱动程序包，实现软件跟踪，或者如何处理和编译的资源或消息文件 （stampinf.exe、 mc.exe、 tracewpp.exe、 binplace.exe 等）。 这些命令行工具需要公开为 MSBuild 作为任务 （包含在目标），以便它们可以在生成过程中运行。 WDK 提供了必要的组件，以便在生成您的驱动程序时，可以作为 MSBuild 任务运行这些工具。

**请注意**  此处列出的 WDK 工具通常用于生成过程中，并具有 MSBuild 任务，有关 WDK 和驱动程序开发非常有用的工具中包含的工具的完整列表，请参阅[Windows 索引驱动程序工具包工具](index-of-windows-driver-kit-tools.md)。

 

WDK 命令行工具支持大量的选项。 每个选项公开为任务参数。 运行任务时，它们也可以从项目文件接收输入。 MSBuild 将执行任务之前设置这些属性。 每个单独的 WDK 任务包装器类创建为项目文件中的这些任务的输入和输出参数可用的.NET 属性。

## <a name="span-idtoolsthathavewdktasksspanspan-idtoolsthathavewdktasksspanspan-idtoolsthathavewdktasksspantools-that-have-wdk-tasks"></a><span id="Tools_that__have_WDK_Tasks"></span><span id="tools_that__have_wdk_tasks"></span><span id="TOOLS_THAT__HAVE_WDK_TASKS"></span>具有 WDK 任务的工具


下表列出了这些工具及其相应的任务、 目标和项名称。

| 工具名称    | 任务名称 | 目标名称    | 项名称      |
|--------------|-----------|----------------|----------------|
| Tracewpp.exe | Wpp       | RunWpp         | ClCompile      |
| StampInf.exe | StampInf  | StampInf       | inf            |
| Mofcomp.exe  | mofcomp   | mofcomp        | mofcomp        |
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

上面的示例中调用**tracewpp.exe**文件**b.c**像执行的命令**tracewpp.exe b.c**。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="tracewpp-task.md" data-raw-source="[TraceWPP task](tracewpp-task.md)">TraceWPP 任务</a></p></td>
<td align="left"><p>WDK 提供 TraceWPP 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 tracewpp.exe 工具。 Tracewpp.exe 工具用于实现<a href="wpp-software-tracing.md" data-raw-source="[WPP Software Tracing](wpp-software-tracing.md)">WPP 软件跟踪</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="stampinf-task.md" data-raw-source="[Stampinf task](stampinf-task.md)">Stampinf 任务</a></p></td>
<td align="left"><p>WDK 提供 StampInf 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 stampinf.exe 工具。 有关 stampinf.exe 工具的信息，请参阅<a href="stampinf.md" data-raw-source="[Stampinf](stampinf.md)">Stampinf</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wmimofck-task.md" data-raw-source="[Wmimofck task](wmimofck-task.md)">Wmimofck 任务</a></p></td>
<td align="left"><p>WDK 提供了 Wmimofck 任务，以便在生成使用 MSBuild 的驱动程序时，可以运行 wmimofck.exe 工具。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="mofcomp-task.md" data-raw-source="[Mofcomp task](mofcomp-task.md)">Mofcomp 任务</a></p></td>
<td align="left"><p>WDK 提供 Mofcomp 任务，以便在生成使用 MSBuld 驱动程序时，可以运行 Mofcomp.exe 工具。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="message-compiler-task.md" data-raw-source="[Message compiler task](message-compiler-task.md)">消息编译器任务</a></p></td>
<td align="left"><p>WDK 提供 MessageCompiler 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 MC.exe 的工具。 有关使用 MC.exe 的信息，请参阅<a href="https://msdn.microsoft.com/library/windows/desktop/aa385638" data-raw-source="[&lt;strong&gt;Message Compiler (MC.exe)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa385638)"><strong>消息编译器 MC.exe</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ctrpp-task.md" data-raw-source="[Ctrpp task](ctrpp-task.md)">Ctrpp 任务</a></p></td>
<td align="left"><p>WDK 提供 Ctrpp 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 ctrpp.exe 工具。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**CTRPP**](https://msdn.microsoft.com/library/windows/desktop/aa372128)

[使用 Wmimofck.exe](https://msdn.microsoft.com/library/windows/hardware/ff565588)

[**消息编译器 (MC.exe)**](https://msdn.microsoft.com/library/windows/desktop/aa385638)

[**mofcomp**](https://msdn.microsoft.com/library/aa392389)

[Stampinf](stampinf.md)

[WPP 预处理器](wpp-preprocessor.md)

 

 






