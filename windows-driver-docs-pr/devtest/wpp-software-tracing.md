---
title: WPP 软件跟踪
description: 本部分介绍如何使用 Windows 软件跟踪预处理器 (WPP) 来跟踪软件组件跟踪提供程序的操作。
ms.assetid: dab776b3-bac9-4157-a530-6e48868ba900
keywords:
- Windows 软件跟踪预处理器 WDK
- 跟踪 WDK WPP 软件
- 跟踪 WDK，WPP 软件
- 内核模式 WPP WDK 软件跟踪
- Windows 软件跟踪预处理器 WDK，有关 WPP
- 跟踪 WDK，有关 WPP WPP 软件
- 默认 WPP 软件跟踪
- 跟踪 WDK WPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f72f3818d7ef207f0edb0681b2adc37401326bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524680"
---
# <a name="wpp-software-tracing"></a>WPP 软件跟踪


本部分介绍如何使用*Windows 软件跟踪预处理器*(WPP) 来跟踪软件组件的操作 ([跟踪提供程序](trace-provider.md))。 跟踪提供程序可以是以下值之一：

-   内核模式驱动程序。

-   用户模式驱动程序、 应用程序或动态链接库 (DLL)。

WPP 软件跟踪补充并增强[WMI 事件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff566350)通过添加方法来简化跟踪的跟踪提供程序操作。 它是用于跟踪提供程序记录实时二进制消息有效机制。 随后可将记录的消息转换的操作的跟踪提供程序的可读跟踪。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">何时应使用 WPP 软件跟踪？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WPP 软件跟踪主要适用于在开发过程中调试代码。 如果你想要发布的可供对结构化的 ETW 事件，除了在开发期间，跟踪感兴趣的应用程序事件使用以下命令：</p>
<ul>
<li>有关内核模式驱动程序，使用<a href="event-tracing-for-windows--etw-.md" data-raw-source="[Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)">事件跟踪 Windows (ETW)</a> API。</li>
<li>对于用户模式驱动程序或应用程序，将<a href="https://msdn.microsoft.com/library/windows/desktop/bb968803" data-raw-source="[Event Tracing](https://msdn.microsoft.com/library/windows/desktop/bb968803)">事件跟踪</a>（Windows 桌面版） API。</li>
</ul>
有关详细信息，请参阅<a href="tools-for-software-tracing.md" data-raw-source="[When should I use WPP Software Tracing or the Event Tracing for Windows (ETW) API?](tools-for-software-tracing.md)">时应使用 WPP 软件跟踪或事件跟踪 Windows (ETW) API？</a></td>
</tr>
</tbody>
</table>

 

使用 WPP 软件跟踪日志记录消息将类似于使用 Windows 事件日志记录服务。 该驱动程序日志文件中记录消息 ID 和未格式化的二进制数据。 随后，后处理器将日志文件中的信息转换为可读的形式。 但是，WPP 软件跟踪支持更多的能力和灵活性大于所支持的事件日志记录服务的消息格式。 例如，WPP 软件跟踪提供 IP 地址、 Guid、 system Id、 时间戳和其他有用的数据类型的内置的支持。 此外，用户可以添加到其应用程序相关的自定义数据类型。

Microsoft Windows 2000 和更高版本的 Windows 支持 WPP 软件跟踪。

### <a name="an-overview-of-the-wpp-software-tracing-process"></a>WPP 软件跟踪过程的概述

将 WPP 软件跟踪添加到驱动程序或应用程序的基本过程包括以下步骤。 如果使用 Visual Studio 模板提供在 WDK 中用于创建 WDF 驱动程序时，大部分的工作是出于您。

-   定义一个控件唯一标识该驱动程序或应用程序作为 GUID[跟踪提供程序](trace-provider.md)。 提供程序在其定义中指定此 GUID [WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)宏和中使用的相关的控件文件[Tracelog](tracelog.md)或另一个[跟踪控制器](trace-controller.md)。

-   添加所需 WPP 相关 C 预处理器指令和 WPP 宏调用到提供程序的源文件，如中所述[添加到 Windows 驱动程序 WPP 软件跟踪](adding-wpp-software-tracing-to-a-windows-driver.md)并在[WPP 软件跟踪引用](https://msdn.microsoft.com/library/windows/hardware/ff556205).

-   修改 Visual Studio 项目，以运行 WPP 预处理器并生成该驱动程序，如中所述[第 6 步](adding-wpp-software-tracing-to-a-windows-driver.md#step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution)添加到 Windows 驱动程序 WPP 软件跟踪。 您可以参考[WPP 预处理器](wpp-preprocessor.md)的生成时间选项的详细信息。

-   安装驱动程序或组件。 启动跟踪会话，并记录跟踪消息。 使用工具进行软件跟踪，例如[TraceView](traceview.md)， [Tracelog](tracelog.md)， [Tracefmt](tracefmt.md)，以及[Tracepdb](tracepdb.md)配置、 启动和停止跟踪会话还可以显示和筛选跟踪消息。 这些工具包括 Windows Driver Kit (WDK) 中。

## <a name="in-this-section"></a>本部分内容


-   [添加 WPP 软件跟踪对 Windows 驱动程序](adding-wpp-software-tracing-to-a-windows-driver.md)
-   [日志中记录跟踪的即时跟踪记录器](using-wpp-recorder.md)
-   [使用 WPP 软件在跟踪提供程序中进行跟踪](using-wpp-software-tracing-in-a-trace-provider.md)
-   [将 WPP 宏添加到跟踪提供程序](adding-wpp-macros-to-a-trace-provider.md)
-   [WPP 预处理器](wpp-preprocessor.md)
-   [跟踪和 WDF 驱动程序的诊断能力](tracing-and-diagnosability-for-wdf-drivers.md)

**请注意**  事件跟踪 Windows (ETW) 和 WPP 支持大多数类型的内核模式和用户模式驱动程序。 但是，ETW 和 WPP 使用不适用于某些类型的驱动程序，例如微型端口驱动程序的类型。 若要确定是否支持特定驱动程序类型，基本 WPP 将宏添加到驱动程序，如[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)并[WPP\_清理](https://msdn.microsoft.com/library/windows/hardware/ff556179)。 如果由于未定义使用的类型，不会进行编译代码，ETW 和 WPP 不能支持的驱动程序类型。
有关 ETW 的详细信息，请参阅[事件跟踪](https://go.microsoft.com/fwlink/p/?linkid=179202)Windows SDK 文档中。

**请注意**WPP 跟踪提供程序只能由一个跟踪会话一次启用。 请参阅[WPP 提供程序](https://msdn.microsoft.com/library/windows/desktop/aa363668#providers)有关详细信息。

璝惠[WMI 库支持例程](https://msdn.microsoft.com/library/windows/hardware/ff566359)的支持 WPP 软件跟踪，请参阅：

[**WmiQueryTraceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff565820)

[**WmiTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff565836)

[**WmiTraceMessageVa**](https://msdn.microsoft.com/library/windows/hardware/ff566340)

 

 





