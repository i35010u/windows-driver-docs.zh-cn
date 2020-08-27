---
description: 本主题提供有关如何查看在 USB ETW 日志中捕获的事件的时间线的信息。
title: 使用 Xperf 和 Netmon 分析 USB 性能问题
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 060ffa378237bf3c1803cb95292914ee0d27abd2
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969474"
---
# <a name="analyzing-usb-performance-issues-by-using-xperf-and-netmon"></a>使用 Xperf 和 Netmon 分析 USB 性能问题


本主题提供有关如何查看在 USB ETW 日志中捕获的事件的时间线的信息。

Xperf 提供了一组用于分析性能问题的内核事件。 它记录这些事件，并将它们显示在图形中。

如果你熟悉 Xperf 和 USB ETW 事件，则可以创建一个 USB ETW 日志和一个 Xperf 日志，其中包含问题方案，合并两个日志文件，并将它们一起进行分析。 结合使用 Xperf 和 Netmon，可以查看给定方案 (Netmon) 的系统事件 (Xperf) 和 USB 事件。

通过从提升的命令提示符发出以下命令，并行启动两个跟踪：

```cpp
Xperf –on Diag

Logman start Usbtrace -p Microsoft-Windows-USB-USBPORT -o usbtrace.etl -ets -nb 128 640 -bs 128

Logman update Usbtrace -p Microsoft-Windows-USB-USBHUB –ets
```

针对问题方案执行操作，然后通过从提升权限的命令提示符发出以下命令来停止跟踪：

```cpp
Logman stop Usbtrace -ets

Xperf –stop
```

使用以下命令将两个跟踪日志文件合并到一个文件中 (不需要权限) ：

```cpp
Xperf –merge usbtrace.etl C:\kernel.etl merged.etl
```

此示例创建一个名为 "已合并" 的合并文件。 可以通过 Xperf 性能分析器或 Netmon 来打开此文件。 若要在 Xperf 中打开该文件，请运行以下命令：

```cpp
Xperf merged.etl
```

Xperf 显示了一系列内核事件的专门图形，如图所示。 有关 Xperf 录制选项和 Xperf GUI 的详细信息，请 [Xperf 命令行工具的详细](https://msdn.microsoft.com/library/cc305221.aspx) 信息和 [Windows 性能分析器 (WPA) ](https://msdn.microsoft.com/library/cc305187.aspx)。

![windows 性能分析器](images/xperf3.png)

若要在 Netmon 中打开合并的跟踪日志，请运行 Netmon，单击 "文件"-" ** &gt; &gt; 捕获**"，然后选择该文件。 Xperf 和 Netmon 可以同时打开合并的文件。 可以在 Xperf GUI 和 Netmon 之间切换，以便分析在特定时间段内系统和 USB 堆栈中发生的情况。 除了系统事件之外，你还可以查看 Xperf 中的 USB 事件，但在 Netmon 中，USB 事件会更易于阅读。

默认情况下，Netmon 显示合并跟踪文件中的所有事件。 若要仅显示 USB 事件，请应用如下所示的筛选器：

```cpp
ProtocolName == "USBHub_MicrosoftWindowsUSBUSBHUB" OR ProtocolName == "USBPort_MicrosoftWindowsUSBUSBPORT"
```

可以在 "Netmon 筛选器" 显示窗格中输入此筛选器文本。 有关在 Netmon 中使用筛选器的详细信息，请参阅本例中的 "USB Netmon 筛选器" [：使用 ETW 和 Netmon 对未知 USB 设备进行故障排除](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)。

若要分析 USB 事件的时间，可以查看 Netmon 中显示的事件之间的时间差。

**查看所显示事件的时间差**

1.  在 " **帧摘要** " 窗格中，右键单击列标题，然后选择 " **选择列**"。
2.  在 " **禁用的列** " 列表中，选择 " **时间增量**"，单击 " **添加**"，然后单击 **"确定"**。
3.  编写一个筛选器，该筛选器仅显示要查看其时间的事件。 例如，若要查看非重叠大容量传输调度和完成事件之间的延迟，请添加以下筛选器：
    ```cpp
    Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Dispatch URB_FUNCTION_BULK_OR_INTERRUPT_TRANSFER" 
    OR Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Complete URB_FUNCTION_BULK_OR_INTERRUPT_TRANSFER" 
    OR Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Complete URB_FUNCTION_BULK_OR_INTERRUPT_TRANSFER with Data"

    ```

    1.  可以从跟踪中显示的事件)  (说明中选择事件 Id。
    2.  若要在筛选器中使用事件 ID，请在 " **帧摘要** " 窗格中右键单击某个事件的说明，然后选择 " **添加说明以显示筛选器**"。

## <a name="related-topics"></a>相关主题
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  
[将 Xperf 与 USB ETW 配合使用](using-xperf-with-usb-etw.md)  



