---
title: MSBuild 的 WDK 任务
description: Windows 驱动程序工具包 (WDK) 包含通常在生成过程中使用的工具，但通常不会与 Visual Studio 一起分发。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37587b5140be70417caa045d97f2ad9bd80ca651
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830093"
---
# <a name="wdk-tasks-for-msbuild"></a>MSBuild 的 WDK 任务

[Windows 驱动程序工具包 (WDK) ](../download-the-wdk.md)包含通常在生成过程中使用的工具，但通常不会与 Visual Studio 一起分发。 这些工具用于签署驱动程序或驱动程序包，实现软件跟踪，或者处理和编译资源或消息文件 ( # A0、mc.exe、tracewpp.exe、binplace.exe 等 ) 。 需要将这些命令行工具公开给 MSBuild，作为 (包含在目标) 中的任务，使其可以在生成过程中运行。 WDK 提供必要的组件，以便在构建驱动程序时可以将这些工具作为 MSBuild 任务运行。

>[!NOTE]
>此处所列的 WDK 工具通常在生成过程中使用，并包含 MSBuild 任务，有关可用于驱动程序开发的 WDK 和工具中包含的工具的完整列表，请参阅 [Windows 驱动程序工具包工具的索引](index-of-windows-driver-kit-tools.md)。

WDK 命令行工具支持大量选项。 每个选项都作为任务参数公开。 当任务运行时，它们还可以从项目文件接收输入。 MSBuild 会在执行任务之前立即设置这些属性。 每个单独的 WDK 任务包装器类创建可用作项目文件中这些任务的输入和输出参数的 .NET 属性。

## <a name="tools-that-have-wdk-tasks"></a>包含 WDK 任务的工具

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

上面的示例将在文件 **b.** 上调用 **tracewpp.exe** ，就像你向发出命令 **tracewpp.exe b.**。

## <a name="in-this-section"></a>在本节中

|主题|描述|
|----|----|
|[TraceWPP 任务](tracewpp-task.md)|WDK 提供 TraceWPP 任务，以便在使用 MSBuild 构建驱动程序时可以运行 tracewpp.exe 工具。 tracewpp.exe 工具用于实现 [WPP 软件跟踪](wpp-software-tracing.md)|
|[Stampinf 任务](stampinf-task.md)|WDK 提供 StampInf 任务，以便在使用 MSBuild 构建驱动程序时可以运行 stampinf.exe 工具。 有关 stampinf.exe 工具的信息，请参阅 [Stampinf](stampinf.md)|
|[Wmimofck 任务](wmimofck-task.md)|WDK 提供 Wmimofck 任务，因此，在使用 MSBuild 构建驱动程序时，可以运行 wmimofck.exe 工具。|
|[Mofcomp 任务](mofcomp-task.md)|WDK 提供 Mofcomp.exe 任务，以便在使用 MSBuld 构建驱动程序时可以运行 Mofcomp.exe 工具。|
|[消息编译器任务](message-compiler-task.md)|WDK 提供 MessageCompiler 任务，以便在使用 MSBuild 构建驱动程序时可以运行 MC.exe 工具。 有关使用 MC.exe 的信息，请参阅 [Message 编译器 ( # A1) ](/windows/desktop/WES/message-compiler--mc-exe-)|
|[Ctrpp 任务](ctrpp-task.md)|WDK 提供 Ctrpp 任务，以便在使用 MSBuild 构建驱动程序时可以运行 ctrpp.exe 工具。|

## <a name="related-topics"></a>相关主题

[CTRPP](/windows/desktop/PerfCtrs/ctrpp)

[使用 Wmimofck.exe](../kernel/using-wmimofck-exe.md)

[消息编译器 (MC.exe)](/windows/desktop/WES/message-compiler--mc-exe-)

[mofcomp](/windows/desktop/WmiSdk/mofcomp)

[Stampinf](stampinf.md)

[WPP 预处理器](wpp-preprocessor.md)
