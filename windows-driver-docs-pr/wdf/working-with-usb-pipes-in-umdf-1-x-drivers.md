---
title: 在 UMDF 1.x 驱动程序中使用 USB 管道
description: 在 UMDF 1.x 驱动程序中使用 USB 管道
ms.assetid: face26da-fa79-4d32-8ad1-9e8022bb23b3
keywords:
- UMDF WDK，USB 管道
- 用户模式驱动程序框架 WDK，USB 管道
- 用户模式驱动程序 WDK UMDF，USB 管道
- USB 通过管道传递 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a27a7841c407462bcc26581e52ef76269d57422
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564707"
---
# <a name="working-with-usb-pipes-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中使用 USB 管道


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

框架为框架 USB 管道对象表示 USB 接口中的每个管道。 时驱动程序会在配置 USB 设备，框架将创建在每个所选接口中每个管道 framework USB 管道对象。 管道对象方法启用到驱动程序：

-   [获取管道的信息](#obtaining-umdf-usb-pipe-information)。

-   [从管道读取](#reading-from-a-umdf-usb-pipe)。

-   [向管道写入](#writing-to-a-umdf-usb-pipe)。

-   [停止、 刷新，或重置管道](#stopping-flushing)。

-   [设置管道策略](#setting-pipe-policy)。

-   [处理管道错误](#handling-pipe-errors)。

### <a name="obtaining-umdf-usb-pipe-information"></a>获取 UMDF USB 管道的信息

UMDF 驱动程序调用后[ **IWDFUsbInterface::RetrieveUsbPipeObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560339)方法来获取一个指向[IWDFUsbTargetPipe](https://msdn.microsoft.com/library/windows/hardware/ff560391) USB 管道对象的接口驱动程序可以调用 USB 管道对象定义的以下方法用于获取有关 USB 管道的信息：

<a href="" id="iwdfusbtargetpipe--getinformation"></a>[**IWDFUsbTargetPipe::GetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff560403)  
检索有关 USB 管道和其终结点的信息。

<a href="" id="iwdfusbtargetpipe--gettype"></a>[**IWDFUsbTargetPipe::GetType**](https://msdn.microsoft.com/library/windows/hardware/ff560406)  
返回一个 USB 管道的类型。

<a href="" id="iwdfusbtargetpipe--isinendpoint"></a>[**IWDFUsbTargetPipe::IsInEndPoint**](https://msdn.microsoft.com/library/windows/hardware/ff560410)  
确定 USB 管道是否已连接到的输入终结点。

<a href="" id="iwdfusbtargetpipe--isoutendpoint"></a>[**IWDFUsbTargetPipe::IsOutEndPoint**](https://msdn.microsoft.com/library/windows/hardware/ff560414)  
确定 USB 管道是否已连接到的输出终结点。

<a href="" id="iwdfusbtargetpipe--retrievepipepolicy"></a>[**IWDFUsbTargetPipe::RetrievePipePolicy**](https://msdn.microsoft.com/library/windows/hardware/ff560418)  
检索 WinUsb 管道策略。

### <a name="reading-from-a-umdf-usb-pipe"></a>读取 UMDF USB 管道

若要从 USB 输入管道中读取数据，您的驱动程序可以使用任一 （或两者） 的以下技术：

-   以同步方式读取数据。

    若要以同步方式从 USB 输入管道读取数据，UMDF 驱动程序首先调用[ **IWDFIoTarget::FormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559233)方法生成的读取的请求。 然后驱动程序调用[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)方法，指定 WDF\_请求\_发送\_选项\_同步标志，以发送请求同步。

-   以异步方式读取数据。

    若要从 USB 输入管道以异步方式读取数据，UMDF 驱动程序首先调用[ **IWDFIoTarget::FormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559233)方法生成的读取的请求。 然后驱动程序调用[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)方法而无需指定 WDF\_请求\_发送\_选项\_同步标志。

-   以同步方式持续地读取数据。

    一个*连续读取器*是一种框架提供的机制，可确保读取的请求都可供 USB 管道。 此机制可确保该驱动程序始终准备好接收来自提供异步的、 未经请求的输入的流的设备的数据。 例如，网络接口卡 (NIC) 的驱动程序可能使用连续读取器接收输入的数据。

    若要配置用于输入管道，该驱动程序的连续阅读器[ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)回调函数必须调用[ **IWDFUsbTargetPipe2:: ConfigureContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff560395)方法。 此方法进行排队读取请求到设备的 I/O 目标的集。

    此外，驱动程序[ **IPnpCallback::OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799)回调函数必须调用[ **IWDFIoTargetStateManagement::Start** ](https://msdn.microsoft.com/library/windows/hardware/ff559213)启动持续读取器和驱动程序的[ **IPnpCallback::OnD0Exit** ](https://msdn.microsoft.com/library/windows/hardware/ff556803)回调函数必须调用[ **IWDFIoTargetStateManagement::Stop**](https://msdn.microsoft.com/library/windows/hardware/ff559217)停止持续读取器。

    数据是从设备中，每次 I/O 目标将完成的读取的请求和框架将调用两个回调函数之一：[**IUsbTargetPipeContinuousReaderCallbackReadComplete::OnReaderCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556910)如果 I/O 目标成功读取数据，或[ **IUsbTargetPipeContinuousReaderCallbackReadersFailed::OnReaderFailure** ](https://msdn.microsoft.com/library/windows/hardware/ff556915)如果 I/O 目标报告错误。

    驱动程序已调用后[ **IWDFUsbTargetPipe2::ConfigureContinuousReader**](https://msdn.microsoft.com/library/windows/hardware/ff560395)，则驱动程序不能使用[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)若要将输入/输出请求发送到管道，除非驱动程序的[ **IUsbTargetPipeContinuousReaderCallbackReadersFailed::OnReaderFailure** ](https://msdn.microsoft.com/library/windows/hardware/ff556915)回调函数调用，并返回**FALSE**。

    连续的读者都支持在 UMDF 版本 1.9 及更高版本。

### <a name="writing-to-a-umdf-usb-pipe"></a>写入 UMDF USB 管道

将数据写入 USB 输出管道，UMDF 驱动程序可以首先调用[ **IWDFIoTarget::FormatRequestForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559236)方法以生成写入请求。 然后，驱动程序可以调用[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)方法以异步方式发送请求。

### <a href="" id="stopping-flushing"></a>停止刷新，和重置 UMDF USB 管道

UMDF 驱动程序可以调用以下方法来停止、 刷新，或重置 USB 管道：

<a href="" id="iwdfusbtargetpipe--abort"></a>[**IWDFUsbTargetPipe::Abort**](https://msdn.microsoft.com/library/windows/hardware/ff560397)  
以同步方式发送请求以停止 USB 管道上的所有挂起的传输。

<a href="" id="iwdfusbtargetpipe--flush"></a>[**IWDFUsbTargetPipe::Flush**](https://msdn.microsoft.com/library/windows/hardware/ff560400)  
以同步方式发送请求以放弃 WinUsb 保存时设备所返回的数据比客户端请求的任何数据。

<a href="" id="iwdfusbtargetpipe--reset"></a>[**IWDFUsbTargetPipe::Reset**](https://msdn.microsoft.com/library/windows/hardware/ff560416)  
以同步方式发送请求以重置 USB 管道。

### <a href="" id="setting-pipe-policy"></a>对于 UMDF USB 管道设置策略

UMDF 驱动程序可以调用[ **IWDFUsbTargetPipe::SetPipePolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff560421)方法来控制由 USB 管道 （例如，超时值、 处理短数据包和其他行为） WinUsb 的行为.

### <a name="handling-pipe-errors"></a>处理管道错误

如果您的驱动程序的 USB 目标[完成](completing-i-o-requests.md)I/O 请求并显示错误状态值，您的驱动程序应执行以下操作：

1.  调用[ **IWDFIoTargetStateManagement::Stop** ](https://msdn.microsoft.com/library/windows/hardware/ff559217)与**WdfIoTargetCancelSentIo**标志设置。 此调用停止管道，并取消所有其他的 I/O 请求驱动程序已发送到的 USB 目标值，如果目标未完成请求。

2.  调用[ **IWDFUsbTargetPipe::Abort** ](https://msdn.microsoft.com/library/windows/hardware/ff560397)将中止请求发送到管道。

3.  调用[ **IWDFUsbTargetPipe::Reset** ](https://msdn.microsoft.com/library/windows/hardware/ff560416)将重置请求发送到管道。

4.  调用[ **IWDFIoTargetStateManagement::Start** ](https://msdn.microsoft.com/library/windows/hardware/ff559213)重启管道。

5.  重新发送的 I/O 请求的失败，并后接失败的请求的所有 I/O 请求。

 

 





