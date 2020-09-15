---
title: 在 UMDF 中将 I/O 请求发送到常规 I/O 目标
description: 在 UMDF 中将 I/O 请求发送到常规 I/O 目标
ms.assetid: f373afa8-292a-47bb-af6f-5035287d1e8c
keywords:
- 一般 i/o 目标为 WDK UMDF，将 i/o 请求发送到
- 发送 i/o 请求 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d052196bb36327e56fc2622c9fe52093fa96f6f
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107158"
---
# <a name="sending-io-requests-to-a-general-io-target-in-umdf"></a>在 UMDF 中将 I/O 请求发送到常规 I/O 目标


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

UMDF 驱动程序可以以同步或异步方式向一般 i/o 目标发送 i/o 请求。

如果驱动程序同步发送 i/o 请求，则驱动程序线程一次发送一个请求。 线程会等待每个请求完成，然后再发送下一个请求。 此过程比异步发送 i/o 请求更简单。 如果驱动程序没有发送多个请求，并且驱动程序等待每个 i/o 请求时系统或设备性能没有降低，则驱动程序可以同步发送 i/o 请求。

如果驱动程序以异步方式发送 i/o 请求，则驱动程序线程将在请求准备就绪后发送每个请求，而无需等待之前发送的请求完成。 如果驱动程序必须在较短的时间内处理多个 i/o 请求，驱动程序可能无法等待每个请求完成，然后再发送下一个请求。 否则，驱动程序可能会丢失数据或其设备的性能，并且可能会降低整个系统的性能。

在 UMDF 驱动程序可以向 i/o 目标发送 i/o 请求之前，驱动程序必须格式化请求。 下表列出了驱动程序可以调用以格式化 i/o 请求的方法。 驱动程序可以使用这些方法来格式化驱动程序在其一个 i/o 队列或驱动程序创建的请求中收到的请求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">方法</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-formatusingcurrenttype" data-raw-source="[&lt;strong&gt;IWDFIoRequest::FormatUsingCurrentType&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-formatusingcurrenttype)"><strong>IWDFIoRequest::FormatUsingCurrentType</strong></a></p></td>
<td align="left"><p>设置驱动程序从框架收到的请求的格式，以便驱动程序可以将未修改的请求发送到目标</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForIoctl&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)"><strong>IWDFIoTarget::FormatRequestForIoctl</strong></a></p></td>
<td align="left"><p>设置设备控件请求的格式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForRead&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)"><strong>IWDFIoTarget::FormatRequestForRead</strong></a></p></td>
<td align="left"><p>格式化读取请求</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForWrite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)"><strong>IWDFIoTarget::FormatRequestForWrite</strong></a></p></td>
<td align="left"><p>格式化写入请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforflush" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForFlush&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforflush)"><strong>IWDFIoTarget2::FormatRequestForFlush</strong></a></p></td>
<td align="left"><p>格式化刷新缓冲区的请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforqueryinformation" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForQueryInformation&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforqueryinformation)"><strong>IWDFIoTarget2::FormatRequestForQueryInformation</strong></a></p></td>
<td align="left"><p>格式化请求以获取文件信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforsetinformation" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForSetInformation&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforsetinformation)"><strong>IWDFIoTarget2::FormatRequestForSetInformation</strong></a></p></td>
<td align="left"><p>格式化请求以设置文件信息。</p></td>
</tr>
</tbody>
</table>

 

若要向 i/o 目标发送 i/o 请求，驱动程序将调用 [**IWDFIoRequest：： send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send) 方法。 为了同步发送 i/o 请求，驱动程序会将 WDF \_ 请求 \_ 发送 \_ 选项 \_ 同步标志传递给 *Flags* 参数。 否则，驱动程序会以异步方式发送 i/o 请求。 如果驱动程序以异步方式发送 i/o 请求，则驱动程序通常需要在其他驱动程序完成请求时发出通知。 驱动程序应定义 [**IRequestCallbackRequestCompletion：： OnCompletion**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion) 回调函数并通过调用 [**IWDFIoRequest：： SetCompletionCallback**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback) 方法进行注册。 有关详细信息，请参阅 [完成 I/o 请求](completing-i-o-requests.md)。

调用 **IWDFIoRequest：： send** 发送 i/o 请求的驱动程序稍后可通过调用 [**IWDFIoRequest：： CancelSentRequest**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-cancelsentrequest) 方法尝试取消请求。 如果驱动程序取消了驱动程序从框架收到的 i/o 请求，则驱动程序必须始终通过调用 [**IWDFIoRequest：： complete**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete) 或 [**IWDFIoRequest：： CompleteWithInformation**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation) 方法来完成请求，并将 *COMPLETIONSTATUS* 参数设置为 "状态已 \_ 取消"。 如果驱动程序创建了 request 对象，则驱动程序将调用 [**IWDFObject：:D eletewdfobject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) ，而不是完成请求。

