---
title: 异步发送 I/O 请求
description: 异步发送 I/O 请求
ms.assetid: 9f6fb85e-96aa-4945-8c8a-13277beff140
keywords:
- 常规 I/O 面向 WDK KMDF，I/O 将请求发送到
- 发送 I/O 请求 WDK KMDF
- 发送的 I/O 请求 WDK KMDF，异步
- 以异步方式发送 I/O 请求 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8de7d75b5b213bddc0a6cc9650f70241696f720
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376219"
---
# <a name="sending-io-requests-asynchronously"></a>异步发送 I/O 请求





可以以异步方式将 I/O 请求发送到的 I/O 目标之前，必须设置请求的格式。 下表列出了您的驱动程序可以调用格式 I/O 请求的 I/O 目标对象方法。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForRead&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread)"><strong>WdfIoTargetFormatRequestForRead</strong></a></p></td>
<td align="left"><p>设置格式的读取的请求</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForWrite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite)"><strong>WdfIoTargetFormatRequestForWrite</strong></a></p></td>
<td align="left"><p>格式写入请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforioctl" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForIoctl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforioctl)"><strong>WdfIoTargetFormatRequestForIoctl</strong></a></p></td>
<td align="left"><p>设置设备控制请求的格式</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl)"><strong>WdfIoTargetFormatRequestForInternalIoctl</strong></a></p></td>
<td align="left"><p>设置内部设备控制请求的格式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctlOthers&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers)"><strong>WdfIoTargetFormatRequestForInternalIoctlOthers</strong></a></p></td>
<td align="left"><p>设置非标准的内部设备控制请求的格式</p></td>
</tr>
</tbody>
</table>

 

若要以异步方式发送的 I/O 请求，您的驱动程序必须：

1.  设置请求的格式。

    使用要设置格式时，将要求的上一表中列出的方法之一。 有关如何使用这些方法的详细信息，请参阅这些方法的参考页。

2.  注册[ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数。

    如果异步发送请求，则通常想要另一个驱动程序完成每个请求时通知您的驱动程序的框架。 您的驱动程序应定义[ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数，并通过调用注册[ **WdfRequestSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine). 有关详细信息，请参阅[完成 I/O 请求](completing-i-o-requests.md)。

3.  发送请求。

    在您的驱动程序后格式请求和注册[ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数，您的驱动程序必须调用[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend). 此方法可以同步或异步，具体取决于中设置的标志发送请求*RequestOptions*参数。 更简单的方法来同步发送的 I/O 请求，请参阅[以同步方式发送 I/O 请求](sending-i-o-requests-synchronously.md)。 有关如何获取的完成状态的异步请求或通过调用发送任何请求信息**WdfRequestSend**，请参阅[完成 I/O 请求](completing-i-o-requests.md)。

调用的驱动程序[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)发送 I/O 请求可以尝试取消该请求更高版本。 有关详细信息，请参阅[取消 I/O 请求](canceling-i-o-requests.md)。

某些驱动程序可能将单个 I/O 请求发送到多个设备，而且因此到多个 I/O 有针对性的通过调用[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)不止一次为每个请求。 这些驱动程序必须调用[ **WdfRequestChangeTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestchangetarget)对每个调用之前**WdfRequestSend**后要验证是否可以将请求发送到下一个 I/O 目标的第一个。

 

 





