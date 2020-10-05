---
title: 在 UMDF 驱动程序中使用 WPP 软件跟踪
description: 在 UMDF 驱动程序中使用 WPP 软件跟踪
ms.assetid: d8469d29-dfc3-41b9-a72d-9dafb3e70123
keywords:
- 软件跟踪 WDK，基于框架的驱动程序
- 调试驱动程序 WDK UMDF、软件跟踪
- 跟踪 WDK，基于框架的驱动程序
- WPP 软件跟踪 WDK，基于框架的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41509d62e9d2119844e50ebe65ab4c8491ae48c7
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733603"
---
# <a name="using-wpp-software-tracing-in-umdf-drivers"></a>在 UMDF 驱动程序中使用 WPP 软件跟踪


通过[WPP 软件跟踪](../devtest/wpp-software-tracing.md)，你可以添加跟踪消息，以帮助你调试驱动程序。 此外，框架的 [事件记录器](using-the-framework-s-event-logger.md) 提供数以百计的跟踪消息，您可以查看这些消息。

您可以通过使用 [TraceView](../devtest/traceview.md) 或 [Tracelog](../devtest/tracelog.md)来查看跟踪消息。 你还可以向 [内核调试器发送跟踪消息](../devtest/how-do-i-send-trace-messages-to-a-kernel-debugger-.md)。

### <a name="adding-tracing-messages-to-your-driver"></a>向驱动程序添加跟踪消息

若要将跟踪消息添加到基于框架的驱动程序，必须执行以下操作：

-   向每个包含任何 WPP 宏的驱动程序源文件添加** \# 包含**指令。 此指令必须标识 [跟踪消息标头 (TMH) 文件](../devtest/trace-message-header-file.md)。 文件名必须具有 tmh 格式的 &lt; *驱动程序*名称。 &gt;

    例如，如果驱动程序包含两个源文件（称为 *mydriver1.inf* 和 *mydriver2.inf 会被*），则 *mydriver1.inf* 必须包含：

    `#include "MyDriver1.tmh"`

    和 *mydriver2.inf 会被* 必须包含：

    `#include "MyDriver2.tmh"`

    在 Microsoft Visual Studio 中生成驱动程序时，WPP 预处理器会生成 tmh 文件。

-   在标头文件中定义 [WPP \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 宏。 此宏为驱动程序的跟踪消息定义 GUID 和 [跟踪标志](../devtest/trace-flags.md) 。 为每个基于 UMDF 的示例驱动程序 (，内部 .h 头文件包含此宏。 ) 

-   在驱动程序的 DllMain 例程中包括 [WPP \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85)) 宏。 此宏激活驱动程序中的软件跟踪。 为每个基于 UMDF 的示例驱动程序 (，DllSup 标头文件包含此宏。 ) 

-   在驱动程序的 DllMain 例程中包括 [WPP \_ 清理](/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85)) 宏。 此宏停用驱动程序中的软件跟踪。 为每个基于 UMDF 的示例驱动程序 (，DllSup 标头文件包含此宏。 ) 

-   使用驱动程序中的 [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)) 宏或宏的 [自定义版本](../devtest/can-i-customize-dotracemessage-.md) 来创建跟踪消息。 为每个基于 UMDF 的示例驱动程序 (，内部 .h 头文件包含自定义宏。 ) 

-   打开驱动程序项目的属性页。 在“解决方案资源管理器”中右键单击驱动程序项目，并选择“属性”  。 在驱动程序的属性页中，单击 " **配置属性**"，然后单击 " **Wpp**"。 在 " **常规** " 菜单下，将 " **运行 WPP 跟踪** " 设置为 "是"。 在 " **文件选项** " 菜单下，还应指定框架的 WPP 模板文件，例如：

    ```cpp
    {km-WdfDefault.tpl}*.tmh
    ```

有关将跟踪消息添加到驱动程序的详细信息，请参阅向 [驱动程序添加 WPP 宏](../devtest/adding-wpp-macros-to-a-trace-provider.md)。

### <a name="sample-drivers-that-use-wpp-software-tracing"></a>使用 WPP 软件跟踪的示例驱动程序

WDK 中所有基于 UMDF 的示例驱动程序都提供了 DllSup、Internal 和源文件，它们可启用 WPP 软件跟踪。 其中的大多数示例驱动程序也使用自定义的宏来创建跟踪消息。

### <a name="viewing-your-drivers-trace-messages"></a>查看驱动程序的跟踪消息

如果已将跟踪消息添加到了驱动程序，则该驱动程序是 [跟踪提供程序](../devtest/trace-provider.md)。 可以使用 [跟踪控制器](../devtest/trace-controller.md)（如 [Tracelog](../devtest/tracelog.md)）来控制 [跟踪会话](../devtest/trace-session.md) 并创建 [跟踪日志](../devtest/trace-log.md)。 可以使用 [跟踪使用者](../devtest/trace-consumer.md)（如 [Tracefmt](../devtest/tracefmt.md)）来查看消息。

有关如何使用软件跟踪工具的详细信息，请参阅 [软件跟踪工具调查](../devtest/survey-of-software-tracing-tools.md)。

### <a name="viewing-the-umdf-trace-log"></a>查看 UMDF 跟踪日志

UMDF 日志文件为% windir% \\ system32 日志 \\ 文件 \\ WUDF \\ WUDFTrace。

**注意**   从 UMDF 2.15 开始，日志目录为 *% ProgramData%* \\ Microsoft \\ WDF。

 

可以使用 [TraceView](../devtest/traceview.md) 或 [Tracelog](../devtest/tracelog.md)查看 UMDF 日志文件。 这两种工具都需要跟踪消息格式 (TMF) 文件格式跟踪日志的消息。 TMF 文件在 WDK 中的 " \\ 工具" \\ 跟踪子目录下提供。  (在 TraceView 中，UMDF 显示为名称为 "UMDF-Framework Trace" 或 "Framework Trace" 的命名提供程序，具体取决于 UMDF 版本。 ) 

借助[WDF 验证](../devtest/wdf-verifier-control-application.md)程序，你可以将跟踪消息同时发送到 UMDF 跟踪日志和内核调试器。  (不应在[Tracelog](../devtest/tracelog.md)中使用 **-kd**选项将跟踪消息发送到内核调试器，因为**Tracelog**可能会中断 UMDF 内的跟踪日志记录。 ) 

你还可以使用 [**！ wmitrace**](../debugger/wmi-tracing-extensions--wmitrace-dll-.md) 调试器扩展来查看调试器中 [的跟踪消息](../devtest/how-do-i-send-trace-messages-to-a-kernel-debugger-.md) ：

1.  在 WinDbg 中，附加到承载驱动程序的 WUDFHost 的实例。 有关详细信息，请参阅 [如何启用 UMDF 驱动程序调试](enabling-a-debugger.md)。
2.  如果驱动程序使用版本1.11 或更高版本，并且使用的是 Windows 8 或更高版本的内核调试器，则可以跳过此步骤。 如果驱动程序使用的是早于1.11 的版本，请使用 [**！ wmitrace**](../debugger/-wmitrace-tmffile.md) 或 [**！ wmitrace**](../debugger/-wmitrace-searchpath.md) 来指定特定于平台的跟踪消息格式 (. tmf) 文件或 tmf 文件的路径。 Tmf 文件位于 WDK 中特定于平台的子目录中。

3.  使用 [**！ wmitrace logdump**](../debugger/-wmitrace-logdump.md) 命令来显示跟踪缓冲区的内容：

    ```cpp
    !wmitrace.logdump WudfTrace
    ```

### <a name="controlling-trace-messages"></a>控制跟踪消息

可以使用 [WDF 验证](../devtest/wdf-verifier-control-application.md) 程序提供的用户界面或通过修改注册表值来控制 UMDF 跟踪消息。 应尽可能使用 **WDF 验证** 程序接口，因为在 UMDF 的未来版本中，注册表值可能会更改。 此外，不应在 INF 文件或驱动程序的代码中访问这些值。

目前，你可以修改以下注册表值，这些值位于 **HKLM \\ SOFTWARE \\ Microsoft \\ Windows NT \\ CurrentVersion \\ WUDF** 注册表项下：

-   **LogEnable**值控制 UMDF 是否为驱动程序创建跟踪日志。 如果此值设置为1，则 UMDF 会创建跟踪日志。

-   **LogLevel**值控制 UMDF 跟踪消息所包含的信息量。 **LogLevel**的默认值为3，这将导致 UMDF 跟踪消息包含错误消息和警告消息。 将此值设置为7可包含错误消息和警告消息，以及非错误信息性消息。 将它设置为15以包含 UMDF 能够提供的所有跟踪信息。

-   **LogKd**值控制 UMDF 是否向内核调试器发送跟踪消息。 如果 **LogKd** 设置为1，则 UMDF 会将其跟踪消息发送到内核调试器。

-   **LogFlushPeriodSeconds**值指定跟踪消息写入跟踪日志的频率（以秒为单位）。

-   **LogMinidumpType**值包含标志，这些标志指定小型转储文件（如果生成）将包含的信息类型。 有关这些标志的详细信息，请参阅 [小型转储 \_ 类型](/windows/win32/api/minidumpapiset/ne-minidumpapiset-minidump_type) 枚举。

你可能会在 **HKLM \\ SOFTWARE \\ Microsoft \\ Windows NT \\ CurrentVersion \\ WUDF** 注册表项下找到其他注册表值。 不应修改这些值。

