---
description: 本主题介绍客户端驱动程序如何构建 USB 请求块 (URB) 将数据传入和传出 USB 设备中的同步终结点。
title: 如何将数据传输到 USB 常时等量终结点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b6fa88f50dee542dc59f07317efdf9e0dc096aa
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009831"
---
# <a name="how-to-transfer-data-to-usb-isochronous-endpoints"></a>如何将数据传输到 USB 常时等量终结点


本主题介绍客户端驱动程序如何构建 USB 请求块 (URB) 将数据传入和传出 USB 设备中的同步终结点。

 (USB) 设备的通用串行总线可支持同步终结点以稳定的速率传输时间相关的数据，例如使用音频/视频流式处理。 若要传输数据，客户端驱动程序会发出请求以便向同步终结点读取数据或向其写入数据。 因此，主机控制器会启动按固定间隔轮询设备发送或接收数据的同步传输。

对于高速和全速设备，轮询是通过使用 (传入/传出) 令牌数据包来完成的。 当终结点准备发送数据时，设备会通过发送数据来响应其中一个 IN 令牌数据包。 若要写入设备，主机控制器会发送输出令牌数据包，后跟数据包。 主机控制器或设备不发送任何握手数据包，因此没有保证的传递。 由于主机控制器不会尝试重试传输，因此在发生错误时可能会丢失数据。

对于同步传输，主机控制器会在总线上保留一定时间段。 若要管理同步终结点的保留时间，则该时间划分为连续的逻辑 chucks 称为 " *总线间隔*"。 总线间隔的单位取决于总线速度。

对于全速，总线间隔为 *帧*。 帧的长度为1毫秒。

为实现高速和 SuperSpeed，总线间隔为 microframe。 Microframe 的长度为125微秒。 八个连续 microframes 构成一个高速或 SuperSpeed 帧。

同步传输基于数据包。 本主题中的 " *同步数据包* " 一词是指在一个总线间隔内传输的数据量。 终结点的特征确定每个数据包的大小是固定的，并由终结点的特征确定。

客户端驱动程序通过为请求创建 URB 并将 URB 提交到 USB 驱动程序堆栈，开始同步传输。 请求由 USB 驱动程序堆栈中的一个较低的驱动程序处理。 收到 URB 后，USB 驱动程序堆栈会执行一组验证并计划该请求的事务。 为了全速，每个总线间隔内传输的同步数据包包含在网络上的单个事务中。 某些高速设备允许在总线间隔内使用多个事务。 在这种情况下，客户端驱动程序可以在 (URB) 的单个请求中发送或接收同步数据包中的更多数据。 SuperSpeed 设备支持多个事务和突发传输，允许每个总线间隔更多的字节。 有关突发传输的详细信息，请参阅 USB 3.0 规范页9-42。

### <a name="prerequisites"></a>先决条件

在为同步传输创建请求之前，必须了解为同步终结点打开的管道的相关信息。

使用 Windows 驱动模型 (WDM) 例程的客户端驱动程序在[**USBD \_ 接口 \_ 列表 \_ 项**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)数组的[**USBD \_ 管道 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)结构之一中包含管道信息。 客户端驱动程序在驱动程序的前一请求中获取了该数组，以便在设备中选择配置或接口。

Windows 驱动程序框架 (WDF) 客户端驱动程序必须获取对框架目标管道对象的引用，并调用 [**WdfUsbTargetPipeGetInformation**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation) 以获取 [**WDF \_ USB \_ 管道 \_ 信息**](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information) 结构中的管道信息。

根据管道信息确定此信息集：

-   主机控制器可将多少数据发送到每个数据包中的管道。

    客户端驱动程序可在请求中发送的数据量不能超过主机控制器可以从终结点发送或接收的最大字节数。 最大字节数由[**USBD \_ 管道 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)和[**WDF \_ USB \_ 管道 \_ 信息**](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)结构的**MaximumPacketSize**成员指示。 USB 驱动程序堆栈在选择配置或选择接口请求期间设置 **MaximumPacketSize** 值。

    对于全速设备， **MaximumPacketSize** 是从终结点描述符的 **wMaxPacketSize** 字段的第11位派生的，它指示终结点可以在事务中发送或接收的最大字节数。 对于全速设备，控制器每个总线间隔发送一个事务。

    在高速同步传输中，如果终结点允许，主机控制器可以在总线间隔内发送其他事务。 其他事务的数目由设备设置，并在 **wMaxPacketSize**的第12位中指示。 该数字可以是0、1或2。 如果 12. 11 指示0，则终结点不支持每个 microframe 的其他事务。 如果数字为1，则主机控制器可以发送额外的事务 (每个 microframe) 的两个事务总计;2表示每个 microframe) 总共 (三个事务的其他事务。 USB 驱动程序堆栈设置的 **MaximumPacketSize** 值包含可在其他事务中发送的字节数。

    对于 SuperSpeed 同步传输，USB \_ SuperSpeed \_ 终结点伴随描述符的某些值 \_ \_ (参阅 Usbspec) 很重要。 USB 驱动程序堆栈使用这些值来计算总线间隔中的最大字节数。

    -   终结点伴随描述符的**Mult**字段。 在 SuperSpeed 同步传输中，附加事务 (非常类似于高速设备) 被称为突发事务。 **Mult**值指示终结点支持的突发事务的最大数量。 在服务间隔中，最多可以有三个 (索引为0到 2) 的突发事务。
    -   终结点伴随描述符的**bMaxBurst**字段。 此值指示单个突发事务中可以存在的 **wMaxPacketSize** 块的数量。 在突发事务中，最多可以有16个块 (索引0到15个) 。
    -   **wBytesPerInterval** 指示主机可以在总线间隔中发送或接收的总字节数。 即使每个总线间隔的最大字节数可以计算为 (**bMaxBurst**+ 1) \* (**Mult**+ 1) \* **wMaxPacketSize**，USB 3.0 规范也建议改为使用 **wBytesPerInterval** 值。 **WBytesPerInterval**值必须小于或等于该计算值。

    **重要提示**  对于客户端驱动程序，以上所述的值仅用于信息。 驱动程序必须始终使用终结点描述符的 **MaximumPacketSize** 值来确定传输缓冲区的布局。



-   终结点发送或接收数据的频率。

    **间隔**成员用于确定终结点可以发送或接收数据的频率。 设备设置该值，并且客户端驱动程序无法对其进行更改。 USB 驱动程序堆栈使用另一个数字来确定它将同步数据包插入数据流的频率：轮询周期，它派生自 **间隔** 值。

    对于全速传输， **时间间隔** 和轮询周期值始终为 1;USB 驱动程序堆栈忽略其他值。

    下表显示了 SuperSpeed 传输的 **时间间隔** 和计算出的轮询周期：

    | 时间间隔 | 轮询周期 (2Interval-1)                       |
    |----------|---------------------------------------------------|
    | 1        | 2数据每个总线间隔传输一次。        |
    | 2        | pps-2每隔一个总线间隔传输数据。 |
    | 3        | 4数据每四个总线间隔传输一次。 |
    | 4        | 8数据每第8个总线间隔传输一次。 |



-   每个总线速度的数据包数量有哪些限制。

    在 URB 中，最多只能为全速设备发送255同步数据包;SuperSpeed 设备的 URB 中的数据包。1024 在 URB 中发送的数据包数必须是每个帧中的数据包数的倍数。

    | 轮询周期 | 高速/SuperSpeed 的数据包数 |
    |----------------|---------------------------------------------|
    | 1              | 8的倍数                               |
    | 2              | 4的倍数                               |
    | 3              | 2的倍数                               |
    | 4              | 任意                                         |



请考虑使用 **wMaxPacketSize** 的全速终结点的示例为1023。 在此示例中，应用程序提供了25575字节的缓冲区。 该缓冲区的传输要求25个同步数据包 (25575/1023) 。

请考虑使用终结点描述符中指示的以下特性的示例高速终结点。

-   **wMaxPacketSize** 为1024。
-   第12位 ... 11 指示另外两个事务。
-   **间隔** 为1。

在客户端驱动程序选择配置后，同步管道的 **MaximumPacketSize** 表示3072字节 (total \* **wMaxPacketSize**) 。 其他事务允许客户端驱动程序在每个 microframe 中传输3072字节，并在一帧中传输24576字节总计。 下图显示了在一个 microframe 中传输同步数据包以实现高速传输的频率。

![同步传输](images/iso-packets.png)

请考虑一个示例 SuperSpeed 终结点，其中包含终结点和 SuperSpeed 终结点伴随描述符中指出的这些特征：

-   **wMaxPacketSize** 为1024。
-   **bMaxBurst** 为15。
-   **间隔** 为1。
-   **Mult** 为2。
-   **wBytesPerInterval** 为45000。

在前面的示例中，即使可以将最大字节数计算为 **wMaxPacketSize** \* (**bMaxBurst** + 1) \* (**Mult** + 1) 生成了49152个字节，设备将该值限制为45000字节的 **wBytesPerInterval** 值。 该值还会反映在 **MaximumPacketSize** 45000 中。 客户端驱动程序只能使用 **MaximumPacketSize** 值。 在此示例中，可以将请求划分为三个突发事务。 前两个突发事务每个都包含16个 **wMaxPacketSize**块。 最后一个突发事务包含12个区块来容纳剩余字节。 此图显示了轮询间隔和通过同步数据包传输的 SuperSpeed 传输的字节数。

![superspeed 同步](images/iso-packets-superspeed.png)

下面的过程介绍如何生成对同步传输的请求。

1.  获取每个同步数据包的大小。
2.  确定每帧同步数据包的数量。
3.  计算保存整个传输缓冲区所需的同步数据包的数量。
4.  分配 [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb) 结构来描述传输的详细信息。
5.  指定每个同步数据包的详细信息，如数据包偏移量。

有关发送同步传输请求的完整代码示例，请 USBSAMP。

本主题中的此示例简化了同步传输的 USBSAMP 实现。 该示例计算传输所需的总帧数。 根据可在帧中发送的数据量，传输缓冲区分为较小的块大小字节数。

以下过程然后详细阐述前面的步骤，并显示客户端驱动程序可用于构建和发送高速同步终结点的同步传输请求的计算和例程。 此过程中使用的值基于前面介绍的示例终结点特征。

<a name="instructions"></a>Instructions
------------

### <a name="step-1-get-the-size-of-an-isochronous-packet"></a><a href="" id="get-the-size-of-an-isochronous-packet--"></a>步骤1：获取同步数据包的大小。

检查管道的 **MaximumPacketSize** 值，确定同步数据包的大小。

对于全速传输，同步数据包的大小是可以在一帧中传输的字节数。 对于高速和 SuperSpeed 传输，同步数据包的大小是可以在一个 microframe 中传输的总字节数。 这些值在管道的 **MaximumPacketSize**中指示。

在此示例中，每个帧的 **MaximumPacketSize** 为1023字节 (全速) ;每 microframe 3072 字节 (高速) ;45000字节/microframe (SuperSpeed) 。

**注意** **MaximumPacketSize** 值指示同步数据包允许的最大大小。 客户端驱动程序可将每个同步数据包的大小设置为小于 **MaximumPacketSize** 值的任何值。



### <a name="step-2-determine-the-number-of-isochronous-packets-per-frame"></a><a href="" id="determine-the-number-of-isochronous-packets-per-frame-"></a>步骤2：确定每帧同步数据包的数量。

对于全速传输，你可以在每个帧中传输一个同步数据包。

对于高速和 SuperSpeed 传输，此值必须派生自间隔值。 在此示例中，Interval 为1。 因此，同步数据包数必须每帧8个。 有关其他间隔值，请参阅先决条件部分中的表。

### <a name="step-3-calculate-the-number-of-isochronous-packets-that-are-required-to-hold-the-entire-transfer-buffer"></a><a href="" id="calculate-the-number-of-isochronous-packets-that-are-required-to-hold-the-entire-transfer-buffer-"></a>步骤3：计算保存整个传输缓冲区所需的同步数据包的数量。

计算传输整个缓冲区所需的同步数据包的数量。 可以通过将传输缓冲区的长度除以同步数据包的大小来计算此值。

在此示例中，我们假设每个同步数据包的大小为 **MaximumPacketSize** ，传输缓冲区长度为 **MaximumPacketSize** 值的倍数。

例如，对于全速传输，提供的25575字节缓冲区需要25个同步数据包 (25575/1023) 。 对于高速传输，大小为24576的缓冲区分为8个同步数据包 (24576/3072) 用于传输。 对于 SuperSpeed，大小为360000字节的缓冲区适用于8个同步数据包 (360000/45000) 。

客户端驱动程序应验证这些要求：

-   同步数据包的数目必须是每帧数据包数的倍数。
-   对于全速设备，传输所需的最大同步数据包数不得超过 255;对于高速或 SuperSpeed 设备，1024。

### <a name="step-4-allocate-an-urb-structure-to-describe-the-details-of-the-transfer"></a><a href="" id="allocate-an-urb-structure-to-describe-the-details-of-the-transfer-"></a>步骤4：分配 URB 结构来描述传输的详细信息。

1.  在非分页池中分配 [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb) 结构。

    如果你的客户端驱动程序使用 WDM 例程，则驱动程序必须调用 [**USBD \_ IsochUrbAllocate**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate) （如果你有适用于 Windows 8 的 Windows 驱动程序工具包 (WDK) 。 客户端驱动程序可以使用例程来面向 Windows Vista 和更高版本的 Windows 操作系统。 如果没有适用于 Windows 8 的 WDK，或者客户端驱动程序适用于早期版本的操作系统，则可以通过调用 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)在堆栈或非分页池中分配结构。

    WDF 客户端驱动程序可以调用 [**WdfUsbTargetDeviceCreateIsochUrb**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb) 方法为 [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb) 结构分配内存。

2.  [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的**UrbIsochronousTransfer**成员指向一个[** \_ URB \_ ISOCH \_ 传输**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_isoch_transfer)结构，该结构描述了同步传输的详细信息。 初始化以下 **UrbIsochronousTransfer** 成员，如下所示：
    -   将 **UrbIsochronousTransfer** 成员设置为 URB 的大小。 若要获取 URB 的大小，请调用 [**获取 \_ ISO \_ URB \_ size**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-get_iso_urb_size) 宏并指定数据包的数量。
    -   将 **UrbIsochronousTransfer** 成员设置为 `URB_FUNCTION_ISOCH_TRANSFER` 。
    -   将 **UrbIsochronousTransfer. NumberOfPackets** 成员设置为同步数据包的数量。
    -   将 **UrbIsochronousTransfer** 设置为与终结点关联的管道的不透明句柄。 请确保管道句柄是通用串行总线 (USB) 驱动程序堆栈使用的 USBD 管道句柄。

        若要获取 USBD 管道句柄，WDF 客户端驱动程序可以调用 [**WdfUsbTargetPipeWdmGetPipeHandle**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle) 方法，并为框架的管道对象指定 WDFUSBPIPE 句柄。 WDM 客户端驱动程序必须使用在[**USBD \_ 管道 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)结构的**PipeHandle**成员中获得的相同句柄。

    -   指定传输方向。 将 **UrbIsochronousTransfer** 设置为中的 USBD \_ 传输 \_ 方向 \_ ， (从设备) 读取;USBD \_ 传输 \_ \_ 向外传输 (写入到设备) 的方向。
    -   \_ \_ 在 UrbIsochronousTransfer 中指定 USBD START ISO \_ TRANSFER TRANSFER \_ 标志。 **UrbIsochronousTransfer**TransferFlags. 该标志指示 USB 驱动程序堆栈在下一个合适的帧中发送传输。 第一次客户端驱动程序发送此管道的同步 URB 时，驱动程序堆栈会尽快在 URB 中发送同步数据包。 USB 驱动程序堆栈跟踪下一个帧，以便用于该管道上的后续 URBs。 如果在发送使用 USBD START ISO TRANSFER ASAP 标志的后续按下同步 URB 时存在延迟 \_ \_ \_ \_ ，则驱动程序堆栈会将该 URB 的部分或全部数据包视为延迟，而不会传输这些数据包。

        \_ \_ \_ \_ 如果堆栈在完成该管道的上一个 URB 后未接收到1024帧的同步 URB，则 USB 驱动程序堆栈会重置其 USBD 启动 ISO 传输尽快启动帧跟踪。 \_可以指定开始帧，而不是指定 USBD start \_ ISO \_ TRANSFER \_ ASAP 标志。 有关详细信息，请参阅“备注”部分。

    -   指定传输缓冲区及其大小。 可以在 TransferBuffer 中设置指向缓冲区的指针，也可以在**UrbIsochronousTransfer**中设置**UrbIsochronousTransfer**描述缓冲区的[**MDL**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl) 。

        若要检索传输缓冲区的 [**MDL**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl) ，WDF 客户端驱动程序可以调用 [**WdfRequestRetrieveOutputWdmMdl**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) 或 [**WdfRequestRetrieveInputWdmMdl**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)，具体取决于传输方向。

### <a name="step-5-specify-the-details-of-each-isochronous-packet-in-the-transfer"></a><a href="" id="specify-the-details-of-each-isochronous-packet-in-the-transfer-"></a>步骤5：指定传输中每个同步数据包的详细信息。

USB 驱动程序堆栈分配新的 [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb) 结构，该结构足以容纳每个同步数据包的相关信息，而不是包含在包中的数据。 在 **URB** 结构中， **UrbIsochronousTransfer. IsoPacket** 成员是一个 [**USBD \_ ISO \_ 数据包 \_ 描述符**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_iso_packet_descriptor) 的数组，用于描述传输中每个同步数据包的详细信息。 数据包必须是连续的。 数组中的元素数必须是 URB 的 **UrbIsochronousTransfer. NumberOfPackets** 成员中指定的同步数据包的数量。

对于高速传输，数组中的每个元素都与一个 microframe 中的一个同步数据包相关联。 对于全速，每个元素都与一帧中传输的一个同步数据包关联。

对于每个元素，指定请求的整个传输缓冲区开始时每个同步数据包的字节偏移量。 可以通过设置 **UrbIsochronousTransfer. IsoPacket i 来指定该值 \[ \] 。Offset** 成员。 USB 驱动程序堆栈使用指定的值跟踪要发送或接收的数据量。

**设置全速传输的偏移量**

在此示例中，这些是以全速传输的传输缓冲区的数组项。 在全速中，客户端驱动程序有一个帧用于传输一个同步数据包，最多1023个字节。 25575字节的传输缓冲区可以容纳25个同步数据包，每个1023字节长。 整个缓冲区需要总共25帧。

``` syntax
Frame 1 IsoPacket [0].Offset = 0 (start address)
Frame 2 IsoPacket [1].Offset = 1023
Frame 3 IsoPacket [2].Offset = 2046
Frame 4 IsoPacket [3].Offset = 3069
...
Frame 25 IsoPacket [24].Offset = 24552

Total length transferred is 25,575 bytes.
```

**设置高速传输的偏移量**

在此示例中，这些是高速传输缓冲区的数组项。 该示例假设缓冲区为24576字节，客户端驱动程序有一个帧用于传输八个同步数据包，每个3072字节长。

``` syntax
Microframe 1 IsoPacket [0].Offset = 0 (start address)
Microframe 2 IsoPacket [1].Offset = 3072
Microframe 3 IsoPacket [2].Offset = 6144
Microframe 4 IsoPacket [3].Offset = 9216
Microframe 5 IsoPacket [4].Offset = 12288
Microframe 6 IsoPacket [5].Offset = 15360
Microframe 7 IsoPacket [6].Offset = 18432
Microframe 8 IsoPacket [7].Offset = 21504

Total length transferred is 24,576 bytes.
```

**设置 SuperSpeed 传输的偏移量**

对于本示例，这是 SuperSpeed 的数组偏移量。 最多可以在一个帧中传输45000个字节。 大小360000的传输缓冲区适用于8个 microframes。

``` syntax
Microframe 1 IsoPacket [0].Offset = 0 (start address)
Microframe 2 IsoPacket [1].Offset = 45000
Microframe 3 IsoPacket [2].Offset = 90000
Microframe 4 IsoPacket [3].Offset = 135000
Microframe 5 IsoPacket [4].Offset = 180000
Microframe 6 IsoPacket [5].Offset = 225000
Microframe 7 IsoPacket [6].Offset = 270000
Microframe 8 IsoPacket [7].Offset = 315000

Total length transferred is 360,000 bytes.
```

**UrbIsochronousTransfer. IsoPacket \[ i \] **。Length 成员不表示每个数据包的 URB 的长度。 **IsoPacket \[ i \] 。** 由 USB 驱动程序堆栈更新长度，以指示从设备接收的、用于同步传输的实际字节数。 对于同步传出传输，驱动程序堆栈会忽略在 IsoPacket i 中设置的值 ** \[ \] 。Length**。

<a name="remarks"></a>备注
-------

**指定传输的起始 USB 帧号**

URB 的 **UrbIsochronousTransfer. StartFrame** 成员指定传输的起始 USB 帧号。 客户端驱动程序提交 URB 的时间与 USB 驱动程序堆栈处理 URB 的时间之间始终存在延迟。 因此，当驱动程序提交 URB 时，客户端驱动程序应始终指定一个晚于当前帧的开始帧。 若要检索当前帧号，客户端驱动程序可以将 URB \_ 函数 \_ 获取 \_ 当前 \_ 帧 \_ 号请求发送到 USB 驱动程序堆栈 ([** \_ URB \_ 获取 \_ 当前 \_ 帧 \_ 号**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_get_current_frame_number)) 。

对于同步传输，当前帧与 **StartFrame** 值之间的绝对差异必须小于 USBD \_ ISO \_ 开始 \_ 帧 \_ 范围。 如果 StartFrame 不在正确的范围内，则 USB 驱动程序堆栈会设置 URB 标头的**Status**成员 (请参阅[** \_ URB \_ 标头**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_header)) 为 USBD \_ 状态 \_ 错误 \_ 开始 \_ 帧并放弃整个 URB。

在 URB 中指定的 **StartFrame** 值指示传输 URB 的第一个同步数据包的帧号。 后续数据包的帧号取决于终结点的总线速度和轮询周期值。 例如，对于全速传输，将在 **StartFrame**中传输第一个数据包;第二个数据包传输 **StartFrame**+ 1，依此类推。 在帧中，USB 驱动程序堆栈以全速方式传输同步数据包的方法如下所示：

``` syntax
Frame (StartFrame)   IsoPacket [0]
Frame (StartFrame+1) IsoPacket [1]
Frame (StartFrame+2) IsoPacket [2]
Frame (StartFrame+3) IsoPacket [3]
...
```

对于时间间隔值为1的高速设备，帧号会更改每个第8个 microframe。 在帧中，USB 驱动程序堆栈传输同步数据包的方式在帧中的显示方式如下：

``` syntax
Frame (StartFrame) Microframe 1 IsoPacket [0]
...
Frame (StartFrame) Microframe 8 IsoPacket [7]
Frame (StartFrame+1) Microframe 1 IsoPacket [8]
...
Frame (StartFrame+1) Microframe 8 IsoPacket [15]
Frame (StartFrame+2) Microframe 1 IsoPacket [16]
...
Frame (StartFrame+2) Microframe 8 IsoPacket [23]
```

当 USB 驱动程序堆栈处理 URB 时，驱动程序将丢弃 URB 中其帧号低于当前帧数的所有同步数据包。 驱动程序堆栈将每个丢弃的数据包的数据包描述符的 **status** 成员设置为 USBD \_ status \_ iso \_ NA \_ 后期 \_ USBPORT， \_ \_ \_ 不能通过硬件访问 USBD 状态 iso \_ \_ \_ ，或者 \_ \_ \_ 不 \_ 延迟访问 \_ USBD 状态 iso。 即使 URB 中的某些数据包被丢弃，驱动程序堆栈也只会尝试传输帧号大于当前帧号的数据包。

检查有效的 **StartFrame** 成员在高速传输中的速度稍微复杂一些，因为 USB 驱动程序堆栈会将每个同步数据包加载到高速 microframe;但是， **StartFrame** 中的值指的是 (全速) 帧号，而不是 microframe 的1毫秒。 例如，如果 URB 中记录的 **StartFrame** 值比当前帧少一，则驱动程序堆栈最多可以丢弃8个数据包。 确切丢弃的数据包数取决于与同步管道关联的轮询周期。

## <a name="isochronous-transfer-example"></a>同步传输示例


下面的代码示例演示如何创建 URB 以实现同步传输，以实现全速、高速和 SuperSpeed 传输。

```cpp
#define MAX_SUPPORTED_PACKETS_FOR_HIGH_OR_SUPER_SPEED 1024
#define MAX_SUPPORTED_PACKETS_FOR_FULL_SPEED 255

NTSTATUS CreateIsochURB  ( PDEVICE_OBJECT         DeviceObject,
                          PUSBD_PIPE_INFORMATION  PipeInfo,
                          ULONG                   TotalLength,
                          PMDL                    RequestMDL,
                          PURB                    Urb)
{  
    PDEVICE_EXTENSION        deviceExtension;
    ULONG                    numberOfPackets;
    ULONG                    numberOfFrames; 
    ULONG                    isochPacketSize = 0;
    ULONG                    transferSizePerFrame;
    ULONG                    currentFrameNumber;
    size_t                   urbSize;
    ULONG                    index;
    NTSTATUS                 ntStatus;  

    deviceExtension = (PDEVICE_EXTENSION) DeviceObject->DeviceExtension;

    isochPacketSize = PipeInfo->MaximumPacketSize;

    // For high-speed transfers
    if (deviceExtension->IsDeviceHighSpeed || deviceExtension->IsDeviceSuperSpeed) 
    {

        // Ideally you can pre-calculate numberOfPacketsPerFrame for the Pipe and 
        // store it in the pipe context.

        switch (PipeInfo->Interval) 
        {
        case 1:
            // Transfer period is every microframe (eight times a frame).
            numberOfPacketsPerFrame = 8;
            break;

        case 2:
            // Transfer period is every 2 microframes (four times a frame).
            numberOfPacketsPerFrame = 4;
            break;

        case 3:
            // Transfer period is every 4 microframes (twice in a frame).
            numperOfPacketsPerFrame = 2;
            break;

        case 4:
        default: 
            // Transfer period is every 8 microframes (once in a frame).
            numberOfPacketsPerFrame = 1;
            break;
        }


        //Calculate the number of packets.
        numberOfPackets = TotalLength / isochPacketSize;

        if (numberOfPackets > MAX_SUPPORTED_PACKETS_FOR_HIGH_OR_SUPER_SPEED) 
        {
            // Number of packets cannot be  greater than 1024.  
            ntStatus = STATUS_INVALID_PARAMETER;
            goto Exit;
        }

        if (numberOfPackets % numberOfPacketsPerFrame != 0) 
        {

            // Number of packets should be a multiple of numberOfPacketsPerFrame
            ntStatus = STATUS_INVALID_PARAMETER;
            goto Exit;
        }

    } 
    else if (deviceExtension->IsDeviceFullSpeed) 
    {
        //For full-speed transfers
        // Microsoft USB stack only supports bInterval value of 1 for
        // full-speed isochronous endpoints.


        //Calculate the number of packets.
        numberOfPacketsPerFrame = 1;

        numberOfPackets = TotalLength / isochPacketSize;

        if (numberOfPackets > MAX_SUPPORTED_PACKETS_FOR_FULL_SPEED) 
        {
            // Number of packets cannot be greater than 255. 
            ntStatus = STATUS_INVALID_PARAMETER;
            goto Exit;
        }

    }

    // Allocate an isochronous URB for the transfer
    ntStatus = USBD_IsochUrbAllocate (deviceExtension->UsbdHandle, 
        numberOfPackets, 
        &Urb);

    if (!NT_SUCCESS(ntStatus)) 
    {
        ntStatus = STATUS_INSUFFICIENT_RESOURCES;
        goto Exit;
    }

    urbSize = GET_ISO_URB_SIZE(numberOfPackets);

    Urb->UrbIsochronousTransfer.Hdr.Length = (USHORT) urbSize;
    Urb->UrbIsochronousTransfer.Hdr.Function = URB_FUNCTION_ISOCH_TRANSFER;
    Urb->UrbIsochronousTransfer.PipeHandle = PipeInfo->PipeHandle;

    if (USB_ENDPOINT_DIRECTION_IN(PipeInfo->EndpointAddress)) 
    {
        Urb->UrbIsochronousTransfer.TransferFlags = USBD_TRANSFER_DIRECTION_IN;
    }
    else
    {
        Urb->UrbIsochronousTransfer.TransferFlags = USBD_TRANSFER_DIRECTION_OUT;
    }

    Urb->UrbIsochronousTransfer.TransferBufferLength = TotalLength;
    Urb->UrbIsochronousTransfer.TransferBufferMDL = RequestMDL;
    Urb->UrbIsochronousTransfer.NumberOfPackets = numberOfPackets;
    Urb->UrbIsochronousTransfer.UrbLink = NULL;


    // Set the offsets for every packet for reads/writes

    for (index = 0; index < numberOfPackets; index++) 
    {
        Urb->UrbIsochronousTransfer.IsoPacket[index].Offset = index * isochPacketSize;
    } 

    // Length is a return value for isochronous IN transfers.  
    // Length is ignored by the USB driver stack for isochronous OUT transfers.

    Urb->UrbIsochronousTransfer.IsoPacket[index].Length = 0;
    Urb->UrbIsochronousTransfer.IsoPacket[index].Status = 0;

    // Set the USBD_START_ISO_TRANSFER_ASAP. The USB driver stack will calculate the start frame.
    // StartFrame value set by the client driver is ignored.
    Urb->UrbIsochronousTransfer.TransferFlags |= USBD_START_ISO_TRANSFER_ASAP;


Exit:

    return ntStatus;  
}  
```

## <a name="related-topics"></a>相关主题
[USB i/o 操作](usb-device-i-o.md)