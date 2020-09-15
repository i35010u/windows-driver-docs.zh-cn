---
title: 异步发送 I/O 请求
description: 异步发送 I/O 请求
ms.assetid: 9f6fb85e-96aa-4945-8c8a-13277beff140
keywords:
- 一般 i/o 目标 WDK KMDF，将 i/o 请求发送到
- 发送 i/o 请求 WDK KMDF
- 发送 i/o 请求 WDK KMDF，异步
- 异步发送 i/o 请求 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d235433d10b64fcbcbab21dbffd4c9fa91378fa
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107156"
---
# <a name="sending-io-requests-asynchronously"></a>异步发送 I/O 请求





必须先格式化请求，然后才能将 i/o 请求异步发送到 i/o 目标。 下表列出了驱动程序可以调用以格式化 i/o 请求的 i/o 目标对象方法。

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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForRead&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread)"><strong>WdfIoTargetFormatRequestForRead</strong></a></p></td>
<td align="left"><p>格式化读取请求</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForWrite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite)"><strong>WdfIoTargetFormatRequestForWrite</strong></a></p></td>
<td align="left"><p>格式化写入请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforioctl" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForIoctl&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforioctl)"><strong>WdfIoTargetFormatRequestForIoctl</strong></a></p></td>
<td align="left"><p>设置设备控件请求的格式</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctl&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl)"><strong>WdfIoTargetFormatRequestForInternalIoctl</strong></a></p></td>
<td align="left"><p>设置内部设备控制请求的格式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctlOthers&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers)"><strong>WdfIoTargetFormatRequestForInternalIoctlOthers</strong></a></p></td>
<td align="left"><p>设置非标准内部设备控制请求的格式</p></td>
</tr>
</tbody>
</table>

 

若要以异步方式发送 i/o 请求，驱动程序必须：

1.  格式化请求。

    使用上表中列出的方法之一来格式化请求。 有关如何使用这些方法的详细信息，请参阅方法的参考页。

2.  注册 [*CompletionRoutine*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine) 回调函数。

    如果以异步方式发送请求，则通常需要框架在另一个驱动程序完成每个请求时通知驱动程序。 你的驱动程序应定义 [*CompletionRoutine*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine) 回调函数并通过调用 [**WdfRequestSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)来注册它。 有关详细信息，请参阅 [完成 I/o 请求](completing-i-o-requests.md)。

3.  发送请求。

    驱动程序格式化请求并注册 [*CompletionRoutine*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine) 回调函数后，你的驱动程序必须调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)。 此方法使你能够以同步或异步方式发送请求，具体取决于在 *RequestOptions* 参数中设置的标志。 有关同步发送 i/o 请求的更简单方法，请参阅 [同步发送 I/o 请求](sending-i-o-requests-synchronously.md)。 有关如何获取异步请求或通过调用 **WdfRequestSend**发送的任何请求的完成状态的信息，请参阅 [完成 i/o 请求](completing-i-o-requests.md)。

调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 发送 i/o 请求的驱动程序稍后可以尝试取消请求。 有关详细信息，请参阅 [取消 I/o 请求](canceling-i-o-requests.md)。

对于每个请求，某些驱动程序可能会通过多次调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) ，将单个 i/o 请求发送到多个设备，进而发送到多个 i/o 目标。 在第一次调用**WdfRequestSend**之前，这些驱动程序必须调用[**WdfRequestChangeTarget**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestchangetarget) ，以验证是否可以将请求发送到下一个 i/o 目标。

