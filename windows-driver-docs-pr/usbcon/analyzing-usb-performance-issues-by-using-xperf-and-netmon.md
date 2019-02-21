---
Description: This topic provides information about how to view the timeline of events captured in a USB ETW log.
title: 使用 Xperf 和 Netmon 分析 USB 性能问题
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12f14a2fc092b8055d6062247aad1e4f3836cd88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540641"
---
# <a name="analyzing-usb-performance-issues-by-using-xperf-and-netmon"></a>使用 Xperf 和 Netmon 分析 USB 性能问题


本主题提供有关如何查看 USB ETW 日志中捕获的事件的时间线的信息。

Xperf 提供一组内核事件用于分析性能问题。 它记录这些事件，并在关系图中显示它们。

如果你熟悉使用 Xperf 和 USB ETW 事件，可以创建 USB ETW 日志和问题的情景的 Xperf 日志、 合并两个日志文件，并放在一起分析。 使用 Xperf 和 Netmon 一起，可查看系统事件 (Xperf) 和针对给定方案的 USB 事件 (Netmon)。

通过发出以下命令从提升的命令提示符中并行启动两个跟踪：

```cpp
Xperf –on Diag

Logman start Usbtrace -p Microsoft-Windows-USB-USBPORT -o usbtrace.etl -ets -nb 128 640 -bs 128

Logman update Usbtrace -p Microsoft-Windows-USB-USBHUB –ets
```

该问题的情景，执行的操作，并发出以下命令从提升的命令提示符，然后停止跟踪：

```cpp
Logman stop Usbtrace -ets

Xperf –stop
```

通过使用以下命令 （权限不是必需的） 合并到单个文件中的两个跟踪日志文件：

```cpp
Xperf –merge usbtrace.etl C:\kernel.etl merged.etl
```

此示例创建名为 merged.etl 合并的文件。 使用 Xperf 性能分析器或使用 Netmon，您可以打开此文件。 若要在 Xperf 中打开该文件，运行以下命令：

```cpp
Xperf merged.etl
```

Xperf 专门针对显示图表范围广泛的内核事件，此图中所示。 有关详细信息 Xperf 录制选项和 Xperf GUI [Xperf 命令行工具详细](https://msdn.microsoft.com/library/cc305221.aspx)并[Windows Performance Analyzer (WPA)](https://msdn.microsoft.com/library/cc305187.aspx)。

![windows 性能分析器](images/xperf3.png)

若要打开合并的跟踪日志中 Netmon，运行 Netmon，单击**文件-&gt;打开-&gt;捕获**，然后选择该文件。 Xperf 和 Netmon 可以同时打开合并的文件。 您可以切换 Xperf GUI 和 Netmon 分析发生的情况在系统中，USB 堆栈中一段特定时间。 您可以查看 USB 事件在 Xperf，除了系统事件，但 USB 事件可以更轻松地在 Netmon 中读取。

默认情况下，网络监视器显示到合并的跟踪文件中的所有事件。 若要显示仅 USB 事件，应用筛选器如下所示：

```cpp
ProtocolName == "USBHub_MicrosoftWindowsUSBUSBHUB" OR ProtocolName == "USBPort_MicrosoftWindowsUSBUSBPORT"
```

可以在网络监视器筛选器显示窗格中输入此筛选器文本。 使用 Netmon 中筛选器的详细信息，请参阅"USB Netmon 筛选器"在此[案例研究：使用 ETW 和 Netmon 未知的 USB 设备进行故障排除](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)。

若要分析的 USB 事件计时，可以查看网络监视器中显示的事件之间的时差。

**若要查看显示的事件的时间差异**

1.  在中**帧摘要**窗格中，右键单击列标题，然后选择**选择列**。
2.  在中**禁用列**列表中，选择**时间增量**，单击**添加**，然后单击**确定**。
3.  编写显示仅想要查看其计时事件的筛选器。 例如，若要查看非重叠大容量传输调度和完成事件数之间的延迟问题，请添加以下筛选器：
    ```cpp
    Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Dispatch URB_FUNCTION_BULK_OR_INTERRUPT_TRANSFER" 
    OR Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Complete URB_FUNCTION_BULK_OR_INTERRUPT_TRANSFER" 
    OR Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Complete URB_FUNCTION_BULK_OR_INTERRUPT_TRANSFER with Data"

    ```

    1.  可以在跟踪中显示的事件从选择的事件 Id （说明）。
    2.  若要使用的事件 ID 筛选器中，右键单击某一事件的说明**帧摘要**窗格，然后选择**添加到显示筛选器的说明**。

## <a name="related-topics"></a>相关主题
[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  
[使用 USB ETW 使用 Xperf](using-xperf-with-usb-etw.md)  



