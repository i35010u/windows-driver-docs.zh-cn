---
description: 本主题提供有关使用 Logman 工具捕获 USB ETW 事件跟踪的信息。
title: 如何使用 Logman 捕获 USB 事件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b97865d2b31bba9a878af778f4b94cb9d4b5412e
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733557"
---
# <a name="how-to-capture-a-usb-event-trace-with-logman"></a>如何使用 Logman 捕获 USB 事件跟踪


本主题提供有关使用 [Logman](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753820(v=ws.10)) 工具捕获 USB ETW 事件跟踪的信息。 Logman 是内置于 Windows 中的跟踪工具。 可以使用 Logman 将事件捕获到事件跟踪日志文件中。

### <a name="prerequisites"></a>先决条件

事件跟踪日志文件的增长速度非常快，但更小的日志文件更易于导航，更易于传输。 在开始跟踪之前，请考虑采取以下步骤从日志中排除无关事件，以便您可以专注于要检查的设备活动：

-   断开所有非重要 USB 设备的连接。 较少的设备会导致较小的跟踪，使其更易于读取和分析。
-   如果系统有 USB 键盘或鼠标，请改为使用 "远程桌面" 输入跟踪命令。
-   尽可能缩小跟踪范围的开始时间和结束时间。
-   如果仅对某类 USB 事件感兴趣，则可以使用关键字筛选所记录的事件。 有关详细信息，请参阅“备注”。

USB 3.0 驱动程序堆栈中的事件跟踪类似于 Windows 7 中引入的 USB 2.0 驱动程序堆栈跟踪。 可以在 Windows 8 计算机上捕获来自 USB 2.0 驱动程序堆栈的事件跟踪。 从 USB 2.0 和 USB 3.0 驱动程序堆栈捕获事件跟踪的方式类似。 你可以独立捕获 USB 2.0 或 USB 3.0 驱动程序堆栈中的事件。 将 USB 2.0 设备连接到 USB 3.0 主机控制器时，将从 USB 3.0 驱动程序堆栈获取事件跟踪。 在这种情况下，你将查看 USB 2.0 设备的新 USB 3.0 驱动程序堆栈事件。

<a name="instructions"></a>Instructions
------------

**收集 USB 跟踪事件**

1.  打开具有管理权限的命令提示符窗口。 为此，请选择 "开始"，在搜索框中键入 **cmd** ，选择并按住 (或右键单击) cmd.exe，然后选择 " **以管理员身份运行**"。
2.  在命令提示符窗口中，输入以下命令以启动捕获会话：

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

    每个命令完成后，Logman 将显示 `The command completed successfully.`

3.  执行要捕获的操作。 例如，若要捕获设备枚举的事件，可以在 **设备管理器**中插入显示为 "未知设备" 的 USB 闪存驱动器。 使命令提示符窗口保持打开状态。
4.  在完成方案后停止会话。 输入以下命令以结束捕获会话：

    可以通过运行以下命令来停止 USB 集线器和端口事件收集：

    ```cpp
    logman stop -n usbtrace 
    logman delete -n usbtrace
    move /Y %SystemRoot%\Tracing\usbtrace_000001.etl %SystemRoot%\Tracing\usbtrace.etl

    ```

上述捕获会话生成名为 usbtrace 的 etl 文件。 跟踪文件存储在% SystemRoot% \\ 跟踪 \\ Usbtrace (C： \\ Windows \\ 跟踪 \\ usbtrace) 上。 将该文件移动到其他位置或将其重命名，以避免在捕获下一个会话时覆盖它。

此文件包含来自 USB 3.0 和 USB 2.0 驱动程序堆栈的事件跟踪。 如果要将事件跟踪减少到一个 USB 驱动程序堆栈，请从下一个跟踪会话中删除其他驱动程序堆栈。 为此，可以修改步骤2中所示的命令序列，删除与要从跟踪会话中删除的驱动程序堆栈相对应的 "logman 更新" 行。

<a name="remarks"></a>备注
-------

**USB 3.0 驱动程序堆栈事件的捕获筛选器**

请注意 ETW 关键字，如 Logman 捕获命令中的 **Default** 和 **PartialDataBusTrace** 。 这些词是 ETW 关键字，用于指示要查看的事件类型。 您可以使用 ETW 关键字来筛选 USB 驱动程序写入跟踪日志的事件，并自定义要查看的有关从 USB 3.0 驱动程序堆栈捕获的事件的信息。 保存与任何关键字匹配的事件。 请注意，此筛选方法在捕获时使用，而不是在分析期间使用。

您可以根据自己的需求筛选基于关键字的事件。 下面是用于筛选 USB 3.0 驱动程序堆栈事件的关键字：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ETW 关键字</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Default</strong></p></td>
<td><p>显示适用于一般故障排除的事件。 事件类似于 USB 2.0 ETW 事件，但不包括任何 USB 传输事件。</p></td>
</tr>
<tr class="even">
<td><p><strong>StateMachine</strong></p></td>
<td><p>显示驱动程序的内部状态机转换。 <strong>默认</strong>关键字中不包含这些事件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>断开</strong></p></td>
<td><p>显示跟踪开始时的设备信息事件，并捕获 USB 树的开始状态。 要保存设备信息 <strong>断开</strong> 事件，以便跟踪包含连接设备的详细信息，例如 usb 描述符和 Usb 设备描述。 这些事件包含在 <strong>Default</strong> 关键字中。 如果不使用 <strong>Default</strong> 关键字，则应使用 <strong>断开</strong> 关键字。 剩余的断开事件提供有关驱动程序内部状态机的最近状态转换的信息。 这些事件包括在 <strong>StateMachine</strong> 关键字中。</p></td>
</tr>
<tr class="even">
<td><p><strong>电源</strong></p></td>
<td><p>显示 <strong>默认</strong> 事件的子集。 显示设备电源转换事件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IRP</strong></p></td>
<td><p>显示 <strong>默认</strong> 事件的子集。 事件显示来自客户端驱动程序和 Irp 的 Irp，这些事件是由用户模式请求引起的。 不过， (URB) 请求的有效 USB 传输不会与 <strong>IRP</strong> 关键字一起显示，并且需要 <strong>HeadersBusTrace</strong>、 <strong>PartialDataBusTrace</strong>或 <strong>FullDataBusTrace</strong> 才能显示。</p></td>
</tr>
<tr class="even">
<td><p><strong>HeadersBusTrace</strong></p></td>
<td><p>显示所有 USB 传输事件，但不保存数据包。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PartialDataBusTrace</strong></p></td>
<td><p>显示所有 USB 传输事件，并保存有限的总线数据负载。</p></td>
</tr>
<tr class="even">
<td><p><strong>FullDataBusTrace</strong></p></td>
<td><p>显示所有 USB 传输事件，并为大容量、中断和控制传输保存最多 4 KB 的总线数据。 请注意，只记录链式 MDL 的第一个缓冲区。 即使 <a href="/windows-hardware/drivers/ddi/usb/ns-usb-_urb_isoch_transfer" data-raw-source="[&lt;strong&gt;URB_ISOCH_TRANSFER&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_isoch_transfer)"><strong>URB_ISOCH_TRANSFER</strong></a> 请求结构保存) ，也永远不会记录同步总线数据 (。 有关详细信息，请参阅 <a href="how-to-send-chained-mdls.md" data-raw-source="[How to send chained MDLs](how-to-send-chained-mdls.md)">如何发送链式 MDLs</a> 和 <a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">如何将数据传输到 USB 同步终结点</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HWVerifyHost</strong></p></td>
<td><p>显示 <strong>默认</strong> 事件的子集。 这些事件指示 USB 主机控制器硬件中发生错误的时间。</p></td>
</tr>
<tr class="even">
<td><p><strong>HWVerifyHub</strong></p></td>
<td><p>显示 <strong>默认</strong> 事件的子集。 这些事件指示 USB 集线器硬件发生错误的时间。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HWVerifyDevice</strong></p></td>
<td><p>显示 <strong>默认</strong> 事件的子集。 这些事件指示 USB 设备硬件中发生错误的时间。</p></td>
</tr>
</tbody>
</table>



例如，下面是一系列命令，用于启动会话来捕获 USB 设备电源转换。 由于 (USB 3.0 驱动程序堆栈) 选择提供程序，因此仅捕获连接了 USB 3.0 主机控制器下游的设备的事件。

```cpp
logman create trace -n usbtrace -o %SystemRoot%\Tracing\usbtrace.etl -nb 128 640 -bs 128
logman update trace -n usbtrace -p Microsoft-Windows-USB-USBXHCI (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-USB-UCX (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-USB-USBHUB3 (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-Kernel-IoTrace 0 2
logman start -n usbtrace
```

**捕获电源事件筛选器**

Usb 设备的有用 ETW 关键字是 USB 端口驱动程序的 PowerDiagnostics 标志。 使用此关键字时，端口驱动程序会记录主机控制器和终结点信息，但会省略描述传输的所有事件。 如果你不需要看到传输事件，可以使用 PowerDiagnostics 关键字将跟踪日志的大小减小到85%。 启动跟踪时指定 PowerDiagnostics 关键字，如以下示例中所示：

```cpp
Logman start Usbtrace -p Microsoft-Windows-USB-USBPORT PowerDiagnostics -o usbtrace.etl -ets -nb 128 640 -bs 128

Logman update Usbtrace -p Microsoft-Windows-USB-USBHUB –ets
```

如果筛选的跟踪日志包含多个主机控制器异步计划启用和禁用事件，则可以在使用 Netmon 筛选器查看日志时对其进行筛选，如以下示例中所示：

```cpp
NOT (Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Host Controller Async Schedule Enable" 
OR Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Host Controller Async Schedule Disable")
```

有关 Netmon 筛选器的详细信息，请参阅 [案例研究：使用 ETW 和 Netmon 对未知 USB 设备进行故障排除](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)中的 "USB Netmon 筛选器"。

有时，在跟踪日志中建立传输事件（例如集线器请求和导致错误（如事务错误或延迟）的设备请求）会很有帮助。 你可能首先捕获不包含传输事件的日志，并分析较小的日志。 在您大致了解问题方案中的问题后，再次运行跟踪而不进行筛选。

## <a name="related-topics"></a>相关主题
[使用 USB ETW](using-usb-etw.md)  
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  
[定义用于对事件类型进行分类的关键字](/windows/desktop/WES/defining-keywords-used-to-classify-types-of-events)