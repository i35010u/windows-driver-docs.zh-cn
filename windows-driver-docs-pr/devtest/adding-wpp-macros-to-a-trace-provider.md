---
title: 将 WPP 宏添加到跟踪提供程序
description: 将 WPP 宏添加到跟踪提供程序
ms.assetid: fc6db47c-ef18-4454-a385-adee1858b9d4
keywords:
- Windows 软件跟踪预处理器 WDK，宏
- WPP 软件跟踪 WDK，宏
- 宏 WDK WPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a2fb3f21653112eee0199fbb05a07f8a102b6cb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840309"
---
# <a name="adding-wpp-macros-to-a-trace-provider"></a>将 WPP 宏添加到跟踪提供程序


## <span id="ddk_adding_wpp_macros_to_a_driver_tools"></span><span id="DDK_ADDING_WPP_MACROS_TO_A_DRIVER_TOOLS"></span>


若要将默认格式的 WPP 软件跟踪添加到[跟踪提供程序](trace-provider.md)（如内核模式驱动程序或用户模式应用程序），请将以下 C 预处理器指令和 WPP 宏调用添加到提供程序的源代码：

-   为包含任何 WPP 宏的每个源文件提供以下形式的 **\#包含**指令。 此语句包含由[WPP 预处理器](wpp-preprocessor.md)为每个源文件创建的[跟踪消息头文件](trace-message-header-file.md)：

    ```
    #include <source-file-name.tmh>
    ```

    跟踪消息头文件必须包含在源文件中的任何 WPP 宏调用之前，并在定义[wpp\_控件\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏之后。

-   [WPP\_控制](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))包含其他 WPP 宏的每个源文件\_guid 定义指令。

    此定义指定驱动程序的控件 GUID 和驱动程序定义的跟踪标志名称。 必须先将定义添加到源文件，然后才能 **\#include**语句包含文件的跟踪消息头文件。

-   一个[WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))对驱动程序源代码的跟踪宏调用。

    对于驱动程序，此宏会激活驱动程序中的软件跟踪。 此宏通常在驱动程序初始化期间调用，例如在[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程中。

    对于用户模式的应用程序，请在源代码中的某个时间点调用此宏，而之前未进行任何跟踪尝试。

    初始化之后，你可以使用[TraceView](traceview.md)或[Tracelog](tracelog.md)来启动软件跟踪会话并显示跟踪消息。

-   一个[WPP\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))对[跟踪提供程序的](trace-provider.md)源代码的宏调用。 此宏停用驱动程序中的软件跟踪。

    对于驱动程序，此宏调用通常添加到驱动程序的[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程。

    对于用户模式应用程序，在执行最后一次跟踪尝试之后，在源代码中的某个点调用此宏。

-   [**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏调用来记录跟踪消息。

 

 





