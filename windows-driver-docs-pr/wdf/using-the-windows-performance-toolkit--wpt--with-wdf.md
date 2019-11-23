---
title: 将 Windows 性能工具包 (WPT) 与 WDF 配合使用
description: 从 Windows 10 开始，你可以使用 Windows 性能工具包（WPT）来查看 KMDF 或 UMDF 2 驱动程序的性能数据。
Search.SourceType: Video
ms.assetid: 0442E4E2-DBC7-4EB0-BEB6-49EFF5132A1D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dffee9de59ff54b39940ba7e62d4ec54fa96854c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845428"
---
# <a name="using-the-windows-performance-toolkit-wpt-with-wdf"></a>将 Windows 性能工具包 (WPT) 与 WDF 配合使用


从 Windows 10 开始，你可以使用 Windows 性能工具包（WPT）来查看给定内核模式驱动程序框架（KMDF）或用户模式驱动程序框架（UMDF）2驱动程序的性能数据。

## <a name="how-can-the-windows-driver-frameworks-wdf-extensions-for-wpt-help"></a>适用于 WPT 的 Windows 驱动程序框架（WDF）扩展如何提供帮助？


你可以使用 WPT 来获取性能见解或排查性能问题。 例如：

-   检查驱动程序的 WDF i/o 请求的完成率、CPU 使用率以及在 PnP 和电源回拨中花费的时间。
-   将 UMDF 2 驱动程序与类似的 KMDF 驱动程序进行比较，并确定 UMDF 是否满足性能要求。
-   确定 WDF i/o 路径中的性能故障。
-   确定给定回调的哪个实例花费了较长时间。 然后检查抽样 CPU 使用率以了解原因。
-   检查设备是否正在进行电源转换，并使其脱离 D0 电源状态。

## <a name="getting-started"></a>入门


WPT 是 Windows 评估和部署工具包（ADK）的一部分。 你可以从[Windows 硬件工具](https://developer.microsoft.com/windows/featured/hardware/windows-10-hardware-preview-tools)站点安装 ADK。

WPT 包含两个单独的工具： Windows 性能记录器和 Windows 性能分析器（WPA）。 在本主题中，我们将使用 "来录制跟踪，然后使用 WPA 来以可配置的 GUI 格式查看跟踪。

若要了解如何使用 Windows 性能工具包来度量 WDF 驱动程序的性能，请观看以下视频或阅读视频下面的步骤。 视频和步骤涵盖了相同的过程。
>[!VIDEO https://www.microsoft.com/videoplayer/embed/fc37f465-9456-45d7-bbe9-6f7d44342563]

**记录和查看 WDF 驱动程序的事件日志**

1.  安装驱动程序（如果尚未安装）。

2.  在提升的命令提示符下，输入以下命令。

    **WdfPerfEnhancedVerifier** *&lt;SERVICENAME&gt;&lt;UMDF 或 KMDF&gt;*

    **注意** 应从安装 WPT 的位置复制 WdfPerfEnhancedVerifier。 如果在开发计算机上安装了 WPT，则需要将脚本从 WPT 安装目录复制到目标计算机。




此脚本为指定的驱动程序设置注册表项，以便在步骤4中启用 ETW 提供程序时，框架记录启用性能分析所需的事件。


3.  重新启动计算机。
4.  在提升的命令提示符下，输入以下命令。

    **"** **-Start WdfTraceLoggingProvider**

    此命令为 WDF 启用 ETW 提供程序。 计算机开始记录跟踪。

    **请注意**  如步骤2所示，应从安装 WPT 的位置复制 "。 如果在开发计算机上安装了 WPT，请将这些文件从 WPT 安装目录复制到目标计算机。

    在适用于桌面版的 Windows 10 （家庭版、专业版、企业版和教育版）上，您还可以使用 Wprui 启动跟踪，后者提供了用于记录跟踪的 GUI。 在 "更多选项" 下，展开 "**资源分析**"，然后选择**WDF 驱动程序活动**。

5.  练习您感兴趣的方案。
6.  停止 ETW 跟踪会话： **"-Stop MyPerfTrace**
7.  在 Windows 性能分析器查看器中打开事件跟踪日志：

    **Wpa-psk MyPerfTrace**

若要捕获同一驱动程序的另一个跟踪，请使用 "启动和停止新的跟踪。 若要捕获其他驱动程序的跟踪，请首先重新运行新驱动程序的 WdfPerfEnhancedVerifier。

## <a name="analyzing-the-trace"></a>分析跟踪


若要开始分析驱动程序的性能，请在左侧找到**图形资源管理器**，打开 "**计算**" 类别，然后将 "UMDF" 或 "KMDF" 图形拖到 "**分析**" 选项卡下的主工作区。此屏幕截图显示了 "**图形资源管理器**" 窗格：

![wpa 中的图形资源管理器](images/WpaUMDFIoCapture-LeftPane.png)

有一个专用表用于 UMDF，另一个用于 KMDF 驱动程序。

## <a name="umdf-io-request-graph-and-summary-table"></a>UMDF i/o 请求图和摘要表


WPT 可以通过两种方式显示 WDF i/o 请求的完成吞吐量：

-   每秒完成的 i/o 请求数
-   每个 i/o 请求的持续时间（格式为甘特图）

以下屏幕截图显示了用于 CPU 和 UMDF i/o 请求性能的示例摘要图表和表。 在 UMDF i/o 请求完成速率图中，每秒的请求数将显示在 y 轴上。

![用于 umdf i/o 请求性能的关系图](images/WpaUMDFIoCapture-Narrow.PNG)

在[摘要表](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh448109(v=win.10))中，大多数列都一目了然，但要注意一些事项。 WdfDevice 列包含与 i/o 请求关联的 WDFDEVICE 句柄。 ActivityID 包含 i/o 请求的唯一标识符。 框架在向驱动程序提供 i/o 请求时创建此标识符。 如果活动标识符已经与相应的 IRP 关联，则框架将使用该标识符。 有关详细信息，请参阅[使用活动标识符](using-activity-identifiers.md)。

输入时间是框架将请求传递给驱动程序时的跟踪时间戳，退出时间是驱动程序调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)或相关方法来完成请求时的时间戳。

## <a name="kmdf-io-request-graph-and-summary-table"></a>KMDF i/o 请求图和摘要表


下面是一个类似屏幕截图，显示了 KMDF 驱动程序的 i/o 请求信息。

![用于 umdf i/o 请求性能的关系图](images/WpaKMDFIoCapture-Narrow.PNG)

## <a name="pnp-power-callback-graph-and-summary-table"></a>PnP Power 回呼 graph 和摘要表


WPT 还可以显示每个 PnP 和电源回拨的处理时间。 以下屏幕截图显示了一个示例 KMDF 驱动程序的[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)、 [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)和[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调持续时间以及一个示例 UMDF 驱动程序。

WdfDevice 列包含与回调关联的 WDFDEVICE 句柄。 ActivityID 包含回调实例的唯一标识符。

![pnp power 回调图形](images/wpa-fx2-pnppwr.PNG)

## <a name="which-calls-are-instrumented"></a>检测哪些调用？


本部分介绍了哪些事件用于生成上面所示的图形和表。

针对特定驱动程序运行 WdfPerfEnhancedVerifier 后，当系统调用某些指定驱动程序的回调时，框架会在 ETL 跟踪日志中记录事件，同时还会在指定的驱动程序调用某些框架方法时记录事件。

若要确定何时开始 i/o 请求，框架会在调用以下回调时记录事件：

-   [*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)
-   [*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)
-   [*EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)
-   [*EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)
-   [*EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)

当驱动程序调用以下方法时，该框架还会记录 i/o 请求开始事件：

-   [**WdfIoQueueRetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)
-   [**WdfIoQueueRetrieveRequestByFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject)
-   [**WdfIoQueueRetrieveFoundRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)

若要确定 i/o 请求何时完成，框架需要跟踪驱动程序调用的时间：

-   [**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
-   [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
-   [**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)

最后，若要确定 PnP/Power 回调的回调持续时间，框架将在调用以下驱动程序提供的回调例程时进行记录，并在它们完成时进行记录：

-   [*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)
-   [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)
-   [*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)
-   [*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)
-   [*EvtIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)

## <a name="resources-and-troubleshooting"></a>资源和疑难解答


-   请确保在运行 WdfPerfEnhancedVerifier 脚本之后重新启动。
-   若要确定是否已将驱动程序配置为记录事件日志，请使用 **！WdfKd. wdfdriverinfo**内核调试器命令。 如果为性能跟踪配置了驱动程序，将看到如下输出：

    ```cpp
    !WdfKd.WdfDriverInfo Echo.sys
    …
    …
    ----------------------------------

    WDF Verifier settings for echo.sys is ON
      Enhanced verifier: performance analysis hooking ON
    ----------------------------------
    ```

-   对于开发和测试目的，可以暂时禁用强制实施驱动程序代码签名策略。 有关详细信息，请参阅[在开发和测试过程中安装未签名的驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/installing-an-unsigned-driver-during-development-and-test)。
-   如果已在 Windows 10 移动设备上捕获跟踪，则需要将 MyPerfTrace 从目标设备复制到具有 Wpa-psk 的计算机。 可以使用[TShell 工具](https://sysdev.microsoft.com/Hardware/oem/docs/Phone_Testing/TShell)执行此操作。

## <a name="related-topics"></a>相关主题


[Windows Performance Analyzer](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh448170(v=win.10))










