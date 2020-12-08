---
title: 将 WPP 宏添加到跟踪提供程序
description: 将 WPP 宏添加到跟踪提供程序
keywords:
- Windows 软件跟踪预处理器 WDK，宏
- WPP 软件跟踪 WDK，宏
- 宏 WDK WPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f73efcfe2d2c7ed6b81aaea3757dae334fed2a42
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795121"
---
# <a name="adding-wpp-macros-to-a-trace-provider"></a>将 WPP 宏添加到跟踪提供程序


## <span id="ddk_adding_wpp_macros_to_a_driver_tools"></span><span id="DDK_ADDING_WPP_MACROS_TO_A_DRIVER_TOOLS"></span>


若要将默认格式的 WPP 软件跟踪添加到 [跟踪提供程序](trace-provider.md)（如内核模式驱动程序或用户模式应用程序），请将以下 C 预处理器指令和 WPP 宏调用添加到提供程序的源代码：

-   对于包含任何 WPP 宏的每个源文件，都包含以下形式的 **\# include** 指令。 此语句包含由[WPP 预处理器](wpp-preprocessor.md)为每个源文件创建的[跟踪消息头文件](trace-message-header-file.md)：

    ```
    #include <source-file-name.tmh>
    ```

    跟踪消息头文件必须包含在源文件中的任何 WPP 宏调用之前和定义 [wpp \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 宏之后。

-   每个包含其他 WPP 宏的源文件的 [WPP \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 定义指令。

    此定义指定驱动程序的控件 GUID 和驱动程序定义的跟踪标志名称。 必须先将定义添加到源文件，然后将包含文件的跟踪消息头文件的 **\# include** 语句添加到其中。

-   一个 [WPP \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85)) 宏调用驱动程序的源代码。

    对于驱动程序，此宏会激活驱动程序中的软件跟踪。 此宏通常在驱动程序初始化期间调用，例如在 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程中。

    对于用户模式的应用程序，请在源代码中的某个时间点调用此宏，而之前未进行任何跟踪尝试。

    初始化之后，你可以使用 [TraceView](traceview.md) 或 [Tracelog](tracelog.md) 来启动软件跟踪会话并显示跟踪消息。

-   一个 [WPP \_ 清理](/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85)) 宏调用 [跟踪提供程序的](trace-provider.md) 源代码。 此宏停用驱动程序中的软件跟踪。

    对于驱动程序，此宏调用通常添加到驱动程序的 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程。

    对于用户模式应用程序，在执行最后一次跟踪尝试之后，在源代码中的某个点调用此宏。

-   [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)) 宏调用来记录跟踪消息。

 

