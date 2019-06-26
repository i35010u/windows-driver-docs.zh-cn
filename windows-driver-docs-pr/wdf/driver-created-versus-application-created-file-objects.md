---
title: 驱动程序创建的文件对象与应用程序创建的文件对象
description: 驱动程序创建的文件对象与应用程序创建的文件对象
ms.assetid: f81ae0ed-a29c-476e-9b16-ff554eef1de9
keywords:
- 要处理 I/O WDK UMDF，驱动程序创建的文件对象
- 要处理 I/O WDK UMDF，应用程序创建的文件对象
- I/O 请求 WDK UMDF 文件对象，而不是驱动程序创建应用程序创建
- 用户模式驱动程序框架 WDK，文件句柄的 I/O，驱动程序创建与应用程序创建的对象
- UMDF WDK，文件对象来处理 I/O，驱动程序的创建与应用程序创建
- 用户模式驱动程序 WDK UMDF 文件对象来处理 I/O，驱动程序的创建与应用程序创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d090fad5592aca66b73d7a78546f18b220a3c314
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377390"
---
# <a name="driver-created-versus-application-created-file-objects"></a>驱动程序创建的文件对象与应用程序创建的文件对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

应用程序打开到设备的句柄，框架将调用您的驱动程序[ **IQueueCallbackCreate::OnCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)方法并提供一个指向[ **IWDFFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile)与设备相关联的文件对象的接口。 任何应用程序发送到打开的句柄的 I/O 请求都与创建的文件对象。 此类请求到达时，框架将调用相应的方法之一的驱动程序提供[UMDF 队列对象接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/)。 然后，该驱动程序可以调用[ **IWDFIoRequest::GetFileObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getfileobject)来确定与请求关联的文件对象。 该驱动程序可以调用[ **AssignContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-assigncontext)上要将特定于 I/O 会话的上下文相关联的文件对象。

下表显示了应用程序发出的调用和生成驱动程序收到的通知。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">应用程序启动</th>
<th align="left">驱动程序将收到</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>调用 Microsoft Win32 <a href="https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)"> <strong>CreateFile</strong> </a>函数。</p></td>
<td align="left"><p>调用其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile" data-raw-source="[&lt;strong&gt;IQueueCallbackCreate::OnCreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)"> <strong>IQueueCallbackCreate::OnCreateFile</strong> </a>方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p>调用 Win32 <strong>ReadFileEx</strong>， <strong>writefileex 只写入</strong>，或<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"> <strong>DeviceIoControl</strong> </a>函数。</p></td>
<td align="left"><p>调用其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackread-onread" data-raw-source="[&lt;strong&gt;IQueueCallbackRead::OnRead&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackread-onread)"> <strong>IQueueCallbackRead::OnRead</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite" data-raw-source="[&lt;strong&gt;IQueueCallbackWrite::OnWrite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)"> <strong>IQueueCallbackWrite::OnWrite</strong></a>，或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol" data-raw-source="[&lt;strong&gt;IQueueCallbackDeviceIoControl::OnDeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)"> <strong>IQueueCallbackDeviceIoControl::OnDeviceIoControl</strong> </a>方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>调用 Win32 <strong>CloseHandle</strong>的最后一个打开句柄的文件对象的函数。</p></td>
<td align="left"><p>调用其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile" data-raw-source="[&lt;strong&gt;IFileCallbackCleanup::OnCleanupFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)"> <strong>IFileCallbackCleanup::OnCleanupFile</strong> </a>方法。</p>
<p>该驱动程序取消或完成与文件对象相关联的所有 I/O 请求。</p>
<p>驱动程序将返回从清理通知后，UMDF 取消任何挂起的 I/O 请求。</p>
<p>清理完成并且 UMDF 取消的挂起 I/O 请求后，该驱动程序接收到调用其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile" data-raw-source="[&lt;strong&gt;IFileCallbackClose::OnCloseFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)"> <strong>IFileCallbackClose::OnCloseFile</strong> </a>方法。</p></td>
</tr>
</tbody>
</table>

 

系统组件可能会发出代表通用 Windows 应用程序创建请求。 如果驱动程序需要确定进程 ID 的应用的发布创建请求，它可以调用[ **IWDFFile3::GetInitiatorProcessId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdffile3-getinitiatorprocessid)方法。

## <a name="driver-created-file-objects"></a>驱动程序创建文件对象


如果您的驱动程序需要创建和发送的 I/O 请求的独立应用程序到堆栈 （默认 I/O 目标） 驱动程序中的下一步驱动程序必须调用[ **IWDFDevice::CreateWdfFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)到检索一个指向[ **IWDFDriverCreatedFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdrivercreatedfile)接口。 在这种情况下下, 一步的驱动程序将收到相同应用程序生成请求时，您的驱动程序收到的通知。

下表显示堆栈中使您的驱动程序的调用和对下一步的驱动程序生成的通知。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序将启动</th>
<th align="left">堆栈中的下一步驱动程序将收到</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createwdffile" data-raw-source="[&lt;strong&gt;IWDFDevice::CreateWdfFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)"> <strong>IWDFDevice::CreateWdfFile</strong> </a>方法。</p>
<p>UMDF 创建的文件对象表示设备和堆栈中的下一个设备之间的 I/O 会话。</p></td>
<td align="left"><p>调用其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile" data-raw-source="[&lt;strong&gt;IQueueCallbackCreate::OnCreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)"> <strong>IQueueCallbackCreate::OnCreateFile</strong> </a>方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createrequest" data-raw-source="[&lt;strong&gt;IWDFDevice::CreateRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createrequest)"> <strong>IWDFDevice::CreateRequest</strong> </a>方法。</p>
<p>若要设置格式的请求的调用 (例如，调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForIoctl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)"> <strong>IWDFIoTarget::FormatRequestForIoctl</strong> </a>方法)。</p>
<p>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"> <strong>IWDFIoRequest::Send</strong> </a>方法。</p></td>
<td align="left"><p>调用其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackread-onread" data-raw-source="[&lt;strong&gt;IQueueCallbackRead::OnRead&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackread-onread)"> <strong>IQueueCallbackRead::OnRead</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite" data-raw-source="[&lt;strong&gt;IQueueCallbackWrite::OnWrite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)"> <strong>IQueueCallbackWrite::OnWrite</strong></a>，或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol" data-raw-source="[&lt;strong&gt;IQueueCallbackDeviceIoControl::OnDeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)"> <strong>IQueueCallbackDeviceIoControl::OnDeviceIoControl</strong> </a>方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close" data-raw-source="[&lt;strong&gt;IWDFDriverCreatedFile::Close&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close)"> <strong>IWDFDriverCreatedFile::Close</strong> </a>方法。</p></td>
<td align="left"><p>调用其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile" data-raw-source="[&lt;strong&gt;IFileCallbackCleanup::OnCleanupFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)"> <strong>IFileCallbackCleanup::OnCleanupFile</strong> </a>方法。</p>
<p>该驱动程序取消或完成与文件对象相关联的所有 I/O 请求。</p>
<p>驱动程序将返回从清理通知后，UMDF 取消任何挂起的 I/O 请求。</p>
<p>清理完成并且 UMDF 取消的挂起 I/O 请求后，该驱动程序接收到调用其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile" data-raw-source="[&lt;strong&gt;IFileCallbackClose::OnCloseFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)"> <strong>IFileCallbackClose::OnCloseFile</strong> </a>方法。</p></td>
</tr>
</tbody>
</table>

 

堆栈中下一步设备之间没有区别的应用程序创建的文件对象并由更高层的设备创建的文件对象。

 

 





