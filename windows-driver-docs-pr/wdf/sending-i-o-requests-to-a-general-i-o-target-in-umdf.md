---
title: 在 UMDF 中将 I/O 请求发送到常规 I/O 目标
description: 在 UMDF 中将 I/O 请求发送到常规 I/O 目标
ms.assetid: f373afa8-292a-47bb-af6f-5035287d1e8c
keywords:
- 常规 I/O 面向 WDK UMDF，I/O 将请求发送到
- 发送 I/O 请求 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 217e10ce4b5a2ff3e15f19a8069bf24ddb511a9b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376213"
---
# <a name="sending-io-requests-to-a-general-io-target-in-umdf"></a>在 UMDF 中将 I/O 请求发送到常规 I/O 目标


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF 驱动程序可以将 I/O 请求发送到常规 I/O 目标同步或异步。

如果驱动程序将以同步方式发送的 I/O 请求，驱动程序线程一次发送一个请求。 为每个请求才能完成再发送下一个等待线程。 此过程是以异步方式发送的 I/O 请求比简单得多。 如果它不会发送多个请求，并且系统或设备的性能不会减少驱动程序等待每个 I/O 请求时，驱动程序可以以同步方式发送 I/O 请求。

如果驱动程序以异步方式发送的 I/O 请求，驱动程序线程将发送每个请求，请求一旦准备好发送，而无需等待以前发送的请求数完成。 如果驱动程序必须处理多个 I/O 请求以短的时间段，该驱动程序可能不能等待每个请求发送的下一个请求之前完成。 否则为该驱动程序可能会丢失数据或其设备以及可能的整个系统的性能可能会降低。

UMDF 驱动程序可以将 I/O 请求发送到的 I/O 目标之前，该驱动程序必须设置请求的格式。 下表列出了该驱动程序可以调用格式 I/O 请求的方法。 该驱动程序可以使用这些方法以设置其 I/O 队列之一接收该驱动程序或驱动程序创建的请求的格式。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">方法</th>
<th align="left">用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-formatusingcurrenttype" data-raw-source="[&lt;strong&gt;IWDFIoRequest::FormatUsingCurrentType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-formatusingcurrenttype)"><strong>IWDFIoRequest::FormatUsingCurrentType</strong></a></p></td>
<td align="left"><p>格式框架从收到该驱动程序，以便该驱动程序发送请求，以未经修改的目标的请求</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForIoctl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)"><strong>IWDFIoTarget::FormatRequestForIoctl</strong></a></p></td>
<td align="left"><p>设置设备控制请求的格式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForRead&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)"><strong>IWDFIoTarget::FormatRequestForRead</strong></a></p></td>
<td align="left"><p>设置格式的读取的请求</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForWrite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)"><strong>IWDFIoTarget::FormatRequestForWrite</strong></a></p></td>
<td align="left"><p>格式写入请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforflush" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForFlush&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforflush)"><strong>IWDFIoTarget2::FormatRequestForFlush</strong></a></p></td>
<td align="left"><p>设置刷新缓冲区的请求的格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforqueryinformation" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForQueryInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforqueryinformation)"><strong>IWDFIoTarget2::FormatRequestForQueryInformation</strong></a></p></td>
<td align="left"><p>格式化请求以获取文件信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforsetinformation" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForSetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforsetinformation)"><strong>IWDFIoTarget2::FormatRequestForSetInformation</strong></a></p></td>
<td align="left"><p>格式设置文件信息的请求。</p></td>
</tr>
</tbody>
</table>

 

若要将 I/O 请求发送到 I/O 目标，该驱动程序调用[ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)方法。 若要以同步方式发送的 I/O 请求，驱动程序通过了 WDF\_请求\_发送\_选项\_同步一个标记，用于*标志*参数。 否则，该驱动程序将以异步方式发送 I/O 请求。 如果驱动程序以异步方式发送的 I/O 请求，驱动程序将在另一个驱动程序完成请求时通常需要通知。 该驱动程序应定义[ **IRequestCallbackRequestCompletion::OnCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)回调函数，并通过调用注册[ **IWDFIoRequest::SetCompletionCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)方法。 有关详细信息，请参阅[完成 I/O 请求](completing-i-o-requests.md)。

调用的驱动程序**IWDFIoRequest::Send**将发送一个 I/O 请求可以尝试取消该请求更高版本通过调用[ **IWDFIoRequest::CancelSentRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-cancelsentrequest)方法。 如果该驱动程序取消 I/O 请求，从框架接收到的驱动程序，该驱动程序必须始终通过调用完成的请求[ **IWDFIoRequest::Complete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-complete)或[ **IWDFIoRequest::CompleteWithInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)方法替换*CompletionStatus*参数设置为状态\_已取消。 如果该驱动程序创建了请求对象，该驱动程序会调用[ **IWDFObject::DeleteWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)而无需完成请求。

 

 





