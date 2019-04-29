---
title: 使用 USB 管道
description: 使用 USB 管道
ms.assetid: d5422ff2-de1e-4a77-8b3c-0b2917b1d9ca
keywords:
- framework 对象 WDK KMDF，USB 管道对象
- USB 通过管道传递 WDK KMDF
- 管道对象 WDK KMDF
- USB I/O 面向 WDK KMDF，USB 管道
- 持续读取器 WDK USB
- 重置管道 WDK KMDF
- 发送 URBs WDK KMDF
- USB 请求阻止 WDK KMDF
- URBs WDK KMDF
- 正在停止管道 WDK KMDF
- 写入管道 WDK KMDF
- 从管道 WDK KMDF 读取
- 输入通过管道传递 WDK KMDF
- 输出通过管道传递 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f54a3ae3c4b4f8840a189f0cbebfe418673058e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361959"
---
# <a name="working-with-usb-pipes"></a>使用 USB 管道


框架为框架 USB 管道对象表示 USB 接口中的每个管道。 当驱动程序[会在配置 USB 设备](working-with-usb-devices.md#selecting-a-device-configuration)，框架在每个所选接口中创建每个管道的 framework USB 管道对象。 管道对象方法启用驱动程序即可执行以下操作：

-   [获取管道的信息。](#obtaining-pipe-information)

-   [从管道读取。](#reading-from-a-pipe)

-   [向管道写入。](#writing-to-a-pipe)

-   [停止或重置管道。](#stopping-and-resetting-a-pipe)

-   [将 URB 发送到管道。](#sending-a-urb-to-a-pipe)

### <a href="" id="obtaining-pipe-information"></a> 获取管道的信息

在调用[ **WdfUsbInterfaceGetConfiguredPipe** ](https://msdn.microsoft.com/library/windows/hardware/ff550057)若要获取 framework USB 管道对象的句柄，您的驱动程序可以调用 USB 管道对象定义的以下方法用于获取有关 USB 管道的信息：

<a href="" id="---------wdfusbtargetpipegetiotarget--------"></a>[**WdfUsbTargetPipeGetIoTarget**](https://msdn.microsoft.com/library/windows/hardware/ff551146)  
返回的句柄与 USB 管道相关联的 I/O 目标对象。 该驱动程序可以将传递到此句柄[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)。

<a href="" id="---------wdfusbtargetpipegetinformation--------"></a>[**WdfUsbTargetPipeGetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff551142)  
检索有关 USB 管道和其终结点的信息。

<a href="" id="---------wdfusbtargetpipegettype--------"></a>[**WdfUsbTargetPipeGetType**](https://msdn.microsoft.com/library/windows/hardware/ff551148)  
返回一个 USB 管道的类型。

<a href="" id="---------wdfusbtargetpipeisinendpoint--------"></a>[**WdfUsbTargetPipeIsInEndpoint**](https://msdn.microsoft.com/library/windows/hardware/ff551151)  
确定 USB 管道是否已连接到的输入终结点。

<a href="" id="---------wdfusbtargetpipeisoutendpoint--------"></a>[**WdfUsbTargetPipeIsOutEndpoint**](https://msdn.microsoft.com/library/windows/hardware/ff551153)  
确定 USB 管道是否已连接到的输出终结点。

<a href="" id="---------wdf-usb-pipe-direction-in--------"></a>[**WDF\_USB\_管道\_方向\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff553027)  
确定 USB 终结点是否为输入终结点。

<a href="" id="---------wdf-usb-pipe-direction-out--------"></a>[**WDF\_USB\_管道\_方向\_出**](https://msdn.microsoft.com/library/windows/hardware/ff553032)  
确定 USB 终结点是否为输出终结点。

有关相关信息，请参阅[如何枚举 USB 管道](https://msdn.microsoft.com/library/windows/hardware/hh968306)。

### <a href="" id="reading-from-a-pipe"></a> 从管道读取

若要从 USB 输入管道中读取数据，您的驱动程序可以使用任何 （或全部） 以下三个方法：

-   以同步方式读取数据

    若要从 USB 输入管道以同步方式读取数据，您的驱动程序可以调用[ **WdfUsbTargetPipeReadSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551155)方法。 此方法生成和发送的读取的请求，并返回 I/O 操作完成后。

-   以异步方式读取数据

    若要从 USB 输入管道以异步方式读取数据，您的驱动程序可以调用[ **WdfUsbTargetPipeFormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff551136)方法生成的读取的请求。 然后，驱动程序可以调用[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)发送请求以异步方式 （或以同步方式）。

-   以异步方式持续地读取数据

    一个*连续读取器*是框架提供的机制，用于确保读取的请求都可供 USB 管道。 此机制可确保始终将准备好接收数据，提供异步的、 未经请求的输入的流的设备驱动程序。 例如，网络接口卡 (NIC) 的驱动程序可能使用连续读取器接收输入的数据。

    若要配置用于输入管道，该驱动程序的连续阅读器[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数必须调用[ **WdfUsbTargetPipeConfigContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff551130)方法。 此方法进行排队读取请求到设备的 I/O 目标的集。

    此外，驱动程序[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)回调函数必须调用[ **WdfIoTargetStart** ](https://msdn.microsoft.com/library/windows/hardware/ff548677)启动持续读取器和驱动程序的[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数必须调用[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)停止持续读取器。

    数据是从设备中，每次 I/O 目标将完成的读取的请求和框架将调用两个回调函数之一：[*EvtUsbTargetPipeReadComplete*](https://msdn.microsoft.com/library/windows/hardware/ff541826)，如果 I/O 目标成功读取数据，或[ *EvtUsbTargetPipeReadersFailed*](https://msdn.microsoft.com/library/windows/hardware/ff541832)，如果 I/O 目标报告错误。

    如果未提供可选[ *EvtUsbTargetPipeReadersFailed* ](https://msdn.microsoft.com/library/windows/hardware/ff541832)回调，该框架读取尝试失败的响应发送另一个读取的请求。 因此如果总线在其中它将不会接受读取的状态，框架将不断发送新请求，若要从此失败读取。

    驱动程序已调用后[ **WdfUsbTargetPipeConfigContinuousReader**](https://msdn.microsoft.com/library/windows/hardware/ff551130)，则驱动程序不能使用[ **WdfUsbTargetPipeReadSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551155)或[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)若要将输入/输出请求发送到管道，除非驱动程序的[ *EvtUsbTargetPipeReadersFailed* ](https://msdn.microsoft.com/library/windows/hardware/ff541832)回调函数调用，并返回**FALSE**。

默认情况下，框架将报告错误，如果您的驱动程序指定读取的缓冲区不是管道的最大数据包大小的倍数。 您的驱动程序可以调用[ **WdfUsbTargetPipeSetNoMaximumPacketSizeCheck** ](https://msdn.microsoft.com/library/windows/hardware/ff551160)若要禁用此测试读取的缓冲区大小。

有关相关信息，请参阅：

-   [如何发送 USB 大容量传输请求](https://msdn.microsoft.com/library/windows/hardware/ff539199)
-   [如何将数据传输到 USB 等时终结点](https://msdn.microsoft.com/library/windows/hardware/hh406225)
-   [如何使用来从 USB 管道读取数据的连续读取器](https://msdn.microsoft.com/library/windows/hardware/hh968308)

### <a href="" id="writing-to-a-pipe"></a> 向管道写入

将数据写入 USB 输出管道，您的驱动程序可以使用其中一个 （或两者） 的以下技术：

-   以同步方式将数据写入

    若要向 USB 输出管道以同步方式写入数据，您的驱动程序可以调用[ **WdfUsbTargetPipeWriteSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551163)方法。 此方法生成，并将写入请求，并返回 I/O 操作完成后。

-   以异步方式写入数据

    若要向 USB 输入管道以异步方式写入数据，您的驱动程序可以调用[ **WdfUsbTargetPipeFormatRequestForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff551141)方法以生成写入请求。 然后，驱动程序可以调用[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)来以异步方式发送请求。

有关相关信息，请参阅[如何发送 USB 大容量传输请求](https://msdn.microsoft.com/library/windows/hardware/ff539199)。

### <a href="" id="stopping-and-resetting-a-pipe"></a> 停止和重置管道

您的驱动程序可以调用以下方法来停止或重置 USB 管道：

<a href="" id="---------wdfusbtargetpipeabortsynchronously--------"></a>[**WdfUsbTargetPipeAbortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551129)  
以同步方式发送请求以停止 USB 管道。

<a href="" id="---------wdfusbtargetpipeformatrequestforabort--------"></a>[**WdfUsbTargetPipeFormatRequestForAbort**](https://msdn.microsoft.com/library/windows/hardware/ff551132)  
设置格式的请求以停止 USB 管道。 该驱动程序可以调用[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)以同步或异步发送请求。

<a href="" id="---------wdfusbtargetpiperesetsynchronously--------"></a>[**WdfUsbTargetPipeResetSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551156)  
以同步方式发送请求以重置 USB 管道。

<a href="" id="---------wdfusbtargetpipeformatrequestforreset--------"></a>[**WdfUsbTargetPipeFormatRequestForReset**](https://msdn.microsoft.com/library/windows/hardware/ff551138)  
设置格式的请求重置 USB 管道。 该驱动程序必须调用[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)以同步或异步发送请求。

如果您的驱动程序的 USB 目标[完成](completing-i-o-requests.md)I/O 请求并显示错误状态值，您的驱动程序应执行以下操作：

1.  停止管道，并取消任何额外的 I/O 请求的驱动程序发送到的 USB 目标值，如果目标未完成请求。

    调用[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)与[ **WdfIoTargetCancelSentIo** ](https://msdn.microsoft.com/library/windows/hardware/ff552388)标志设置。

2.  以同步方式将中止请求发送到管道。

    调用[ **WdfUsbTargetPipeAbortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551129)，或调用[ **WdfUsbTargetPipeFormatRequestForAbort** ](https://msdn.microsoft.com/library/windows/hardware/ff551132)跟[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)与[ **WDF\_请求\_发送\_选项\_同步**](https://msdn.microsoft.com/library/windows/hardware/ff552491)标志设置。

3.  以同步方式将重置请求发送到管道。

    调用[ **WdfUsbTargetPipeResetSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551156)，或调用[ **WdfUsbTargetPipeFormatRequestForReset** ](https://msdn.microsoft.com/library/windows/hardware/ff551138)跟[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)与[ **WDF\_请求\_发送\_选项\_同步**](https://msdn.microsoft.com/library/windows/hardware/ff552491)标志设置。

4.  重新启动管道。

    调用[ **WdfIoTargetStart**](https://msdn.microsoft.com/library/windows/hardware/ff548677)。

5.  重新发送的 I/O 请求的失败，并后接失败的请求的所有 I/O 请求。

后大量的多个故障，则驱动程序应尝试通过执行以下操作重置的 USB 端口：

1.  停止所有活动的管道，并取消该驱动程序已发送到每个管道的 USB 目标时，如果目标尚未完成其任何其他 I/O 请求。

    对于每个活动的管道，调用[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)与[ **WdfIoTargetCancelSentIo** ](https://msdn.microsoft.com/library/windows/hardware/ff552388)标志设置。

2.  以同步方式发送请求以重置的 USB 端口。

    调用[ **WdfUsbTargetDeviceResetPortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550097)。

3.  重新启动管道。

    调用[ **WdfIoTargetStart** ](https://msdn.microsoft.com/library/windows/hardware/ff548677)驱动程序停止每个管道。

4.  重新发送最后一个 I/O 请求失败，并后接失败的请求的所有 I/O 请求。

有关相关信息，请参阅[如何从 USB 管道错误中恢复](https://msdn.microsoft.com/library/windows/hardware/hh968307)。

### <a href="" id="sending-a-urb-to-a-pipe"></a> 发送到管道 URB

如果 KMDF 驱动程序通过发送包含 URBs 的 I/O 请求使用 USB 管道进行通信，该驱动程序可以调用以下方法：

<a href="" id="---------wdfusbtargetpipesendurbsynchronously--kmdf-only-"></a>[**WdfUsbTargetPipeSendUrbSynchronously (仅适用于 KMDF)**](https://msdn.microsoft.com/library/windows/hardware/ff551158)  
以同步方式将发送包含 URB 的 I/O 请求。

<a href="" id="---------wdfusbtargetpipeformatrequestforurb--kmdf-only-"></a>[**WdfUsbTargetPipeFormatRequestForUrb (仅适用于 KMDF)**](https://msdn.microsoft.com/library/windows/hardware/ff551139)  
设置包含 URB 的 I/O 请求的格式。 该驱动程序可以调用[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)以同步或异步发送请求。

<a href="" id="---------wdfusbtargetpipewdmgetpipehandle--kmdf-only-"></a>[**WdfUsbTargetPipeWdmGetPipeHandle (仅适用于 KMDF)**](https://msdn.microsoft.com/library/windows/hardware/ff551162)  
返回设备的 USBD 管道句柄。 某些 URBs 要求此句柄。

 

 





