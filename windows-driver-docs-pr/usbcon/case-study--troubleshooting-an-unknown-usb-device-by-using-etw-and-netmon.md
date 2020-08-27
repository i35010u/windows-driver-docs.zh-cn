---
description: 提供有关如何使用 USB ETW 和 Netmon 排查 Windows 无法识别的 USB 设备的示例。
title: 案例研究-排查未知 USB 设备问题
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bab9c24ffce0fc30c06a69c829e66ac9bde956a6
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969002"
---
# <a name="case-study-troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon"></a>案例研究：使用 ETW 和 Netmon 排查未知 USB 设备的问题

本主题提供有关如何使用 USB ETW 和 Netmon 排查 Windows 无法识别的 USB 设备的示例。

在此示例中，我们插入了一个设备，它在设备管理器和用户界面的其他部分 (UI) 中显示为未知设备。 硬件 ID \\ 未知。 为了进一步诊断，我们拔出了设备，开始 ETW 跟踪，并再次插入设备。 设备显示为未知设备后，会停止跟踪。

## <a name="about-the-unknown-device-problem"></a>关于未知设备问题

若要调试未知的 USB 设备问题，有助于了解当用户将设备插入系统时，USB 驱动程序堆栈对设备进行枚举的方法。 有关 USB 枚举的信息，请参阅标题为 " [usb Stack 如何枚举设备"](https://go.microsoft.com/fwlink/p/?linkid=617517)的博客文章。

通常，当 USB 驱动程序堆栈无法枚举设备时，集线器驱动程序仍会将设备到达报告给 Windows，并在设备管理器中将 USB 设备标记为未知设备。 设备的设备 ID 为 USB \\ VID \_ 0000&PID \_ 0000，硬件 ID 和兼容 ID （ \\ 未知）。 以下事件导致 USB 集线器驱动程序将 USB 设备枚举为未知设备：

* 枚举期间端口重置请求超时。
* 设置 USB 设备的地址请求失败。
* 请求 USB 设备的设备描述符失败。
* [USB 设备描述符](usb-device-descriptors.md)的格式不正确，验证失败。
* 配置描述符的请求失败。
* [USB 配置描述符](usb-configuration-descriptors.md)的格式不正确，验证失败。

在 Windows 7 中，无法枚举的未知设备将标记为设备管理器中的失败 [代码 43](https://go.microsoft.com/fwlink/p/?linkid=617523) 。

如果在设备管理器中使用故障 [代码 28](https://go.microsoft.com/fwlink/p/?linkid=617525) 对设备进行标记，则设备已成功枚举，但仍是未知设备。 此失败代码表明设备在枚举过程中未提供产品 ID 字符串，Windows 找不到用于安装驱动程序的设备的匹配 INF。

## <a name="starting-the-event-trace-analysis"></a>开始事件跟踪分析

由于这是设备故障，因此我们建议你将 Netmon 与 USB 分析器一起使用来分析日志文件。

### <a name="to-view-the-event-trace-log"></a>查看事件跟踪日志

1. 运行 Netmon，单击 "文件"-" ** &gt; &gt; 捕获**"，然后选择文件。
2. 在 " **帧摘要** " 窗格中选择第一个事件，该事件具有 SystemTrace 说明。 此图显示了在选择第一个事件时屏幕的外观。

    ![microsoft 网络监视器](images/devicefailure-etl.png)

3. 若要自定义 Netmon 显示的列，请右键单击列名称，然后选择 " **选择列**"。
4. 第一个事件（标识为 **SystemTrace**类型）包含有关日志的常规信息。 你可以展开 " **帧详细** 信息" 窗格中的信息树，以查看丢失的事件数和跟踪开始时间等信息。

## <a name="usb-device-summary-events"></a>USB 设备摘要事件

事件2是日志中的第一个 USB 事件。 此事件和多个后续事件描述了启动跟踪时连接到系统的 USB 主机控制器、集线器和设备。 我们可以将此事件组称为设备摘要事件，或者只是摘要事件。 与第一个事件类似，摘要事件不描述驱动程序活动。 摘要事件记录在日志记录会话开始时设备的状态。 其他事件表示在总线上发生的事件、与客户端驱动程序或系统的交互或内部状态的更改。

USB 集线器和 USB 端口驱动程序都记录摘要事件。 记录事件的驱动程序在 "协议名称" 列中标识。 例如，USB 端口驱动程序记录的事件具有 USBPort \_ MicrosoftWindowsUSBPORT 协议名称。 USB 事件跟踪通常包含一系列端口摘要事件，后跟一系列中心摘要事件。 许多 USB 端口和 USB 集线器摘要事件的描述中包含 "信息" 或 "特性" 字样。

如何确定摘要事件的结束时间？ 如果在启动日志时，在 USB 集线器事件的时间戳模式中出现重大中断，则中断可能是设备摘要的结束。 否则，在任何 USB 集线器事件之后的第一个 USB 端口事件可能是第一个非摘要事件。 图3在下面的页上显示此示例跟踪中的第一个非摘要事件。

在此示例中，启动跟踪时，目标设备未连接到系统，因此你现在可以跳过设备摘要事件。

![microsoft 网络监视器](images/devicefailure-etl1.png)

## <a name="event-description-and-data-payload"></a>事件说明和数据负载

在示例日志中，设备摘要事件之后的第一个事件是 USB 集线器等待唤醒 IRP 完成的事件。 接下来，我们插入了一个设备，主机控制器或集线器正在响应中唤醒。 若要确定正在唤醒哪个组件，请查看该事件的数据。 数据位于 "帧详细信息" 窗格中，其中显示的树结构大致如下所示：

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

展开 "USB 集线器等待唤醒 IRP 完成" 事件的负载数据，您将看到一个名为 fid USBHUB Hub 的 ETW \_ 结构 \_ 。 结构名称包含以下组件：

|术语|说明|
|----|----|
|**fid_**|USB ETW 结构的典型前缀。|
|**USBHUB_**|指示 USB 集线器驱动程序记录了该事件。|
|**字符串的其余部分**|结构的数据所描述的对象的名称。 对于此事件，它是一个中心对象。|

USB 集线器驱动程序使用 **fid \_ USBHUB \_ 集线器** 结构来描述 USB 集线器。 在其数据负载中具有此中心结构的事件指的是中心，我们可以使用结构的内容来识别特定的中心。 图4显示了 "帧详细信息" 窗格，其中的 **fid \_ USBHUB \_ 中心** 结构展开以显示其字段。

![microsoft 网络监视器-帧详细信息](images/framedetails.png)

中心结构非常类似于通常出现在 USB ETW 事件中的两个其他结构：**fid \_ USBHUB \_ 设备** 和 **fid \_ USBPORT \_ 设备**。 以下重要字段适用于所有三种结构：

|字段|说明|
|----|----|
|**fid_idVendor**|设备的 USB 供应商 ID (VID) |
|**fid_idProduct**|设备的 USB 产品 ID (PID) |
|**fid_PortPath**|USB 设备连接到的一个基于的集线器端口号列表。 列表中的端口号数目包含在 **PortPathDepth** 字段中。 对于根集线器设备，此列表全为零。 对于直接连接到根集线器端口的 USB 设备，PortPath 0 中的值 \[ \] 是设备连接到的端口的根集线器端口号。|

对于通过一个或多个附加 USB 集线器连接的 USB 设备，集线器端口号列表以根集线器端口开头，并继续以从根中心) 的距离 (的其他集线器继续。 忽略任何零。 例如：

| 示例值|说明|
|----|----|
|[0，0，0，0，0，0]|事件指的是 (计算机上的端口的根集线器，由 USB 主机控制器) 直接控制。|
|[3，0，0，0，0，0]|事件是指插入到根集线器端口号3的集线器或设备。|
|[3，1，0，0，0，0]|集线器插入根集线器端口3中。 事件是指插入到此外部集线器端口1的集线器或设备。|

应监视任何相关设备的端口路径。 枚举设备时，VID 和 PID 未知并记录为0。 在某些低级设备请求（如重置和暂停）期间，VID 和 PID 不会出现。 这些请求将发送到设备插入到的中心。

在我们的示例日志中，等待唤醒完成事件的端口路径包含六个零。 此事件表示根集线器上的等待唤醒操作。 这是因为我们的操作：我们已将设备插入根集线器端口，因此根集线器正在唤醒。

## <a name="usb-netmon-filters"></a>USB Netmon 筛选器

如果有时间，可以按时间顺序检查日志中的每个事件。 即使有经验，也很难通过扫描事件说明的列表来快速确定重要事件。 若要更快地找出未知设备的原因，可以使用 Netmon 筛选器功能。

### <a name="the-usb-error-filter"></a>USB 错误筛选器

若要在 Netmon 中激活 USB 错误筛选器，请单击 "**筛选器-> 显示" 筛选器-> 加载筛选器-> 标准筛选器-> usb-> Usb 集线器错误**"，然后在"**显示筛选器**"窗格中单击"**应用**"。

USB 错误筛选器将事件列表缩小到仅符合下表中所示的条件的事件列表。

|筛选文本|说明|
|-----|----|
| (USBPort_MicrosoftWindowsUSBUSBPORT 和 NetEvent = = 34) |具有 opcode 34 的 USB 端口事件是端口错误。|
| (USBHub_MicrosoftWindowsUSBUSBHUB 和 NetEvent = = 11) |具有 opcode 11 的 USB 集线器事件是集线器错误。|
| (NetEvent = = 0x2) |具有级别0x2 的事件通常是错误的。|
| (USBHub_MicrosoftWindowsUSBUSBHUB 和 NetEvent.Header.Descriptor.Id = = 210) | ID 为210的 USB 集线器事件是 "USB 集线器异常记录" 事件。 有关详细信息，请参阅 [了解错误事件和状态代码](#understanding-error-events-and-status-codes)。|

此图显示了将 USB 错误筛选器应用于示例跟踪日志后，在 " **帧摘要** " 窗格中显示的较小事件集。

![microsoft 网络监视器](images/devicefailure-etl2.png)

若要查看错误序列的概述，可以简单地查看每个错误事件。 需要注意的重要字段包括 **fid \_ NtStatus**、 **fid \_ UsbdStatus**和 **fid \_ DebugText**。 有关详细信息，请参阅 [了解错误事件和状态代码](#understanding-error-events-and-status-codes)。 若要关闭筛选器，请单击 "**显示筛选器**" 窗格中的 "**删除**" 按钮。

### <a name="custom-netmon-filters"></a>自定义 Netmon 筛选器

可以在 Netmon 中创建自定义筛选器。 最简单的方法是使用以下方法之一从屏幕上的数据创建筛选器：

* 右键单击 " **帧详细信息** " 窗格中的字段，然后选择 " **添加所选值" 以显示筛选器**。
* 右键单击 " **帧摘要** " 窗格中的字段，然后选择 " **添加 [字段名]" 以显示筛选器**。

您可以更改运算符 (例如 OR、AND、and = =) 和筛选器值以生成相应的筛选表达式。

## <a name="understanding-error-events-and-status-codes"></a>了解错误事件和状态代码

在未知设备示例中，大多数 USB 集线器例外都有 **fid_DebugText** 数据 CreateDeviceFailure。 这并不清楚异常的严重程度，但调试文本会给出原因提示：与新设备相关的操作失败。 现在，假定相邻的 "创建设备失败" 事件是冗余的。 最后两个例外是 CreateDeviceFailure_Popup 和 GenErr_UserIoctlFailed。 Popup 异常听起来像是向用户公开的错误，但所有这些错误都可能与未知设备问题相关。

USB 错误事件和其他事件的数据中具有状态值，这些值提供有关问题的重要信息。 您可以通过使用下表中的资源来查找有关状态值的信息。

|状态类型|资源|
|----|----|
|**fid_NtStatus**|请参阅 [NTSTATUS 值](https://go.microsoft.com/fwlink/p/?linkid=617532)。|
|USB 请求块的 "状态" 字段 (URB) 或 **fid_UsbdStatus**|在 Windows 驱动程序工具包 (WDK) 的 inc\api\usb.h 中查找作为 USBD_STATUS 的值。 你还可以使用 [USBD \_ 状态](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff539136(v=vs.85))。 本主题列出了 USBD 状态值的符号名称和含义 \_ 。|

## <a name="reading-backwards-from-problem-events"></a>从问题事件中反向读取

在错误事件发生之前记录的事件可能会提供有关错误原因的重要线索。 应查看出现错误之前记录的事件，以尝试确定未知设备的根本原因。 在此示例中，从 CreateDeviceFailure_Popup 事件开始向后查找第二个异常。 启用 USB 错误筛选器后选择此事件，然后在 "**显示筛选器**" 窗格中单击 "**删除**"。 USB 错误筛选器仍会显示在 " **显示筛选器** " 窗格中，您可以在以后重新应用此筛选器。 但现在筛选器处于禁用状态，并且 " **帧摘要** " 窗格将显示此图像中所示的所有事件。

![microsoft 网络监视器](images/devicefailure-etl3.png)

在 CreateDeviceFailure_Popup 事件之前记录的两个事件是一个调度和一个完整的 USB 控件传输。 这两个事件的 " **fid_USBPORT_Device** 端口路径" 字段均为零，这表示传输的目标是根中心。 在完成事件的 fid_USBPORT_URB_CONTROL_TRANSFER 结构中，状态为零 (USBD_STATUS_SUCCESS) ，这表示传输成功。 继续检查以前的事件。

接下来的两个事件是第四个 (最终) 创建设备失败事件和第四个 (最终) CreateDeviceFailure 异常，我们在前面进行了介绍。

下一个上一个事件是端点关闭。 此事件表示终结点不再可用。 事件数据描述设备和该设备上的终结点。 设备端口路径为 [1，0，0，0，0，0]。 在其上运行跟踪的系统只有主机控制器 (根中心) 以及我们连接的设备，因此此端口路径不描述集线器。 关闭的终结点必须位于接下来的单个设备上，现在我们知道设备的路径为1。 由于先前遇到的问题，导致设备终结点的驱动程序可能无法访问。 继续检查以前的事件。

下一个上一个事件是已完成的 USB 控件传输。 事件数据显示传输的目标是设备 (端口路径为 1) 。 Fid_USBPORT_Endpoint_Descriptor 结构指示终结点的地址为0，因此这是 USB 定义的默认控制终结点。 URB 状态为0xC0000004。 由于状态不为零，因此传输可能不成功。 有关此 USBD_STATUS 值的更多详细信息，请参阅 "usb .h" 和 " [了解错误事件和状态代码](#understanding-error-events-and-status-codes)"。

```cpp
#define USBD_STATUS_STALL_PID ((USBD_STATUS)0xC0000004L)
```

意思：设备返回了一个 "延迟数据包标识符"。 终结点停止了哪些请求？ 为事件记录的其他数据表明请求是标准的设备控制请求。 下面是已分析的请求：

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

将 bRequest (获取 \_ 描述符) 与值 \_ DESCRIPTORTYPE (设备) 合并，并确定请求是获取设备描述符。

若要继续使用 USB 枚举，设备应已使用其设备描述符对此请求做出响应。 相反，设备停止了请求，导致枚举失败。 因此，所有四个创建设备故障都是由停止对设备描述符的请求引起的。 您已确定设备未知，因为枚举失败并且枚举失败，因为设备没有完成其设备描述符的请求。

## <a name="related-topics"></a>相关主题

[使用 USB ETW](using-usb-etw.md)  
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  
