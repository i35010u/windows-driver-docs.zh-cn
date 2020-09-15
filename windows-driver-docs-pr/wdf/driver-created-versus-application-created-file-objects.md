---
title: 驱动程序创建的文件对象与应用程序创建的文件对象
description: 驱动程序创建的文件对象与应用程序创建的文件对象
ms.assetid: f81ae0ed-a29c-476e-9b16-ff554eef1de9
keywords:
- 用于处理 i/o WDK UMDF、驱动程序创建的文件对象
- 用于处理 i/o WDK UMDF 的文件对象，应用程序已创建
- I/o 请求 WDK UMDF、文件对象、驱动程序创建的与应用程序创建的
- 用户模式驱动程序框架 WDK，处理 i/o、驱动程序创建与应用程序创建的文件对象
- UMDF WDK，处理 i/o、驱动程序创建与应用程序创建的文件对象
- 用户模式驱动程序 WDK UMDF，处理 i/o、驱动程序创建与应用程序创建的文件对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeb9ad6814ee7b28dda3167c6fdbf6b6e174d289
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106916"
---
# <a name="driver-created-versus-application-created-file-objects"></a>驱动程序创建的文件对象与应用程序创建的文件对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当应用程序打开设备的句柄时，框架会调用驱动程序的 [**IQueueCallbackCreate：： OnCreateFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile) 方法，并为与设备关联的文件对象提供指向 [**IWDFFile**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile) 接口的指针。 应用程序发送到打开的句柄的任何 i/o 请求都与创建的文件对象相关联。 当此类请求到达时，框架从驱动程序提供的一个 [UMDF 队列对象接口](/windows-hardware/drivers/ddi/wudfddi/)调用适当的方法。 然后，驱动程序可以调用 [**IWDFIoRequest：： GetFileObject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getfileobject) 来确定与请求关联的文件对象。 驱动程序可以对文件对象调用 [**AssignContext**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-assigncontext) ，以关联特定于 i/o 会话的上下文。

下表显示了应用程序的调用和驱动程序收到的生成的通知。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">应用程序启动</th>
<th align="left">驱动程序接收</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>对 Microsoft Win32 <a href="/windows/desktop/api/fileapi/nf-fileapi-createfilea" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](/windows/desktop/api/fileapi/nf-fileapi-createfilea)"><strong>CreateFile</strong></a> 函数的调用。</p></td>
<td align="left"><p>对其 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile" data-raw-source="[&lt;strong&gt;IQueueCallbackCreate::OnCreateFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)"><strong>IQueueCallbackCreate：： OnCreateFile</strong></a> 方法的调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>对 Win32 <strong>ReadFileEx</strong>、 <strong>WriteFileEx</strong>或 <a href="/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl</strong></a> 函数的调用。</p></td>
<td align="left"><p>对其 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread" data-raw-source="[&lt;strong&gt;IQueueCallbackRead::OnRead&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread)"><strong>IQueueCallbackRead：： OnRead</strong></a>、 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite" data-raw-source="[&lt;strong&gt;IQueueCallbackWrite::OnWrite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)"><strong>IQueueCallbackWrite：： OnWrite</strong></a>或 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol" data-raw-source="[&lt;strong&gt;IQueueCallbackDeviceIoControl::OnDeviceIoControl&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)"><strong>IQueueCallbackDeviceIoControl：： OnDeviceIoControl</strong></a> 方法的调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>对文件对象的最后一个打开句柄调用 Win32 <strong>CloseHandle</strong> 函数。</p></td>
<td align="left"><p>对其 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile" data-raw-source="[&lt;strong&gt;IFileCallbackCleanup::OnCleanupFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)"><strong>IFileCallbackCleanup：： OnCleanupFile</strong></a> 方法的调用。</p>
<p>驱动程序将取消或完成与该文件对象关联的所有 i/o 请求。</p>
<p>驱动程序从清除通知返回后，UMDF 会取消任何挂起的 i/o 请求。</p>
<p>清理完成后，UMDF 将取消挂起的 i/o 请求，驱动程序将收到对其 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile" data-raw-source="[&lt;strong&gt;IFileCallbackClose::OnCloseFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)"><strong>IFileCallbackClose：： OnCloseFile</strong></a> 方法的调用。</p></td>
</tr>
</tbody>
</table>

 

系统组件可能代表通用 Windows 应用发出创建请求。 如果驱动程序需要确定发出 create 请求的应用程序的进程 ID，它可以调用 [**IWDFFile3：： GetInitiatorProcessId**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdffile3-getinitiatorprocessid) 方法。

## <a name="driver-created-file-objects"></a>驱动程序创建的文件对象


如果驱动程序需要创建独立于应用程序的 i/o 请求并将其发送到堆栈 (默认 i/o 目标) ，则驱动程序必须调用 [**IWDFDevice：： CreateWdfFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile) 来检索指向 [**IWDFDriverCreatedFile**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdrivercreatedfile) 接口的指针。 在这种情况下，下一个驱动程序收到的通知与应用程序生成请求时的驱动程序收到的通知相同。

下表显示了驱动程序的调用，以及向堆栈中的下一个驱动程序发出的通知。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序启动</th>
<th align="left">堆栈中的下一个驱动程序接收</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>对 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile" data-raw-source="[&lt;strong&gt;IWDFDevice::CreateWdfFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)"><strong>IWDFDevice：： CreateWdfFile</strong></a> 方法的调用。</p>
<p>UMDF 创建的文件对象表示设备与堆栈中的下一个设备之间的 i/o 会话。</p></td>
<td align="left"><p>对其 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile" data-raw-source="[&lt;strong&gt;IQueueCallbackCreate::OnCreateFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)"><strong>IQueueCallbackCreate：： OnCreateFile</strong></a> 方法的调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>对 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest" data-raw-source="[&lt;strong&gt;IWDFDevice::CreateRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)"><strong>IWDFDevice：： CreateRequest</strong></a> 方法的调用。</p>
<p>对请求进行格式设置的调用 (例如，对 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForIoctl&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)"><strong>IWDFIoTarget：： FormatRequestForIoctl</strong></a> 方法的调用) 。</p>
<p>调用 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest：： Send</strong></a> 方法。</p></td>
<td align="left"><p>对其 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread" data-raw-source="[&lt;strong&gt;IQueueCallbackRead::OnRead&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread)"><strong>IQueueCallbackRead：： OnRead</strong></a>、 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite" data-raw-source="[&lt;strong&gt;IQueueCallbackWrite::OnWrite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)"><strong>IQueueCallbackWrite：： OnWrite</strong></a>或 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol" data-raw-source="[&lt;strong&gt;IQueueCallbackDeviceIoControl::OnDeviceIoControl&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)"><strong>IQueueCallbackDeviceIoControl：： OnDeviceIoControl</strong></a> 方法的调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>调用 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close" data-raw-source="[&lt;strong&gt;IWDFDriverCreatedFile::Close&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close)"><strong>IWDFDriverCreatedFile：： Close</strong></a> 方法。</p></td>
<td align="left"><p>对其 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile" data-raw-source="[&lt;strong&gt;IFileCallbackCleanup::OnCleanupFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)"><strong>IFileCallbackCleanup：： OnCleanupFile</strong></a> 方法的调用。</p>
<p>驱动程序将取消或完成与该文件对象关联的所有 i/o 请求。</p>
<p>驱动程序从清除通知返回后，UMDF 会取消任何挂起的 i/o 请求。</p>
<p>清理完成后，UMDF 将取消挂起的 i/o 请求，驱动程序将收到对其 <a href="/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile" data-raw-source="[&lt;strong&gt;IFileCallbackClose::OnCloseFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)"><strong>IFileCallbackClose：： OnCloseFile</strong></a> 方法的调用。</p></td>
</tr>
</tbody>
</table>

 

对于堆栈中的下一个设备，由应用程序创建的文件对象与更高层设备创建的文件对象之间没有差异。

