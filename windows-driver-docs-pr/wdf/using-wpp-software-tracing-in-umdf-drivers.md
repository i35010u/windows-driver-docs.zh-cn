---
title: 在 UMDF 驱动程序中使用 WPP 软件跟踪
description: 在 UMDF 驱动程序中使用 WPP 软件跟踪
ms.assetid: d8469d29-dfc3-41b9-a72d-9dafb3e70123
keywords:
- 跟踪 WDK，基于框架的驱动程序软件
- 调试 WDK UMDF 驱动程序软件跟踪
- 跟踪 WDK，基于框架的驱动程序
- WPP 软件跟踪 WDK，基于框架的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e72c83d299be4136ed63ac199e046bac9fc6f06
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372149"
---
# <a name="using-wpp-software-tracing-in-umdf-drivers"></a>在 UMDF 驱动程序中使用 WPP 软件跟踪


[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)，可以添加跟踪消息，以帮助您调试您的驱动程序。 此外，框架的[事件记录器](using-the-framework-s-event-logger.md)提供了数百个您可以查看的跟踪消息。

可以通过查看跟踪消息[TraceView](https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview)或[Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)。 此外可以[将跟踪消息发送到内核调试程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-do-i-send-trace-messages-to-a-kernel-debugger-)。

### <a name="adding-tracing-messages-to-your-driver"></a>将跟踪消息到您的驱动程序添加

若要将跟踪消息添加到您基于 framework 的驱动程序，必须：

-   添加 **\#包括**到每个驱动程序的源代码文件包含任何 WPP 宏指令。 此指令必须标识[跟踪消息标头 (TMH) 文件](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-message-header-file)。 文件名称的格式必须&lt;*驱动程序的源的文件名*&gt;.tmh。

    例如，如果您的驱动程序由两个源文件组成，称为*MyDriver1.c*并*MyDriver2.c*，然后*MyDriver1.c*必须包含：

    `#include "MyDriver1.tmh"`

    并*MyDriver2.c*必须包含：

    `#include "MyDriver2.tmh"`

    生成您在 Microsoft Visual Studio 中的驱动程序时，预处理器 WPP 生成.tmh 文件。

-   定义[WPP\_控制\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))标头文件中的宏。 此宏可定义 GUID 并[跟踪标志](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-flags)用于驱动程序的跟踪的消息。 （对于每个 WDK 的基于 UMDF 的示例驱动程序，Internal.h 标头文件包括此宏。）

-   包括[WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))驱动程序的 DllMain 例程中的宏。 此宏将激活软件驱动程序中的跟踪。 （对于每个 WDK 的基于 UMDF 的示例驱动程序，DllSup.h 标头文件包括此宏。）

-   包括[WPP\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))驱动程序的 DllMain 例程中的宏。 此宏将停用软件驱动程序中的跟踪。 （对于每个 WDK 的基于 UMDF 的示例驱动程序，DllSup.h 标头文件包括此宏。）

-   使用[ **DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏，或[自定义的版本](https://docs.microsoft.com/windows-hardware/drivers/devtest/can-i-customize-dotracemessage-)的驱动程序来创建跟踪消息中的宏。 （对于每个 WDK 的基于 UMDF 的示例驱动程序，Internal.h 标头文件包括一个自定义的宏。）

-   打开您的驱动程序项目的属性页。 在“解决方案资源管理器”中右键单击驱动程序项目，并选择**属性**。 在驱动程序的属性页中，单击**配置属性**，然后**Wpp**。 下**常规**菜单中，设置**运行 WPP 跟踪**为是。 下**文件选项**菜单中，你还应指定框架的 WPP 模板文件，例如：

    ```cpp
    {km-WdfDefault.tpl}*.tmh
    ```

有关将跟踪消息添加到您的驱动程序的详细信息，请参阅[添加到驱动程序 WPP 宏](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-wpp-macros-to-a-trace-provider)。

### <a name="sample-drivers-that-use-wpp-software-tracing"></a>使用 WPP 软件跟踪的示例驱动程序

所有基于 UMDF 的示例驱动程序 WDK 中提供 DllSup.h、 Internal.h 和源启用 WPP 软件跟踪的文件。 大多数这些示例驱动程序还使用自定义的宏来创建跟踪消息。

### <a name="viewing-your-drivers-trace-messages"></a>查看您的驱动程序的跟踪消息

跟踪消息添加到您的驱动程序后，该驱动程序是否[跟踪提供程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-provider)。 可以使用[跟踪控制器](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-controller)，如[Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)，用于控制[跟踪会话](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-session)并创建[跟踪日志](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-log)。 可以使用[跟踪使用者](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-consumer)，如[Tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt)，若要查看的消息。

有关如何使用软件跟踪工具的详细信息，请参阅[软件跟踪工具的调查](https://docs.microsoft.com/windows-hardware/drivers/devtest/survey-of-software-tracing-tools)。

### <a name="viewing-the-umdf-trace-log"></a>查看 UMDF 跟踪日志

UMDF 日志文件为 %windir%\\system32\\LogFiles\\WUDF\\WUDFTrace.etl。

**请注意**  UMDF 2.15 从开始，日志目录是 *%programdata%* \\Microsoft\\WDF。

 

可以通过使用查看 UMDF 日志文件[TraceView](https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview)或[Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)。 这两种工具需要格式化跟踪日志消息的跟踪消息格式 (TMF) 文件。 TMF 文件均位于 WDK 下\\工具\\跟踪子目录。 （在 TraceView，UMDF 显示为"UMDF Framework 跟踪"或"Framework 跟踪"，具体取决于 UMDF 版本的名称命名的提供程序。）

[WDF 验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)使您能够将跟踪消息发送到 UMDF 跟踪日志和内核调试程序。 (您不应将跟踪消息通过使用发送到内核调试程序 **-kd**选项[Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)，这是因为**Tracelog**可能会破坏内 UMDF 跟踪日志记录。)

此外可以使用[ **！ wmitrace** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)调试器扩展[查看跟踪消息](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-do-i-send-trace-messages-to-a-kernel-debugger-)在调试器中：

1.  在 WinDbg 中，将附加到 WUDFHost 承载该驱动程序的实例。 有关详细信息，请参阅[如何启用调试 UMDF 驱动程序的](enabling-a-debugger.md)。
2.  如果您的驱动程序使用版本 1.11 或更高版本，并使用内核调试程序从 Windows 8 或更高版本，则可以跳过此步骤。 如果您的驱动程序使用早于 1.11 UMDF 的版本，使用[ **！ wmitrace.tmffile** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wmitrace-tmffile)或[ **！ wmitrace.searchpath** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wmitrace-searchpath)指定特定于平台的跟踪消息格式 (.tmf) 文件或.tmf 文件的路径。 .Tmf 文件位于在 WDK 中的特定于平台的子目录中。

3.  使用[ **！ wmitrace.logdump** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wmitrace-logdump)命令以显示跟踪缓冲区的内容：

    ```cpp
    !wmitrace.logdump WudfTrace
    ```

### <a name="controlling-trace-messages"></a>控制跟踪消息

您可以控制 UMDF 跟踪消息与用户界面[WDF 验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)提供，或通过修改注册表值。 应使用**WDF 验证程序**接口在可能的情况，因为注册表值可能会更改在将来版本的 UMDF。 此外，不应访问 INF 文件或驱动程序的代码中的这些值。

目前，可以修改以下注册表值，位于**HKLM\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF**注册表项：

-   **LogEnable**值该值控制是否 UMDF 创建跟踪日志，了解您的驱动程序。 如果此值设置为 1，UMDF 创建跟踪日志。

-   **LogLevel**值控制 UMDF 跟踪消息包含的信息量。 默认值为**LogLevel**为 3，这将导致 UMDF 跟踪消息，以包含错误和警告消息。 将此值设置为 7 可包括错误和警告消息，以及非错误信息性消息。 将其设置为 15，以包含所有 UMDF 是能够提供的跟踪信息。

-   **LogKd**值该值控制是否 UMDF 将跟踪消息发送到内核调试程序。 如果**LogKd**设置为 1，UMDF 发送它的跟踪消息到内核调试程序。

-   **LogFlushPeriodSeconds**值指定何种频率，以秒为单位，跟踪消息写入跟踪日志。

-   **LogMinidumpType**值包含指定的微型转储文件，如果生成，将包含的信息类型的标志。 有关这些标志的详细信息，请参阅[小型转储\_类型](https://go.microsoft.com/fwlink/p/?linkid=160310)枚举。

你可能会发现其他注册表值下的**HKLM\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF**注册表项。 不应修改这些值。

 

 





