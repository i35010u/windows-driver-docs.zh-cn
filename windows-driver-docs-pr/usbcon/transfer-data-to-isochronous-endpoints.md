---
Description: 本主题介绍客户端驱动程序可以如何生成 USB 请求块 (URB) 将在同步终结点在 USB 设备中的数据传输。
title: 如何将数据传输到 USB 常时等量终结点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d7895644493e58c4d72ce0a7054007d12655b26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379913"
---
# <a name="how-to-transfer-data-to-usb-isochronous-endpoints"></a>如何将数据传输到 USB 常时等量终结点


本主题介绍客户端驱动程序可以如何生成 USB 请求块 (URB) 将在同步终结点在 USB 设备中的数据传输。

通用串行总线 (USB) 设备可以支持同步终结点将依赖于时间的数据以稳定速率，如与音频/视频流式处理。 若要将数据传输，客户端驱动程序发出请求以读取或写入到等时终结点的数据。 因此，主控制器启动同步传输的发送或通过按固定间隔轮询设备接收数据。

对于高速度和全速设备，轮询可通过使用 (IN/OUT) 令牌的数据包。 准备好发送数据的终结点时，设备响应之一在标记数据包通过发送数据。 要写入到设备，主机控制器发送带标记数据包跟数据包。 主机控制器或设备不会发送任何握手数据包，并且因此，没有任何有保证的传递。 因为主机控制器不会尝试重试传输，数据可能会丢失，如果发生错误。

对同步传输主机控制器保留某个总线上的时间段。 若要管理等时终结点的保留的时间，时间划分为称为连续逻辑 chuck*总线间隔*。 总线间隔的单位取决于总线速度。

对于全速运行，是总线间隔*帧*。 框架的长度为 1 毫秒。

对于高速度和 SuperSpeed，总线间隔为 microframe。 Microframe 的长度为 125 微秒为单位。 八个连续 microframes 构成一个高速或 SuperSpeed 框架。

同步传输所基于的数据包。 术语*同步数据包*本主题中引用的传输总线条系统总线间隔中的数据量。 终结点的特征确定每个数据包的大小是固定，由终结点的特征确定。

客户端驱动程序将开始创建请求 URB 并提交到 USB 驱动程序堆栈 URB 等时传输。 由一个 USB 驱动程序堆栈中较低的驱动程序处理请求。 一旦收到 URB，USB 驱动程序堆栈请求执行一系列验证和计划的事务。 对于全速运行，在网络上的单个事务中包含同步总线每个间隔中传输数据包。 某些高速设备总线间隔中允许多个事务。 在这种情况下，客户端驱动程序可以发送或接收单个请求 (URB) 中同步的数据包中的更多数据。 SuperSpeed 设备支持多个事务，并且迸发传输，每个总线间隔允许更多的字节数。 突发传输有关的详细信息，请参阅 USB 3.0 规范页 9-42。

### <a name="prerequisites"></a>系统必备

同步传输创建一个请求之前，必须具有有关等时终结点的打开的管道的信息。

使用 Windows 驱动程序模型 (WDM) 例程的客户端驱动程序具有的管道信息之一[ **USBD\_管道\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539114)结构[ **USBD\_接口\_列表\_条目**](https://msdn.microsoft.com/library/windows/hardware/ff539076)数组。 该数组中的驱动程序的上一个请求，若要选择的配置或设备中的接口，获取客户端驱动程序。

Windows 驱动程序框架 (WDF) 客户端驱动程序必须获得对框架的目标的管道对象，并调用的引用[ **WdfUsbTargetPipeGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff551142)若要获取管道中的信息[**WDF\_USB\_管道\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff553037)结构。

根据管道的信息，确定此集的信息：

-   主控制器可以向每个数据包中的管道发送多少数据。

    客户端驱动程序可以在请求中发送的数据量不能超过的最大主机控制器可以发送或从终结点接收的字节数。 指示最大字节数**MaximumPacketSize**的成员[ **USBD\_管道\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539114)和[**WDF\_USB\_管道\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff553037)结构。 USB 驱动程序堆栈集**MaximumPacketSize**值选择配置或选择接口请求过程。

    对于全速设备**MaximumPacketSize**派生自的第一个 11 位**wMaxPacketSize**终结点描述符，其指示终结点可以字节的最大数目的字段发送或接收在事务中。 对于全速设备控制器会根据总线时间间隔发送一个事务。

    在高速同步传输，主机控制器可以发送其他事务总线时间间隔内如果终结点允许它们。 由设备设置和位 12..11 中指示的其他事务数**wMaxPacketSize**。 该数字可以是 0、 1 或 2。 如果 12..11 指示 0，每 microframe 其他事务不支持终结点。 如果数量为 1，则主机控制器可以发送的其他事务 （共两个事务 / microframe）;2 表示两个其他事务 （共三个事务 / microframe）。 **MaximumPacketSize** USB 驱动程序堆栈设置的值包括可以在其他事务中发送的字节数。

    SuperSpeed 等时传输，某些值 USB\_SUPERSPEED\_终结点\_配套\_描述符 （请参阅 Usbspec.h） 非常重要。 USB 驱动程序堆栈使用这些值来计算总线间隔中的最大字节数。

    -   **Isochronous.Mult**终结点配套描述符字段。 在 SuperSpeed 同步传输 （很像高速设备） 的其他事务都称为迸发的事务。 **Mult**值表示的最大突发终结点支持的事务数。 在服务间隔中可以有最多三个突发事务 （索引 0 到 2）。
    -   **bMaxBurst**终结点配套描述符字段。 此值指示消息块的数量**wMaxPacketSize** ，可以在单次事务中出现。 突发事务中可以有最多 16 个消息块 （索引 0 到 15）。
    -   **wBytesPerInterval**指示主机可以发送或接收总线间隔中的字节总数。 即使每个总线间隔的字节数最大可计算为 (**bMaxBurst**+ 1) \* (**Mult**+ 1) \* **wMaxPacketSize**、USB 3.0 规范建议使用**wBytesPerInterval**相反值。 **WBytesPerInterval**值必须小于或等于该计算的值。

    **重要**对于客户端驱动程序中前面所述的值是仅用于提供信息。 该驱动程序必须始终使用**MaximumPacketSize**终结点描述符来确定的传输缓冲区布局的值。



-   何种频率 does 终结点发送或接收数据。

    **间隔**成员用于确定终结点发送或接收数据的频率。 设备设置值和客户端驱动程序不能更改它。 USB 驱动程序堆栈使用另一个数来确定与它将插入同步数据包到数据流的频率： 轮询周期，该类派生自**间隔**值。

    以便进行最快速度传输**间隔**和轮询期的值始终为 1; USB 驱动程序堆栈将忽略其他值。

    下表显示**间隔**和高速度和 SuperSpeed 传输的计算的轮询期：

    | Interval | 轮询期间 (2Interval-1)                      |
    |----------|---------------------------------------------------|
    | 1        | 1;数据传输总线间隔。        |
    | 2        | 2;数据传输到每个第二个总线时间间隔。 |
    | 3        | 4;数据传输到每个第四个总线时间间隔。 |
    | 4        | 8;数据传输到每个第八个总线时间间隔。 |



-   什么是对每种总线速度的数据包数的限制。

    在 URB 只能发送最多 255 个等时数据包最快速度的设备;中的高速和 SuperSpeed 设备中 URB 1024 个数据包。 在 URB 中发送的数据包数必须为每个帧中的数据包数的倍数。

    | 轮询周期 | 对于高速度/SuperSpeed 的数据包数 |
    |----------------|---------------------------------------------|
    | 1              | 8 的倍数                               |
    | 2              | 4 的倍数                               |
    | 3              | 2 的倍数                               |
    | 4              | Any                                         |



请考虑使用示例最快速度终结点**wMaxPacketSize**为 1023。 此示例中，应用程序提供的 25,575 字节的缓冲区。 该缓冲区传输需要 25 同步数据包 （25575/1023 个字符）。

请考虑具有以下特征的高速终结点的终结点描述符中所示的示例。

-   **wMaxPacketSize**为 1024。
-   位 12..11 指示两个其他事务。
-   **间隔**为 1。

客户端驱动程序选择一个配置之后, **MaximumPacketSize**等时管道指示 3,072 字节 (总事务\* **wMaxPacketSize**)。 其他事务允许客户端驱动程序来传输中每个 microframe 3,072 字节数和总 24576 一帧中的字节数。 下图显示了何种频率将同步数据包传输中的高速传输一个 microframe。

![同步传输](images/iso-packets.png)

考虑具有以下特征的终结点和 SuperSpeed 终结点配套描述符所示的示例 SuperSpeed 终结点：

-   **wMaxPacketSize**为 1024。
-   **bMaxBurst**为 15。
-   **间隔**为 1。
-   **Isochronous.Mult**为 2。
-   **wBytesPerInterval**为 45000。

在前面的示例中，即使最大字节数可计算为也是如此**wMaxPacketSize** \* (**bMaxBurst** + 1) \* (**Mult** + 1)导致 49,152 字节，设备限制为值**wBytesPerInterval**为 45000 个字节的值。 中的值也是反映**MaximumPacketSize** 45,000。 客户端驱动程序必须仅使用**MaximumPacketSize**值。 在此示例中，请求可以分为三个突发事务。 每个前两个突发事务包含的 16 区块**wMaxPacketSize**。 最后一个迸发事务包含 12 块，以便保留剩余的字节数。 下图显示的轮询间隔和通过同步 SuperSpeed 传输数据包传输的字节数。

![superspeed 等时](images/iso-packets-superspeed.png)

以下过程介绍如何构建的同步传输的请求。

1.  获取每个同步的数据包的大小。
2.  确定每个框架等时数据包数。
3.  计算同步所需保存整个传输缓冲区的数据包的数。
4.  分配[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构来描述传输的详细信息。
5.  指定每个同步的数据包，如数据包偏移量的详细信息。

有关完整的代码示例来了解发送等时转移请求，USBSAMP。

本主题中的此示例可简化 USBSAMP 实现同步传输。 该示例计算所需的传输的总数字帧。 传输缓冲区基于可以在帧中发送的数据量，分为较小块区大小的字节数。

以下过程将详细介绍前面的步骤，并显示计算和客户端驱动程序可用于生成和发送高速等时终结点的同步传输请求的例程。 该过程中使用的值基于前面所述的示例终结点特征。

<a name="instructions"></a>说明
------------

### <a href="" id="get-the-size-of-an-isochronous-packet--"></a>步骤 1:获取同步数据包的大小。

通过检查管道的确定同步数据包的大小**MaximumPacketSize**值。

对于最快速度传输同步数据包的大小是可以在一个框架中传输的字节数。 有关高速 SuperSpeed 传输的同步数据包大小为可以在一个 microframe 中传输的字节总数。 这些值所示的管道**MaximumPacketSize**。

在示例中， **MaximumPacketSize**为每个框架 （全速） 1023 字节; 3072 每 microframe （高速度） 的字节数; 每 microframe (SuperSpeed) 45000 字节数。

**请注意** **MaximumPacketSize**值指示同步数据包的最大允许的大小。 客户端驱动程序可以将每个同步的数据包的大小设置为任何值小于**MaximumPacketSize**值。



### <a href="" id="determine-the-number-of-isochronous-packets-per-frame-"></a>步骤 2:确定每个框架等时数据包数。

以便进行最快速度传输，传输一个同步数据包中的每个帧。

有关高速且 SuperSpeed 传输，此值必须派生自间隔值。 在示例中，间隔为 1。 因此，同步数据包数必须为每个框架的八个。 有关其他时间间隔值，请参阅先决条件部分中的表。

### <a href="" id="calculate-the-number-of-isochronous-packets-that-are-required-to-hold-the-entire-transfer-buffer-"></a>步骤 3:计算同步所需保存整个传输缓冲区的数据包的数。

计算同步所需传输整个缓冲区的数据包的数。 可以通过传输缓冲区的长度除以同步数据包的大小来计算此值。

在此示例中，我们假定，每个同步的数据包的大小是**MaximumPacketSize**和传输缓冲区长度是倍数**MaximumPacketSize**值。

例如，最快速度传输提供的缓冲区的 25,575 字节需要 25 同步数据包 （25575/1023 个字符）。 高速传输 24,576 大小的缓冲区被划分为八个同步数据包 (24576 /3072) 进行传输。 有关 SuperSpeed，360000 字节大小的缓冲区适合八个同步数据包 (360000/45000)。

客户端驱动程序应该验证这些要求：

-   同步数据包数必须为每个框架的数据包数的倍数。
-   同步所需进行传输的数据包的最大数目不能超过 255 个全速设备;高速或 SuperSpeed 1024 设备。

### <a href="" id="allocate-an-urb-structure-to-describe-the-details-of-the-transfer-"></a>步骤 4:分配一个 URB 结构，以描述传输的详细信息。

1.  分配[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)中非分页缓冲池的结构。

    如果您的客户端驱动程序使用 WDM 例程，该驱动程序必须调用[ **USBD\_IsochUrbAllocate** ](https://msdn.microsoft.com/library/windows/hardware/hh406231)如果您有用于 Windows 8 的 Windows Driver Kit (WDK)。 客户端驱动程序可以使用该例程以面向 Windows Vista 和更高版本的 Windows 操作系统。 如果您不具有 Windows 8 的 WDK 或如果客户端驱动程序旨在用于早期版本的操作系统，你可以通过调用分配的结构在堆栈上或在非分页缓冲池[ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520).

    WDF 客户端驱动程序可以调用[ **WdfUsbTargetDeviceCreateIsochUrb** ](https://msdn.microsoft.com/library/windows/hardware/hh439420)方法来分配内存[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构。

2.  **UrbIsochronousTransfer**的成员[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构指向[  **\_URB\_ISOCH\_传输**](https://msdn.microsoft.com/library/windows/hardware/ff540414)介绍同步传输的详细信息的结构。 初始化以下**UrbIsochronousTransfer**成员，如下所示：
    -   设置**UrbIsochronousTransfer.Hdr.Length**成员添加到 URB 的大小。 若要获取 URB 大小，请调用[**获取\_ISO\_URB\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff537144)宏，并指定数据包数。
    -   设置**UrbIsochronousTransfer.Hdr.Function**成员添加到`URB_FUNCTION_ISOCH_TRANSFER`。
    -   设置**UrbIsochronousTransfer.NumberOfPackets**成员添加到同步数据包数。
    -   设置**UrbIsochronousTransfer.PipeHandle**到与该终结点相关联的管道的不透明句柄。 请确保管道句柄使用的通用串行总线 (USB) 驱动程序堆栈的 USBD 管道句柄。

        若要获取 USBD 管道句柄，WDF 客户端驱动程序可以调用[ **WdfUsbTargetPipeWdmGetPipeHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff551162)方法并指定框架的管道对象的 WDFUSBPIPE 句柄。 WDM 客户端驱动程序必须使用相同的句柄中获得**PipeHandle**的成员[ **USBD\_管道\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539114)结构。

    -   指定传输的方向。 设置**UrbIsochronousTransfer.TransferFlags**到 USBD\_传输\_方向\_中为同步传输 （从设备读取）;USBD\_传输\_方向\_出以进行同步出传输 （写入到设备）。
    -   指定 USBD\_启动\_ISO\_传输\_中的标志，ASAP **UrbIsochronousTransfer**。TransferFlags。 该标志指示 USB 驱动程序堆栈中的下一步的相应帧发送传输。 第一次客户端驱动程序将发送此管道等时 URB，驱动程序堆栈等时在发送数据包 URB 就立即可以。 USB 驱动程序堆栈跟踪要用于该管道上的后续 URBs 下一帧。 如果在发送使用 USBD 后续同步 URB 延迟\_启动\_ISO\_传输\_ASAP 标志，驱动程序堆栈认为该 URB 将晚的部分或全部数据包并不会传输这些数据包。

        USB 驱动程序堆栈重置其 USBD\_启动\_ISO\_传输\_尽快开始帧跟踪，如果堆栈不会收到 1024年框架等时 URB 完成该管道上一 URB 后。 而不是指定 USBD\_启动\_ISO\_传输\_ASAP 标志，可以指定起始帧。 有关详细信息，请参阅“备注”部分。

    -   指定的传输缓冲区和其大小。 可以将指针设置为指向的缓冲区**UrbIsochronousTransfer.TransferBuffer**或[ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414)描述中的缓冲区**UrbIsochronousTransfer.TransferBufferMDL**。

        若要检索[ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414) WDF 客户端驱动程序可以调用为传输缓冲区[ **WdfRequestRetrieveOutputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550021)或[ **WdfRequestRetrieveInputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550016)，取决于传输的方向。

### <a href="" id="specify-the-details-of-each-isochronous-packet-in-the-transfer-"></a>步骤 5:指定在传输中的每个同步的数据包的详细信息。

USB 驱动程序堆栈分配的新[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构，它是足够大以保存每个同步的数据包，但不是包含在包中的数据有关的信息。 在中**URB**结构**UrbIsochronousTransfer.IsoPacket**成员是一个数组[ **USBD\_ISO\_数据包\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539084)描述每个同步数据包在传输中的详细信息。 数据包必须是连续的。 数组中的元素数必须为同步 URB 中指定的数据包数**UrbIsochronousTransfer.NumberOfPackets**成员。

为高速传输，数组中的每个元素将在一个 microframe 一个同步数据包相关联。 有关最快速度，每个元素与其中一个同步数据包传输在一个框架中相关联。

对于每个元素，指定每个同步数据包从请求的整个传输缓冲区开头的字节偏移量。 可以通过设置中指定该值**UrbIsochronousTransfer.IsoPacket\[我\]。偏移量**成员。 USB 驱动程序堆栈使用指定的值来跟踪要发送或接收的数据量。

**设置偏移量的最快速度传输**

有关示例，这些对象位于传输缓冲区的数组项全速运行。 在全速运行，客户端驱动程序都有一个帧传输最多 1,023 字节的一个同步数据包。 25,575 字节的传输缓冲区可以容纳 25 同步数据包，每个 1,023 字节长。 25 帧，总共不需要整个缓冲区。

``` syntax
Frame 1 IsoPacket [0].Offset = 0 (start address)
Frame 2 IsoPacket [1].Offset = 1023
Frame 3 IsoPacket [2].Offset = 2046
Frame 4 IsoPacket [3].Offset = 3069
...
Frame 25 IsoPacket [24].Offset = 24552

Total length transferred is 25,575 bytes.
```

**设置偏移量的高速传输**

对于此示例中，这些高速度是传输缓冲区的数组项。 该示例假定缓冲区 24576 字节，而客户端驱动程序有一个帧传输八个同步数据包，每个 3,072 字节长。

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

**SuperSpeed 传输设置偏移量**

对于此示例中，这是 SuperSpeed 的数组偏移量。 您可以传输一帧中最多为 45000 个字节。 传输缓冲区的大小 360000 容纳八个 microframes。

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

**UrbIsochronousTransfer.IsoPacket\[我\]**。长度成员并不表示等时 URB 每个数据包的长度。 **IsoPacket\[我\]。长度**USB 驱动程序堆栈，以指示实际的同步在从设备接收的字节数由更新传输。 有关将忽略的传输出等时，驱动程序堆栈中设置的值**IsoPacket\[我\]。长度**。

<a name="remarks"></a>备注
-------

**为传输指定起始 USB 帧数**

**UrbIsochronousTransfer.StartFrame** URB 成员指定传输开始 USB 帧数。 始终是客户端驱动程序提交 URB 的时间和 USB 驱动程序堆栈处理 URB 的时间之间的延迟。 因此，客户端驱动程序应始终指定晚于驱动程序提交 URB 时的当前帧的开始帧。 若要检索当前的帧数，客户端驱动程序可以发送 URB\_函数\_获取\_当前\_帧\_编号 USB 驱动程序堆栈的请求 ([  **\_URB\_获取\_当前\_帧\_数**](https://msdn.microsoft.com/library/windows/hardware/ff540401))。

对同步传输的绝对差异的当前帧并**StartFrame**值必须小于 USBD\_ISO\_启动\_帧\_范围。 如果 StartFrame 不适当的范围内，USB 驱动程序堆栈设置**状态**URB 标头的成员 (请参阅[  **\_URB\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff540409)) 到USBD\_状态\_错误\_启动\_帧，而丢弃整个 URB。

**StartFrame** URB 中指定的值指示在其中传输 URB 第一个同步数据包的帧号码。 后续数据包的帧号码依赖于总线速度和轮询终结点的期的值。 例如，有关完整的速度传输，第一个数据包传输在**StartFrame**; 第二个中传输数据包**StartFrame**+ 1，依此类推。 USB 驱动程序堆栈中传输同步数据包，完整的速度，在帧中的方式显示，如下所示：

``` syntax
Frame (StartFrame)   IsoPacket [0]
Frame (StartFrame+1) IsoPacket [1]
Frame (StartFrame+2) IsoPacket [2]
Frame (StartFrame+3) IsoPacket [3]
...
```

对于时间间隔值为 1 的高速设备，请更改每个第八个 microframe 帧数量。 USB 驱动程序堆栈中传输同步数据包，对高速度、 在帧中的方式显示，如下所示：

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

当 URB，驱动程序将放弃所有同步数据包中的帧号码的 URB 的 USB 驱动程序堆栈进程低于当前的帧数。 驱动程序堆栈集**状态**USBD 到每个已丢弃数据包的数据包描述符的成员\_状态\_ISO\_NA\_LATE\_USBPORT，USBD\_状态\_ISO\_不\_ACCESSED\_BY\_硬件、 或 USBD\_状态\_ISO\_不\_ACCESSED\_LATE。 即使在 URB 某些数据包将被丢弃，驱动程序堆栈尝试传输仅这些数据包的帧号码是大于当前的帧数。

一个有效的检查**StartFrame**成员是在高速传输中稍微复杂一些，因为 USB 驱动程序堆栈将每个同步数据包加载到高速的 microframe; 但是，在值**StartFrame**指 1 毫秒 （全速） 帧数，以及不 microframe。 例如，如果**StartFrame** URB 中记录的值是一个更少比当前帧时，驱动程序堆栈可以放弃多达八个数据包。 丢弃的数据包的精确数目取决于轮询周期与同步管道相关联。

## <a name="isochronous-transfer-example"></a>同步传输示例


下面的代码示例演示如何创建完整的速度、 高速度、 和 SuperSpeed 传输同步传输 URB。

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
[USB I/O 操作](usb-device-i-o.md)  



