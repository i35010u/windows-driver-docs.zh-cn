---
Description: 本主题介绍有关使用 Logman 工具捕获 USB ETW 事件跟踪。
title: 如何使用 Logman 捕获 USB 事件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cb23adec030ad43785acdc47776ef3d0eb6e182
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350340"
---
# <a name="how-to-capture-a-usb-event-trace-with-logman"></a>如何使用 Logman 捕获 USB 事件跟踪


本主题提供有关使用信息[Logman](https://go.microsoft.com/fwlink/p/?linkid=617153)工具，用于捕获的 USB ETW 事件跟踪。 Logman 是内置于 Windows 的跟踪工具。 可以使用 Logman 捕获到事件跟踪日志文件的事件。

### <a name="prerequisites"></a>先决条件

事件跟踪日志文件可以增长得非常迅速，但较小的日志文件是更轻松地导航和更轻松地传输。 在开始跟踪之前，请考虑执行以下步骤，从日志中排除无关的事件，以便你可以专注于你想要检查的设备活动：

-   断开连接不感兴趣的设备的任何非关键 USB 设备。 较少的设备会导致较小的跟踪，从而更轻松地读取和分析。
-   您的系统具有 USB 键盘或鼠标，则输入跟踪命令改为使用远程桌面。
-   缩小范围开始和尽可能多地围绕感兴趣的操作的跟踪的结束。
-   如果您有兴趣某些类别的 USB 事件，可以使用关键字来筛选记录的事件。 有关详细信息，请参阅备注。

从 USB 3.0 驱动程序堆栈的事件跟踪是类似于 Windows 7 中引入的 USB 2.0 驱动程序堆栈跟踪。 从 USB 2.0 驱动程序堆栈的事件跟踪可以捕获 Windows 8 计算机上。 捕获事件跟踪从 USB 2.0 和 USB 3.0 驱动程序堆栈的方式是类似的。 您可以独立地捕获 USB 2.0 或 USB 3.0 驱动程序堆栈中的事件。 USB 2.0 设备连接到 USB 3.0 主机控制器时，可以从 USB 3.0 驱动程序堆栈获取事件跟踪。 在这种情况下，将查看 USB 2.0 设备的新 USB 3.0 驱动程序堆栈事件。

<a name="instructions"></a>说明
------------

**若要收集 USB 跟踪事件**

1.  打开具有管理权限的命令提示符窗口。 为此，请单击开始，类型**cmd**在搜索框中，右键单击 cmd.exe，，然后选择**以管理员身份运行**。
2.  在命令提示符窗口中，输入以下命令，启动捕获会话：

    ```cpp
    logman create trace -n usbtrace -o %SystemRoot%\Tracing\usbtrace.etl -nb 128 640 -bs 128
    logman update trace -n usbtrace -p Microsoft-Windows-USB-USBXHCI (Default,PartialDataBusTrace)
    logman update trace -n usbtrace -p Microsoft-Windows-USB-UCX (Default,PartialDataBusTrace)
    logman update trace -n usbtrace -p Microsoft-Windows-USB-USBHUB3 (Default,PartialDataBusTrace)
    logman update trace -n usbtrace -p Microsoft-Windows-USB-USBPORT
    logman update trace -n usbtrace -p Microsoft-Windows-USB-USBHUB
    logman update trace -n usbtrace -p Microsoft-Windows-Kernel-IoTrace 0 2
    logman start -n usbtrace

    ```

    每个命令完成后，显示 Logman `The command completed successfully.`

3.  执行将想要捕获的操作。 例如，若要捕获设备枚举的事件，您可以插入中显示为"未知设备"USB 闪存驱动器**设备管理器**。 在命令提示符窗口保持打开。
4.  停止该方案完成的会话。 输入以下命令以结束捕获会话：

    可以通过运行以下命令来停止 USB 集线器和端口事件收集：

    ```cpp
    logman stop -n usbtrace 
    logman delete -n usbtrace
    move /Y %SystemRoot%\Tracing\usbtrace_000001.etl %SystemRoot%\Tracing\usbtrace.etl

    ```

在前面的捕获会话生成一个名为 usbtrace.etl 的 etl 文件。 跟踪文件存储在 %systemroot%\\跟踪\\usbtrace.etl (c:\\Windows\\跟踪\\usbtrace.etl)。 将文件移动到另一个位置，或将其重命名为了避免捕获下一个会话时覆盖它。

该文件包含从 USB 3.0 和 USB 2.0 驱动程序堆栈的事件跟踪。 如果你想要减少到只是一个 USB 驱动程序堆栈的事件跟踪，请从下一步跟踪会话中删除其他驱动程序堆栈。 可以通过修改删除对应于你想要从跟踪会话中删除驱动程序堆栈的"logman update"行第 2 步中所示的命令序列来执行此操作。

<a name="remarks"></a>备注
-------

**捕获 USB 3.0 驱动程序堆栈事件筛选的器**

请注意 ETW 关键字，如**默认**并**PartialDataBusTrace**在 Logman 捕获命令。 这些词语的 ETW 关键字，指示你想要查看的事件的类型。 ETW 关键字可用于筛选事件的 USB 驱动程序将写入到跟踪日志和自定义您想要查看有关从 USB 3.0 驱动程序堆栈中捕获的事件的信息。 与任何关键字匹配的事件保存。 请注意，此筛选方法用于在捕获时，不是在分析期间使用。

你可以筛选事件基于具体取决于您的要求的关键字。 下面是用于筛选 USB 3.0 驱动程序堆栈事件的关键字：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ETW 关键字</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>默认</strong></p></td>
<td><p>显示可用于常规故障排除的事件。 事件类似于 USB 2.0 ETW 事件，但不是包括任何 USB 传输事件。</p></td>
</tr>
<tr class="even">
<td><p><strong>StateMachine</strong></p></td>
<td><p>显示驱动程序内部状态机转换。 中不包含事件<strong>默认</strong>关键字。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rundown</strong></p></td>
<td><p>显示设备的信息事件的跟踪的开始处，并捕获 USB 树的起始状态。 设备信息<strong>断开</strong>事件非常重要，若要保存的跟踪包含详细信息，例如 USB 描述符和连接的设备的 USB 设备说明。 中包含这些事件<strong>默认</strong>关键字。 当不使用<strong>默认</strong>关键字，则应使用<strong>断开</strong>关键字。 剩余断开事件提供有关最新的驱动程序内部状态机的状态转换的信息。 中包含这些事件<strong>StateMachine</strong>关键字。</p></td>
</tr>
<tr class="even">
<td><p><strong>电源</strong></p></td>
<td><p>显示的子集<strong>默认</strong>事件。 显示设备电源转换事件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IRP</strong></p></td>
<td><p>显示的子集<strong>默认</strong>事件。 事件从客户端显示 Irp，驱动程序而导致用户模式下请求的 Irp。 但是，有效 USB 传输 (URB) 请求不会显示<strong>IRP</strong>关键字，并且需要<strong>HeadersBusTrace</strong>， <strong>PartialDataBusTrace</strong>，或<strong>FullDataBusTrace</strong>要显示。</p></td>
</tr>
<tr class="even">
<td><p><strong>HeadersBusTrace</strong></p></td>
<td><p>显示所有 USB 传输事件，但是不会保存数据的数据包。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PartialDataBusTrace</strong></p></td>
<td><p>显示所有 USB 传输事件，并将保存有限的 bus 数据的有效负载。</p></td>
</tr>
<tr class="even">
<td><p><strong>FullDataBusTrace</strong></p></td>
<td><p>显示所有 USB 传输事件，并将保存最多 4 KB 的总线的数据大容量，中断，以及控制传输。 请注意，记录仅链接 MDL 的第一个缓冲区。 永远不会记录同步总线数据 (尽管<a href="https://msdn.microsoft.com/library/windows/hardware/ff540414" data-raw-source="[&lt;strong&gt;URB_ISOCH_TRANSFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540414)"> <strong>URB_ISOCH_TRANSFER</strong> </a>保存请求结构)。 有关详细信息，请参阅<a href="how-to-send-chained-mdls.md" data-raw-source="[How to send chained MDLs](how-to-send-chained-mdls.md)">如何发送链接 MDLs</a>并<a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">如何将数据传输到 USB 等时终结点</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HWVerifyHost</strong></p></td>
<td><p>显示的子集<strong>默认</strong>事件。 事件指示在 USB 主机控制器硬件中发生错误时。</p></td>
</tr>
<tr class="even">
<td><p><strong>HWVerifyHub</strong></p></td>
<td><p>显示的子集<strong>默认</strong>事件。 事件指示 USB 集线器硬件中发生错误时。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HWVerifyDevice</strong></p></td>
<td><p>显示的子集<strong>默认</strong>事件。 事件指示在 USB 设备硬件中发生错误时。</p></td>
</tr>
</tbody>
</table>



例如，下面是一系列命令，启动会话，以便捕获 USB 设备电源转换。 由于提供程序 （USB 3.0 驱动程序堆栈） 的所选内容，而捕获事件仅适用于连接的设备的 USB 3.0 主机控制器下一级。

```cpp
logman create trace -n usbtrace -o %SystemRoot%\Tracing\usbtrace.etl -nb 128 640 -bs 128
logman update trace -n usbtrace -p Microsoft-Windows-USB-USBXHCI (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-USB-UCX (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-USB-USBHUB3 (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-Kernel-IoTrace 0 2
logman start -n usbtrace
```

**捕获电源事件的筛选器**

USB 设备的有用 ETW 关键字是 USB 端口驱动程序的 PowerDiagnostics 标志。 当使用此关键字时，端口驱动程序记录主控制器和终结点的信息，但忽略描述传输的所有事件。 如果不需要看到传输事件，您可以使用 PowerDiagnostics 关键字减少高达 85%的跟踪日志的大小。 指定 PowerDiagnostics 关键字时启动跟踪，如下面的示例中所示：

```cpp
Logman start Usbtrace -p Microsoft-Windows-USB-USBPORT PowerDiagnostics -o usbtrace.etl -ets -nb 128 640 -bs 128

Logman update Usbtrace -p Microsoft-Windows-USB-USBHUB –ets
```

如果你已筛选的跟踪日志中的许多异步的主控制器计划启用和禁用事件，如下面的示例中所示可以筛选它们出筛选时，通过使用网络监视器查看日志：

```cpp
NOT (Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Host Controller Async Schedule Enable" 
OR Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Host Controller Async Schedule Disable")
```

网络监视器筛选器的详细信息，请参阅"USB Netmon 筛选器"中[案例研究：使用 ETW 和 Netmon 未知的 USB 设备进行故障排除](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)。

有时是有助于在跟踪日志，如中心请求和事务错误或停滞之类的错误会导致设备请求中的传输事件。 首先，你可能会捕获日志，而无需传输事件和分析该较小的日志。 然后跟踪再次运行而不筛选后你问题的方案中有一般了解的问题。

## <a name="related-topics"></a>相关主题
[使用 USB ETW](using-usb-etw.md)  
[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  
[定义用于事件的类型进行分类的关键字](https://msdn.microsoft.com/library/windows/desktop/dd996915)  



