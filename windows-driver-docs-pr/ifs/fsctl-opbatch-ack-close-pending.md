---
title: FSCTL_OPBATCH_ACK_CLOSE_PENDING 控制代码
description: FSCTL\_OPBATCH\_ACK\_关闭\_挂起的控制代码响应通知的排他 （级别 1、 批处理或筛选器） 文件中的机会锁 (oplock) 已中断。
ms.assetid: 310cd778-5a1c-46e2-8c05-127fc754ecfe
keywords:
- FSCTL_OPBATCH_ACK_CLOSE_PENDING 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_OPBATCH_ACK_CLOSE_PENDING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82d1c7534e8460c100c568ebd3aba9bafdd95571
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380123"
---
# <a name="fsctlopbatchackclosepending-control-code"></a>FSCTL\_OPBATCH\_ACK\_关闭\_挂起的控制代码


**FSCTL\_OPBATCH\_ACK\_关闭\_PENDING**控制代码响应通知的排他 （级别 1、 批处理或筛选器） 文件中的机会锁 (oplock) 具有被破坏。 客户端应用程序将发送此控制代码，以指示它确认破坏 oplock，并且它即将关闭文件句柄。

为批处理或筛选器 oplock 时，调用方必须发送此控制代码后关闭其文件句柄。 否则，系统将阻止等待要关闭的文件句柄。

此控制代码不应与第 1 级 oplock 一起使用。 然而，对于级别 1 oplock 时，该系统作为完整的中断，确认将此控制代码，并且调用方不需要关闭文件句柄。

很少使用此控制代码。 当客户端应用程序会收到通知的破坏 oplock 的文件，并关闭该文件的句柄时，该系统会将作为完整确认破坏 oplock 的文件句柄关闭。 因此不需要发送此控制代码。

若要处理此控制代码，微筛选器调用[ **FltOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)使用以下参数。 文件系统或旧筛选器驱动程序调用[ **FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)。

有关详细信息，有关伺机锁定以及 FSCTL\_OPBATCH\_ACK\_关闭\_挂起的控制代码，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
该文件的不透明 oplock 对象指针。

<a href="" id="callbackdata"></a>*CallbackData*  
[**FltOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)仅。 回调数据 ([**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 的 IRP 结构\_MJ\_文件\_系统\_控件 FSCTL请求。 *FsControlCode*操作的参数必须为 FSCTL\_OPBATCH\_ACK\_关闭\_PENDING。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)仅。 IRP 的 IRP\_MJ\_文件\_系统\_控件 FSCTL 请求。 *FsControlCode*操作的参数必须为 FSCTL\_OPBATCH\_ACK\_关闭\_PENDING。

<a href="" id="opencount"></a>*OpenCount*  
不用于此操作;设置为零。

<a name="status-block"></a>状态块
------------

[**FltOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)始终返回 FLT\_PREOP\_完成此操作。

[**FsRtlOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)返回值对于此操作的以下 NTSTATUS 之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>持有此句柄 oplock 已被破坏的过程中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_OPLOCK_PROTOCOL</strong></p></td>
<td align="left"><p>通过此句柄，持有没有机会锁的时间或需要破坏 oplock 不是当前正在进行中。 这是一个错误代码。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FLT\_CALLBACK\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IRP 的参数\_MJ\_文件\_系统\_控件**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FSCTL\_OPLOCK\_BREAK\_ACK\_NO\_2**](fsctl-oplock-break-ack-no-2.md)

[**FSCTL\_OPLOCK\_BREAK\_ACKNOWLEDGE**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_OPLOCK\_BREAK\_NOTIFY**](fsctl-oplock-break-notify.md)

[**FSCTL\_REQUEST\_BATCH\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_REQUEST\_FILTER\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_REQUEST\_OPLOCK\_LEVEL\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_REQUEST\_OPLOCK\_LEVEL\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

 

 






