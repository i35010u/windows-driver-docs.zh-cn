---
title: WPP 软件跟踪
description: 本部分介绍如何使用 Windows 软件跟踪预处理器（WPP）来跟踪软件组件跟踪提供程序的操作。
ms.assetid: dab776b3-bac9-4157-a530-6e48868ba900
keywords:
- Windows 软件跟踪预处理器 WDK
- WPP 软件跟踪 WDK
- 软件跟踪 WDK，WPP
- 内核模式 WPP WDK 软件跟踪
- Windows 软件跟踪预处理器 WDK，关于 WPP
- WPP 软件跟踪 WDK，关于 WPP
- 默认 WPP 软件跟踪
- 跟踪 WDK，WPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb1772fa4a4ccfbedd739a610d1bae7207aa4d92
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769651"
---
# <a name="wpp-software-tracing"></a>WPP 软件跟踪


本节介绍如何使用*Windows 软件跟踪预处理器*（WPP）来跟踪软件组件（[跟踪提供程序](trace-provider.md)）的操作。 跟踪提供程序可以是以下项之一：

-   内核模式驱动程序。

-   用户模式驱动程序、应用程序或动态链接库（DLL）。

WPP 软件跟踪通过添加简化跟踪提供程序操作的方法来补充和增强[WMI 事件跟踪](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-event-tracing)。 这是一种有效的机制，用于跟踪提供程序记录实时二进制消息。 然后，可以将记录的消息转换为跟踪提供程序操作的可读跟踪。

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
<td align="left"><p>WPP 软件跟踪主要用于调试开发过程中的代码。 如果希望发布可由对结构化 ETW 事件感兴趣的应用程序使用的事件，以及在开发期间进行跟踪，请使用以下内容：</p>
<ul>
<li>对于内核模式驱动程序，请使用<a href="event-tracing-for-windows--etw-.md" data-raw-source="[Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)">Windows 事件跟踪（ETW）</a> API。</li>
<li>对于用户模式驱动程序或应用程序，请使用<a href="https://docs.microsoft.com/windows/desktop/ETW/event-tracing-portal" data-raw-source="[Event Tracing](https://docs.microsoft.com/windows/desktop/ETW/event-tracing-portal)">事件跟踪</a>（Windows 桌面） API。</li>
</ul>
有关详细信息，请参阅<a href="tools-for-software-tracing.md" data-raw-source="[When should I use WPP Software Tracing or the Event Tracing for Windows (ETW) API?](tools-for-software-tracing.md)">何时应使用 WPP 软件跟踪或 Windows 事件跟踪（ETW） API？</a></td>
</tr>
</tbody>
</table>

 

使用 WPP 软件跟踪来记录消息的方式类似于使用 Windows 事件日志服务。 驱动程序在日志文件中记录消息 ID 和未格式化的二进制数据。 然后，postprocessor 将日志文件中的信息转换为可读的形式。 但是，WPP 软件跟踪支持的消息格式比事件日志记录服务支持的格式更强且更灵活。 例如，WPP 软件跟踪为 IP 地址、Guid、系统 Id、时间戳和其他有用的数据类型提供内置支持。 此外，用户还可以添加与应用程序相关的自定义数据类型。

Microsoft Windows 2000 和更高版本的 Windows 支持 WPP 软件跟踪。

### <a name="an-overview-of-the-wpp-software-tracing-process"></a>WPP 软件跟踪过程概述

向驱动程序或应用程序添加 WPP 软件跟踪的基本过程包括以下步骤。 如果使用 WDK 中提供的一个 Visual Studio 模板来创建 WDF 驱动程序，将完成大部分工作。

-   定义唯一地将驱动程序或应用程序标识为[跟踪提供](trace-provider.md)程序的控件 GUID。 提供程序在其[WPP \_ 控制 \_ guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏的定义和[Tracelog](tracelog.md)或其他[跟踪控制器](trace-controller.md)使用的相关控件文件中指定此 GUID。

-   如向[Windows 驱动程序添加 Wpp 软件跟踪](adding-wpp-software-tracing-to-a-windows-driver.md)和[Wpp 软件跟踪参考](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556205(v=vs.85))中所述，将所需的与 wpp 相关的 C 预处理器指令和 WPP 宏调用添加到提供程序的源文件中。

-   修改 Visual Studio 项目以运行 WPP 预处理器并构建驱动程序，如向 Windows 驱动程序添加 WPP 软件跟踪[步骤 6](adding-wpp-software-tracing-to-a-windows-driver.md#step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution)中所述。 可以参考[WPP 预处理器](wpp-preprocessor.md)以获取更多生成时间选项。

-   安装驱动程序或组件。 启动跟踪会话并记录跟踪消息。 使用软件跟踪工具，如[TraceView](traceview.md)、 [Tracelog](tracelog.md)、 [Tracefmt](tracefmt.md)和[Tracepdb](tracepdb.md) ，以配置、启动和停止跟踪会话并显示和筛选跟踪消息。 这些工具包含在 Windows 驱动程序工具包（WDK）中。

## <a name="in-this-section"></a>本部分内容


-   [将 WPP 软件跟踪添加到 Windows 驱动程序](adding-wpp-software-tracing-to-a-windows-driver.md)
-   [用于记录跟踪的即时跟踪记录器](using-wpp-recorder.md)
-   [在跟踪提供程序中使用 WPP 软件跟踪](using-wpp-software-tracing-in-a-trace-provider.md)
-   [将 WPP 宏添加到跟踪提供程序](adding-wpp-macros-to-a-trace-provider.md)
-   [WPP 预处理器](wpp-preprocessor.md)
-   [WDF 驱动程序的跟踪和诊断能力](tracing-and-diagnosability-for-wdf-drivers.md)

**注意**   Windows 事件跟踪（ETW）和 WPP 支持大多数类型的内核模式和用户模式驱动程序。 但 ETW 和 WPP 使用某些类型的驱动程序（如微型端口驱动程序）不可用的类型。 若要确定是否支持某个特定的驱动程序类型，请将基本的 WPP 宏添加到该驱动程序，如[WPP \_ INIT \_ 跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))和[wpp \_ 清除](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))。 如果代码由于未定义所使用的类型而无法编译，则 ETW 和 WPP 不能支持驱动程序类型。

有关 ETW 的详细信息，请参阅[Windows 事件跟踪](https://docs.microsoft.com/windows-hardware/test/wpt/event-tracing-for-windows)。

**注意**WPP 跟踪提供程序一次只能由一个跟踪会话启用。 有关详细信息，请参阅[WPP 提供程序](https://docs.microsoft.com/windows/desktop/ETW/about-event-tracing#providers)。

有关支持 WPP 软件跟踪的[WMI 库支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)的信息，请参阅：

[**WmiQueryTraceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-wmiquerytraceinformation)

[**WmiTraceMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-wmitracemessage)

[**WmiTraceMessageVa**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-wmitracemessageva)

 

 





