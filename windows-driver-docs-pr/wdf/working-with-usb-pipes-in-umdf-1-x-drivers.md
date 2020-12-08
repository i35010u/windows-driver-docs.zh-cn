---
title: 在 UMDF 1.x 驱动程序中使用 USB 管道
description: 在 UMDF 1.x 驱动程序中使用 USB 管道
keywords:
- UMDF WDK，USB 管道
- User-Mode Driver Framework WDK，USB 管道
- 用户模式驱动程序 WDK UMDF，USB 管道
- USB 管道 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0dbe3362ac99a6247ab658053dcd3666f5a37ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833921"
---
# <a name="working-with-usb-pipes-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中使用 USB 管道


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架将 USB 接口中的每个管道表示为框架 USB 管道对象。 当驱动程序配置 USB 设备时，框架会为每个选定接口中的每个管道创建一个框架 USB 管道对象。 通过管道对象方法，驱动程序可以：

-   [获取管道信息](#obtaining-umdf-usb-pipe-information)。

-   [从管道读取](#reading-from-a-umdf-usb-pipe)。

-   [写入管道](#writing-to-a-umdf-usb-pipe)。

-   [停止、刷新或重置管道](#stopping-flushing)。

-   [设置管道策略](#setting-pipe-policy)。

-   [处理管道错误](#handling-pipe-errors)。

### <a name="obtaining-umdf-usb-pipe-information"></a>获取 UMDF-USB 管道信息

在 UMDF 驱动程序调用 [**IWDFUsbInterface：： RetrieveUsbPipeObject**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-retrieveusbpipeobject) 方法以获取指向 usb 管道对象的 [IWDFUsbTargetPipe](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe) 接口的指针后，驱动程序可以调用 usb 管道对象定义的以下方法来获取有关 usb 管道的信息：

<a href="" id="iwdfusbtargetpipe--getinformation"></a>[**IWDFUsbTargetPipe：： GetInformation**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)  
检索有关 USB 管道及其终结点的信息。

<a href="" id="iwdfusbtargetpipe--gettype"></a>[**IWDFUsbTargetPipe：： GetType**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-gettype)  
返回 USB 管道的类型。

<a href="" id="iwdfusbtargetpipe--isinendpoint"></a>[**IWDFUsbTargetPipe::IsInEndPoint**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-isinendpoint)  
确定 USB 管道是否连接到输入终结点。

<a href="" id="iwdfusbtargetpipe--isoutendpoint"></a>[**IWDFUsbTargetPipe::IsOutEndPoint**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-isoutendpoint)  
确定 USB 管道是否连接到输出终结点。

<a href="" id="iwdfusbtargetpipe--retrievepipepolicy"></a>[**IWDFUsbTargetPipe::RetrievePipePolicy**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-retrievepipepolicy)  
检索 WinUsb 管道策略。

### <a name="reading-from-a-umdf-usb-pipe"></a>从 UMDF USB 管道读取

若要从 USB 输入管道中读取数据，驱动程序可以使用以下两种方法中的 (一种或两种) ：

-   同步读取数据。

    若要从 USB 输入管道同步读取数据，UMDF 驱动程序首先会调用 [**IWDFIoTarget：： FormatRequestForRead**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread) 方法来生成读取请求。 然后，驱动程序将调用 [**IWDFIoRequest：： send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send) 方法，并指定 WDF \_ 请求 \_ 发送 \_ 选项 \_ 同步标志，以同步发送请求。

-   异步读取数据。

    若要从 USB 输入管道异步读取数据，UMDF 驱动程序首先会调用 [**IWDFIoTarget：： FormatRequestForRead**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread) 方法来生成读取请求。 然后，驱动程序将调用 [**IWDFIoRequest：： send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send) 方法，而不指定 WDF \_ 请求 \_ 发送 \_ 选项 \_ 同步标志。

-   同步和持续地读取数据。

    *连续的读取器* 是一个框架提供的机制，可确保读取请求始终可用于 USB 管道。 此机制保证驱动程序始终可以从提供异步、未经请求的输入流的设备接收数据。 例如，网络接口卡 (NIC 的驱动程序) 可能使用连续读取器来接收输入数据。

    若要为输入管道配置连续读取器，驱动程序的 [**IPnpCallbackHardware：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware) 回调函数必须调用 [**IWDFUsbTargetPipe2：： ConfigureContinuousReader**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader) 方法。 此方法将一组读取请求排队给设备的 i/o 目标。

    此外，驱动程序的 [**IPnpCallback：： OnD0Entry**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry) 回调函数必须调用 [**IWDFIoTargetStateManagement：： start**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start) 来启动持续读取器，驱动程序的 [**IPnpCallback：： OnD0Exit**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit) 回调函数必须调用 [**IWDFIoTargetStateManagement：： stop**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop) 来停止连续读取器。

    每次从设备获取数据时，i/o 目标将完成读取请求，并且框架将调用以下两个回调函数之一： [**IUsbTargetPipeContinuousReaderCallbackReadComplete：： OnReaderCompletion**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete-onreadercompletion) （如果 i/o 目标成功读取数据）或 [**IUsbTargetPipeContinuousReaderCallbackReadersFailed：： OnReaderFailure**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed-onreaderfailure) （如果 i/o 目标报告错误）。

    驱动程序调用 [**IWDFUsbTargetPipe2：： ConfigureContinuousReader**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)后，除非调用了驱动程序的 [**IUsbTargetPipeContinuousReaderCallbackReadersFailed：： OnReaderFailure**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed-onreaderfailure)回调函数并返回 **FALSE**，否则驱动程序无法使用 [**IWDFIoRequest：： send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)向管道发送 i/o 请求。

    在 UMDF 版本1.9 及更高版本中支持连续读取器。

### <a name="writing-to-a-umdf-usb-pipe"></a>写入 UMDF USB 管道

若要将数据写入 USB 输出管道，UMDF 驱动程序可以首先调用 [**IWDFIoTarget：： FormatRequestForWrite**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite) 方法以生成写入请求。 然后，驱动程序可以调用 [**IWDFIoRequest：： send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send) 方法以异步方式发送请求。

### <a name="stopping-flushing-and-resetting-a-umdf-usb-pipe"></a><a href="" id="stopping-flushing"></a>停止、刷新和重置 UMDF-USB 管道

UMDF 驱动程序可以调用以下方法来停止、刷新或重置 USB 管道：

<a href="" id="iwdfusbtargetpipe--abort"></a>[**IWDFUsbTargetPipe：： Abort**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-abort)  
同步发送请求以停止 USB 管道上的所有等待传输。

<a href="" id="iwdfusbtargetpipe--flush"></a>[**IWDFUsbTargetPipe：： Flush**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-flush)  
当设备返回的数据多于客户端请求的数据时，同步发送请求以放弃 WinUsb 保存的所有数据。

<a href="" id="iwdfusbtargetpipe--reset"></a>[**IWDFUsbTargetPipe：： Reset**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-reset)  
同步发送请求以重置 USB 管道。

### <a name="setting-policy-for-a-umdf-usb-pipe"></a><a href="" id="setting-pipe-policy"></a>为 UMDF USB 管道设置策略

UMDF 驱动程序可以调用 [**IWDFUsbTargetPipe：： SetPipePolicy**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-setpipepolicy) 方法来控制 WINUSB 用于 USB 管道 (的行为，例如超时、处理短数据包和其他) 的行为。

### <a name="handling-pipe-errors"></a>处理管道错误

如果驱动程序的 USB 目标 [完成](completing-i-o-requests.md) 的 i/o 请求带有错误状态值，则驱动程序应执行以下操作：

1.  调用 [**IWDFIoTargetStateManagement：： Stop**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop) 并设置 **WdfIoTargetCancelSentIo** 标志。 如果目标尚未完成请求，此调用将停止管道并取消驱动程序已发送到 USB 目标的任何其他 i/o 请求。

2.  调用 [**IWDFUsbTargetPipe：： abort**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-abort) 将中止请求发送到管道。

3.  调用 [**IWDFUsbTargetPipe：： reset**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-reset) 将重置请求发送到管道。

4.  调用 [**IWDFIoTargetStateManagement：： Start**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start) 以重新启动管道。

5.  重新发送失败的 i/o 请求，以及按照失败请求的所有 i/o 请求。

 

