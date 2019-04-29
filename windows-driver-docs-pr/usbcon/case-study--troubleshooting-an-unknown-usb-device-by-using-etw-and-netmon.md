---
Description: 举例说明如何使用 USB ETW 和 Netmon Windows 不能识别 USB 设备进行故障排除。
title: 案例研究-未知的 USB 设备进行故障排除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a9909ed6a0ab9fbc506ad3bca3bf5a3fcfaa0e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392132"
---
# <a name="case-study-troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon"></a>案例研究：使用 ETW 和 Netmon 排查未知 USB 设备的问题


本主题举例说明如何使用 USB ETW 和 Netmon Windows 不能识别 USB 设备进行故障排除。

对于此示例中，我们插入设备，它显示为设备管理器和用户界面 (UI) 的其他部分中的未知设备。 硬件 ID 是 USB\\未知。 若要进一步诊断，我们拔出设备、 开始 ETW 跟踪，并再次插入设备。 设备显示为未知设备后，我们将停止跟踪。

-   [有关未知的设备问题](#about-the-unknown-device-problem)
-   [启动事件跟踪分析](#starting-the-event-trace-analysis)
-   [USB 设备篕璶 ㄆ ン](#usb-device-summary-events)
-   [事件说明和数据有效负载](#event-description-and-data-payload)
-   [USB Netmon 筛选器](#usb-netmon-filters)
-   [了解错误事件和状态代码](#status-codes)
-   [向后从问题事件读取](#reading-backwards-from-problem-events)
-   [相关的主题](#related-topics)

## <a name="about-the-unknown-device-problem"></a>有关未知的设备问题


若要调试未知的 USB 设备问题，最好先了解 USB 驱动程序堆栈的作用要枚举设备时用户将其插入到系统。 有关 USB 枚举的信息，请参阅博客文章[USB 堆栈如何枚举设备？](https://go.microsoft.com/fwlink/p/?linkid=617517)

通常当 USB 驱动程序堆栈无法枚举设备时，中心驱动程序仍将报告到 Windows 设备的到达和 USB 设备标记为未知设备在设备管理器。 设备具有设备 ID 的 USB\\VID\_0000 & PID\_0000 和一个硬件 ID 和兼容 ID 的 USB\\未知。 以下事件会导致枚举作为未知设备的 USB 设备的 USB 集线器驱动程序：

-   一个端口重置请求超时枚举过程。
-   USB 设备的设置地址请求失败。
-   USB 设备的设备描述符的请求失败。
-   [USB 设备描述符](usb-device-descriptors.md)的格式不正确和未通过验证。
-   配置描述符的请求失败。
-   [USB 配置描述符](usb-configuration-descriptors.md)的格式不正确和未通过验证。

在 Windows 7 中，枚举的未知的设备标记有故障[代码 43](https://go.microsoft.com/fwlink/p/?linkid=617523)设备管理器中。

如果设备被标记为失败[代码 28](https://go.microsoft.com/fwlink/p/?linkid=617525)在设备管理器中，设备枚举成功，但仍是未知的设备。 此失败代码指示设备未在枚举过程中提供的产品 ID 字符串和 Windows 找不到设备匹配 INF 安装驱动程序。

## <a name="starting-the-event-trace-analysis"></a>启动事件跟踪分析


由于这是设备故障，我们建议使用 Netmon USB 分析器来分析日志文件。

**若要查看事件跟踪日志**

1.  运行网络监视器，请单击**文件-&gt;打开-&gt;捕获**，然后选择该文件。
2.  选择中的第一个事件**帧摘要**窗格中，具有说明 SystemTrace。 此图显示了屏幕如下所示时选择的第一个事件。

    ![microsoft 网络监视器](images/devicefailure-etl.png)

3.  若要自定义网络监视器显示的列，请右键单击列名称并选择**选择列**。
4.  标识为类型的第一个事件**SystemTrace**，包含有关日志的常规信息。 可以扩展中的信息树**帧详细信息**窗格以查看信息，例如丢失的事件数和跟踪开始时间。

## <a name="usb-device-summary-events"></a>USB 设备篕璶 ㄆ ン


事件 2 是在日志中的第一个 USB 事件。 这和多个后续事件描述 USB 主控制器、 中心和我们启动跟踪时连接到系统的设备。 设备摘要事件或只是摘要事件，我们可以调用此组的事件。 第一个与事件类似，摘要事件不会介绍驱动程序活动。 摘要事件记录在日志记录会话开始时的设备的状态。 其他事件表示某种事件总线，与客户端驱动程序的交互或系统，或内部状态发生更改。

USB 集线器和 USB 端口驱动程序都记录摘要事件。 在协议名称列中标识记录了一个事件驱动程序。 例如，事件是记录的 USB 端口驱动程序具有 USBPort\_MicrosoftWindowsUSBPORT 协议名称。 USB 事件跟踪通常包含一系列端口摘要事件后, 跟一系列中心摘要事件。 有许多的 USB 端口和 USB 集线器摘要事件在其描述中的单词"信息"或"属性"。

可以识别摘要事件的结束的方式？ 如果 USB 集线器事件开头之间的时间戳模式中的重大突破，广告可能是日志的设备摘要的末尾。 否则，任何 USB 集线器事件后的第一个 USB 端口事件可能是第一个非摘要事件。 在以下页面的图 3 显示了此示例跟踪中的第一个非摘要事件。

在此示例中，感兴趣的设备未连接到系统时我们启动跟踪，因此您现在可以跳过设备摘要事件。

![microsoft 网络监视器](images/devicefailure-etl1.png)

## <a name="event-description-and-data-payload"></a>事件说明和数据有效负载


示例日志中的设备摘要事件后的第一个事件是一个 USB 集线器等待唤醒 IRP 已完成的事件。 我们插入设备，并且主机控制器或集线器唤醒在响应中。 若要确定哪个组件唤醒，请查看事件的数据。 数据已在帧详细信息窗格中，大约采用以下格式的树状结构中所示：

```cpp
Frame information
ETW event header information
    ETW event descriptor (Constant information about the event ID such
    as error level)
Event payload (Data logged at the time of the event)
    Name of a USB-specific structure
        Structure members and their values (Types: numbers, strings,
        or arrays)
    ...
```

展开 USB 集线器等待唤醒 IRP 完成事件的有效负载数据，您将看到 ETW 结构，它名为 fid\_USBHUB\_中心。 结构的名称具有以下组件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>fid_</strong></p></td>
<td><p>USB ETW 结构典型前缀。</p></td>
</tr>
<tr class="even">
<td><p> <strong>USBHUB_</strong></p></td>
<td><p>指示 USB 集线器驱动程序记录事件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>字符串的其余部分</strong></p></td>
<td><p>该结构的数据描述的对象的名称。 对于此事件，它是一个中心对象。</p></td>
</tr>
</tbody>
</table>



USB 集线器驱动程序使用**fid\_USBHUB\_中心**结构来描述的 USB 集线器。 其数据有效负载中具有此中心结构事件到中心，请参阅，我们可以使用该结构的内容来标识特定的中心。 图 4 显示帧详细信息窗格中，使用**fid\_USBHUB\_中心**结构展开以显示其字段。

![microsoft 网络监视器-帧详细信息](images/framedetails.png)

中心结构是非常类似于两个其他通常出现在 USB ETW 事件的结构：**fid\_USBHUB\_设备**并**fid\_USBPORT\_设备**. 以下重要字段是普遍适用于所有三个结构：

<a href="" id="fid-idvendor"></a>**fid\_idVendor**  
USB 供应商 ID (VID) 的设备。

<a href="" id="-fid-idproduct"></a> **fid\_idProduct**  
USB 产品 ID (PID) 的设备。

<a href="" id="-fid-portpath"></a> **fid\_PortPath**  
通过这些附加的 USB 设备的基于 1 的中心端口号的列表。 在列表中的端口号包含在**PortPathDepth**字段。 对于根 hub 设备，此列表是全为零。 直接连接到根集线器端口，PortPath 中的值的 USB 设备\[0\]是设备附加到的端口的根集线器端口号。 通过一个或多个附加的 USB 集线器连接的 USB 设备的中心端口号列表启动与根集线器端口，并继续执行 （按顺序列出的距离根集线器） 的其他中心。 忽略任何零。 例如：

| 示例值         | 描述                                                                                                                       |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| \[0, 0, 0, 0, 0, 0\] | 该事件是指根中心 （在 PC 上，通过 USB 主控制器直接控制的端口）。                                  |
| \[3, 0, 0, 0, 0, 0\] | 该事件是指一个中心或插入到根中心的端口号 3 的设备。                                            |
| \[3, 1, 0, 0, 0, 0\] | 中心插入根中心的端口 3。 事件是指一个中心或插入此外部集线器端口 1 的设备。 |



你应监视感兴趣的任何设备的端口路径。 当枚举设备时，视频和 PID 是未知和记录为 0。 VID 和 PID 不在如重置某些低级别设备请求过程中显示并挂起。 这些请求发送到设备插入到中心。

在我们的示例日志，等待唤醒完成事件具有端口路径用六个零。 该事件指示根集线器中的等待唤醒操作。 这是逻辑因为我们的操作： 我们插入设备的根集线器端口，因此根集线器唤醒。

## <a name="usb-netmon-filters"></a>USB Netmon 筛选器


如果您有时间，您可以检查每个事件日志中按时间顺序。 即使使用体验，很难快速扫描从而确定重要事件的事件说明的列表。 若要查找多个未知的设备的原因快速，可以使用 Netmon 筛选功能。

**USB 错误筛选器**

若要激活中 Netmon 的 USB 错误筛选器，请单击**筛选器-&gt;显示筛选器-&gt;加载筛选器-&gt;标准筛选器-&gt; USB-&gt; USB 集线器错误**，然后单击**Apply**中**显示筛选器**窗格。

USB 错误筛选器用于限制到仅满足下表中所示的条件的事件的列表。

| 筛选器文本                                                                       | 描述                                                                                                                                               |
|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| (USBPort\_MicrosoftWindowsUSBUSBPORT AND NetEvent.Header.Descriptor.Opcode == 34) | 具有操作码 34 的 USB 端口事件是端口的错误。                                                                                                      |
| (USBHub\_MicrosoftWindowsUSBUSBHUB AND NetEvent.Header.Descriptor.Opcode == 11)   | 具有操作码 11 的 USB 集线器事件是集线器错误。                                                                                                        |
| (NetEvent.Header.Descriptor.Level == 0x2)                                         | 具有级别 0x2 事件通常是错误。                                                                                                            |
| (USBHub\_MicrosoftWindowsUSBUSBHUB AND NetEvent.Header.Descriptor.Id == 210)      | 具有 ID 210 USB 集线器事件是"USB 集线器异常记录"事件。 有关详细信息，请参阅[了解错误事件和状态代码](#status-codes)。 |



下图显示了事件中显示的较小的集**帧摘要**窗格后我们将 USB 错误筛选器应用到我们的示例跟踪日志。

![microsoft 网络监视器](images/devicefailure-etl2.png)

若要查看的一系列错误的概述，您可以简要查看每个错误事件。 要观察的重要字段包括**fid\_NtStatus**， **fid\_UsbdStatus**，以及**fid\_DebugText**。 有关详细信息，请参阅[了解错误事件和状态代码](#status-codes)。 若要关闭筛选器，请单击**删除**按钮**显示筛选器**窗格。

**自定义网络监视器筛选器**

可以在网络监视器中创建自定义筛选器。 最简单方法是通过以下方式之一从屏幕上的数据创建筛选器：

-   右键单击某个字段中的**帧详细信息**窗格，然后选择**添加到显示筛选器所选的值**。
-   右键单击某个字段中的**帧摘要**窗格，然后选择**添加\[字段名\]显示筛选器到**。

您可以更改运算符 (如 OR、 AND、 和 = =) 和筛选器值以生成相应的筛选器表达式。
## <a name="understanding-error-events-and-status-codes"></a>了解错误事件和状态代码


在我们未知的设备的示例中，有的大多数 USB 中心异常**fid\_DebugText** CreateDeviceFailure 数据。 不清楚如何严重的例外是，但调试文本提供了有关原因的提示： 与新的设备相关的操作失败。 现在，假设相邻创建设备失败事件是冗余的。 最后两个例外情况是 CreateDeviceFailure\_弹出窗口和 GenErr\_UserIoctlFailed。 弹出窗口异常听起来像一个错误，已公开给用户，但这些错误的所有可能与未知的设备问题。

USB 错误事件和其他事件，提供有价值信息有关的问题其数据中有状态的值。 下表中使用的资源，可以找到有关状态值。

| 状态类型                                                          | 资源                                                                                                                                                                                                                         |
|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **fid\_NtStatus**                                                    | 请参阅[NTSTATUS 值](https://go.microsoft.com/fwlink/p/?linkid=617532)。                                                                                                                                                          |
| USB 请求块 (URB) 的状态字段或**fid\_UsbdStatus** | 查找的值作为 USBD\_状态中 inc\\api\\usb.h Windows Driver Kit (WDK) 中。 此外可以使用[USBD\_状态](https://msdn.microsoft.com/library/windows/hardware/ff539136)。 本主题列出的符号名称和含义 USBD\_状态值。 |



## <a name="reading-backwards-from-problem-events"></a>向后从问题事件读取


之前的错误事件记录的事件可能提供有关错误的原因的重要线索。 您应查看之前要尝试确定未知设备的根本原因的错误记录的事件。 在此示例中，启动从 CreateDeviceFailure 查看后向\_弹出事件，第二个至最后一个异常。 选择启用 USB 错误筛选器时，此事件，然后单击**删除**中**显示筛选器**窗格。 USB 错误筛选器仍会显示在**显示筛选器**窗格中，并且您可以重新将其应用更高版本。 但现在禁用筛选器和**帧摘要**窗格中显示的所有事件，此图中所示。

![microsoft 网络监视器](images/devicefailure-etl3.png)

恰好在 CreateDeviceFailure 之前记录的两个事件\_弹出事件是调度和 USB 控制传输完成。 **Fid\_USBPORT\_设备**端口路径字段为零的两个事件，指示传输的目标是根集线器。 在 fid\_USBPORT\_URB\_控件\_传输结构的完成事件，状态为零 (USBD\_状态\_成功)，指示传输是否成功。 继续检查上一事件。

接下来两个以前的事件是第四个 （最终） 创建设备失败事件和第四个 （最终） CreateDeviceFailure 异常，从而我们先前检查。

下一步之前的事件是终结点关闭。 此事件意味着终结点不再可用。 事件数据描述该设备上的设备和终结点。 设备端口路径是\[1、 0，0，0，0，0\]。 我们运行的跟踪系统以及我们已连接的设备具有只有主机控制器 （根中心），因此此端口路径不描述集线器。 已关闭的终结点必须是单个我们插入的设备上，现在我们知道设备的路径为 1。 很可能将驱动程序进行设备的终结点无法访问，因为以前遇到的问题。 继续检查上一事件。

下一步之前的事件是已完成的 USB 控制传输。 事件数据显示传输的目标是 （端口路径为 1） 的设备。 Fid\_USBPORT\_终结点\_描述符结构指示终结点的地址是 0，因此，这是 USB 定义的默认控制终结点。 URB 状态为 0xC0000004。 状态不为零，因为传输可能不成功。 有关详细信息此 USBD\_状态值，请参阅 usb.h 并[了解错误事件和状态代码](#status-codes)。

```cpp
#define USBD_STATUS_STALL_PID ((USBD_STATUS)0xC0000004L)
```

含义：设备返回停滞数据包标识符。 哪些请求已停止的终结点？ 记录事件的其他数据指示该请求是标准的设备控制请求。 下面是已分析的请求：

```cpp
  Frame: Number = 184, Captured Frame Length = 252, MediaType = NetEvent 
+ NetEvent: 
- MicrosoftWindowsUSBUSBPORT: Complete Internal URB_FUNCTION_CONTROL_TRANSFER 
  - USBPORT_ETW_EVENT_COMPLETE_INTERNAL_URB_FUNCTION_CONTROL_TRANSFER: Complete Internal URB_FUNCTION_CONTROL_TRANSFER 
   + fid_USBPORT_HC: 
   + fid_USBPORT_Device: 
   + fid_USBPORT_Endpoint: 
   + fid_USBPORT_Endpoint_Descriptor: 
   + fid_URB_Ptr: 0x84539008 
   - ControlTransfer: 
    + Urb: Status = 0xc0000004, Flags 0x3, Length = 0 
    - SetupPacket: GET_DESCRIPTOR 
     + bmRequestType: (Standard request) 0x80 
       bRequest: (6) GET_DESCRIPTOR 
       Value_DescriptorIndex: 0 (0x0) 
       Value_DescriptorType: (1) DEVICE 
       _wIndex: 0 (0x0) 
       wLength: 64 (0x40)
```

合并 bRequest (获取\_描述符) 的值\_DescriptorType （设备），并且您可以确定该请求是 get 设备描述符。

若要继续的 USB 枚举，设备应对其设备描述符与此请求做出响应。 相反，设备将停止请求，这会导致枚举失败。 因此，所有四个创建设备失败而引起的设备描述符的停止请求。 已确定该设备是未知的因为枚举失败和枚举失败，因为设备未完成其设备描述符的请求。

## <a name="related-topics"></a>相关主题
[使用 USB ETW](using-usb-etw.md)  
[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  



