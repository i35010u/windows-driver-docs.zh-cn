---
title: 将 Windows 性能工具包 (WPT) 与 WDF 配合使用
description: 从 Windows 10 开始，你可以使用 Windows 性能工具包 (WPT) 若要查看 KMDF 或 UMDF 2 驱动程序的性能数据。
Search.SourceType: Video
ms.assetid: 0442E4E2-DBC7-4EB0-BEB6-49EFF5132A1D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e4cbfe2e61cbc474055f06e9e73f7a417a18b69
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391872"
---
# <a name="using-the-windows-performance-toolkit-wpt-with-wdf"></a>将 Windows 性能工具包 (WPT) 与 WDF 配合使用


从 Windows 10 开始，你可以使用 Windows 性能工具包 (WPT) 若要查看给定内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 2 驱动程序的性能数据。

## <a name="how-can-the-windows-driver-frameworks-wdf-extensions-for-wpt-help"></a>WPT 的 Windows 驱动程序框架 (WDF) 扩展有何帮助？


WPT 可用于获取性能见解，或排查性能问题。 例如：

-   检查驱动程序的 WDF I/O 请求完成速率、 CPU 使用率和 PnP 和电源回调中所用的时间。
-   比较针对类似 KMDF 驱动程序的 UMDF 2 驱动程序，并确定 UMDF 是否满足性能要求。
-   标识 WDF I/O 路径中的性能问题。
-   确定给定的回调的实例需要很长时间。 然后查看采样的 CPU 使用情况以了解其中的原因。
-   检查是否太过频繁设备发出 power 转换入和移出 D0 电源状态。

## <a name="getting-started"></a>即刻体验


WPT 是 Windows 评估和部署工具包 (ADK) 的一部分。 你可以安装从 ADK [Windows 硬件工具](http://dev.windows.com/featured/hardware/windows-10-hardware-preview-tools)站点。

WPT 包含两个单独的工具：Windows 性能记录器和 Windows 性能分析器 (WPA)。 在本主题中，我们使用 WPR 来记录跟踪，然后 WPA 以可配置的 GUI 格式查看跟踪。

若要了解如何使用 Windows 性能工具包来测量 WDF 驱动程序的性能，请观看以下视频或阅读视频下面的步骤。 视频和步骤涵盖的相同过程。
>[!VIDEO https://www.microsoft.com/videoplayer/embed/fc37f465-9456-45d7-bbe9-6f7d44342563]

**记录和查看 WDF 驱动程序的事件日志**

1.  如果尚未安装，请安装您的驱动程序。

2.  在提升的命令提示符，输入以下命令。

    **WdfPerfEnhancedVerifier.cmd**  *&lt;ServiceName&gt;&lt;UMDF 或 KMDF&gt;*

    **请注意**WdfPerfEnhancedVerifier.cmd 应将复制从位置中安装 WPT。 如果开发计算机上安装 WPT，您需要将该脚本从 WPT 安装目录复制到目标计算机。




此脚本设置为指定的驱动程序注册表项，以便在 framework 记录时的 ETW 提供程序启用在步骤 4 中启用性能分析所需的事件。


3.  重新启动计算机。
4.  在提升的命令提示符，输入以下命令。

    **Wpr.exe** **-Start WdfPerfTraceProviders.wprp**

    此命令启用 WDF 的 ETW 提供程序。 记录跟踪启动计算机。

    **请注意**为在步骤 2 中，Wpr.exe WdfPerfTraceProviders.wprp 应从复制和位置安装 WPT。 如果开发计算机上安装 WPT，将这些文件从 WPT 安装目录复制到目标计算机。




在桌面版本中 （主页、 专业版、 企业版和教育版） 的 Windows 10，也可以使用 Wprui.exe，提供用于记录跟踪的 GUI 中启动跟踪。


5.  执行感兴趣的方案。
6.  停止 ETW 跟踪会话：**Wpr.exe -Stop MyPerfTrace.etl**
7.  在 Windows 性能分析器查看器中打开事件跟踪日志：

    **Wpa.exe MyPerfTrace.etl**

若要捕获的相同的驱动程序的另一个跟踪，请使用 Wpr.exe 启动和停止新的跟踪。 若要捕获的跟踪不同驱动程序，第一次重新运行 WdfPerfEnhancedVerifier.cmd 新驱动程序。

## <a name="analyzing-the-trace"></a>分析跟踪


若要启动分析驱动程序的性能，查找**图形资源管理器**在左侧，打开**计算**类别中，，再拖动 UMDF 或 KMDF 图形到主工作区中，在**分析**选项卡。此屏幕截图显示**图形资源管理器**窗格：

![在 wpa 中的图形资源管理器](images/WpaUMDFIoCapture-LeftPane.png)

没有针对 UMDF 和 KMDF 驱动程序的专用的表。

## <a name="umdf-io-request-graph-and-summary-table"></a>UMDF I/O 请求图形和摘要表


WPT 可以通过两种方式显示 WDF I/O 请求完成的吞吐量：

-   每秒完成的 I/O 请求数
-   （格式为甘特图） 每个 I/O 请求的时间的持续时间

以下屏幕截图显示了用于 CPU 和 UMDF I/O 请求性能示例摘要图形和表。 在 UMDF I/O 请求完成速率图中，y 轴上显示的每秒请求数。

![umdf i/o 请求性能的关系图](images/WpaUMDFIoCapture-Narrow.PNG)

在中[摘要表](https://msdn.microsoft.com/library/windows/hardware/hh448109.aspx)，大多数列都很容易理解，但有几个需要注意的事项。 WdfDevice 列包含与 I/O 请求相关联的 WDFDEVICE 句柄。 ActivityID 包含 I/O 请求的唯一标识符。 当它向驱动程序提供的 I/O 请求时，框架将创建此标识符。 如果已经与相应的 IRP 相关联的活动标识符，框架将使用该标识符。 有关详细信息，请参阅[使用活动标识符](using-activity-identifiers.md)。

框架将请求传递到该驱动程序，并退出时是时间戳，该驱动程序调用时，条目时间是跟踪时间戳[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)或相关的方法以完成请求。

## <a name="kmdf-io-request-graph-and-summary-table"></a>KMDF I/O 请求图形和摘要表


下面是类似的屏幕截图显示 KMDF 驱动程序的 I/O 请求信息。

![umdf i/o 请求性能的关系图](images/WpaKMDFIoCapture-Narrow.PNG)

## <a name="pnp-power-callback-graph-and-summary-table"></a>即插即用 Power 回调图形和摘要表


WPT 还可以显示每个 PnP 和电源回调的处理时间。 以下屏幕截图显示[ *EvtDeviceD0Entry*](https://msdn.microsoft.com/library/windows/hardware/ff540848)， [ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)并[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调示例 KMDF 驱动程序和示例 UMDF 驱动程序的持续时间。

WdfDevice 列包含与回调相关联的 WDFDEVICE 句柄。 ActivityID 包含回调实例的唯一标识符。

![即插即用 power 回调关系图](images/wpa-fx2-pnppwr.PNG)

## <a name="which-calls-are-instrumented"></a>它调用进行性能分析？


本部分介绍哪些事件可用来生成关系图和上面所示的表。

框架 WdfPerfEnhancedVerifier.cmd 运行特定的驱动程序后，当系统调用某些指定的驱动程序的回调，在 ETL 跟踪日志中记录了事件，同时时指定的驱动程序调用一些框架方法。

若要确定何时 I/O 请求开始，framework 记录事件时调用以下回调：

-   [*EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)
-   [*EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)
-   [*EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813)
-   [*EvtIoDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541758)
-   [*EvtIoInternalDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541768)

该框架还会记录 I/O 请求开始事件时，驱动程序调用以下方法：

-   [**WdfIoQueueRetrieveNextRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548462)
-   [**WdfIoQueueRetrieveRequestByFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548470)
-   [**WdfIoQueueRetrieveFoundRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548456)

若要确定 I/O 请求完成时，框架会跟踪该驱动程序调用时：

-   [**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
-   [**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
-   [**WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)

最后，若要确定回调持续时间的 PnP/电源回调，该框架记录时它将调用以下驱动程序提供的回调例程，并在完成时：

-   [*EvtDeviceD0Entry*](https://msdn.microsoft.com/library/windows/hardware/ff540848)
-   [*EvtDeviceD0Exit*](https://msdn.microsoft.com/library/windows/hardware/ff540855)
-   [*EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)
-   [*EvtDeviceReleaseHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540890)
-   [*EvtIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541788)

## <a name="resources-and-troubleshooting"></a>资源和故障排除


-   请务必重新启动后运行 WdfPerfEnhancedVerifier.cmd 脚本。
-   若要确定您的驱动程序是否配置为记录事件日志，请使用 **！WdfKd.wdfdriverinfo**内核调试器命令。 如果驱动程序配置为性能跟踪，您将看到如下输出：

    ```cpp
    !WdfKd.WdfDriverInfo Echo.sys
    …
    …
    ----------------------------------

    WDF Verifier settings for echo.sys is ON
      Enhanced verifier: performance analysis hooking ON
    ----------------------------------
    ```

-   对于开发和仅用于测试用途，可以暂时禁用强制驱动程序代码签名策略。 有关详细信息，请参阅[开发和测试期间安装未签名的驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff547565)。
-   如果捕获跟踪在 Windows 10 移动版上的，你将需要将 MyPerfTrace.etl 从目标设备复制到具有 Wpa.exe 的计算机。 可以使用[TShell 工具](https://sysdev.microsoft.com/Hardware/oem/docs/Phone_Testing/TShell)若要执行此操作。

## <a name="related-topics"></a>相关主题


[Windows Performance Analyzer](https://msdn.microsoft.com/library/windows/hardware/hh448170.aspx)










