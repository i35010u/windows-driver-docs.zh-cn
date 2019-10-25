---
title: FSCTL_OPBATCH_ACK_CLOSE_PENDING 控制代码
description: FSCTL\_OPBATCH\_ACK\_CLOSE\_挂起控制代码对文件上的独占（级别1、批处理或筛选）机会锁（oplock）的通知进行响应。
ms.assetid: 310cd778-5a1c-46e2-8c05-127fc754ecfe
keywords:
- FSCTL_OPBATCH_ACK_CLOSE_PENDING 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: d21a7b4a2787947dee0d269e7f8cdd572d17f67a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841276"
---
# <a name="fsctl_opbatch_ack_close_pending-control-code"></a>FSCTL\_OPBATCH\_ACK\_关闭\_挂起控制代码


**FSCTL\_OPBATCH\_ACK\_CLOSE\_挂起**控制代码对文件上的独占（级别1、批处理或筛选）机会锁（oplock）的通知进行响应。 客户端应用程序发送此控制代码以指示它会确认 oplock 中断，并即将关闭文件句柄。

对于批处理或筛选器 oplock 中断，调用方必须在发送此控制代码后关闭其文件句柄。 否则，系统将阻止等待文件句柄关闭。

此控制代码不应与 level 1 oplock 一起使用。 尽管如此，对于第1级 oplock 中断，系统会将此控制代码视为完全确认中断，并且不需要调用方关闭文件句柄。

很少使用此控制代码。 当对某个文件的 oplock 中断通知客户端应用程序时，如果该客户端应用程序关闭了该文件的句柄，则系统会将该文件句柄关闭，作为对 oplock 中断的完全确认。 因此，永远不需要发送此控制代码。

若要处理此控制代码，微筛选器将使用以下参数调用[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) 。 文件系统或旧筛选器驱动程序调用[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)。

有关机会锁定以及有关 FSCTL\_OPBATCH\_ACK\_关闭\_挂起控制代码的详细信息，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="oplock"></a>*机会*  
文件的不透明 oplock 对象指针。

<a href="" id="callbackdata"></a>*CallbackData*  
仅[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) 。 IRP\_MJ\_文件\_SYSTEM\_控制 FSCTL 请求的回调数据（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构。 操作的*FsControlCode*参数必须是 FSCTL\_OPBATCH\_ACK\_关闭\_挂起。

<a href="" id="irp"></a>*Irp*  
仅[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl) 。 Irp\_MJ\_文件\_系统\_控制 FSCTL 请求。 操作的*FsControlCode*参数必须是 FSCTL\_OPBATCH\_ACK\_关闭\_挂起。

<a href="" id="opencount"></a>*OpenCount*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------

对于此操作， [**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)始终返回 FLT\_PREOP\_完成。

对于此操作， [**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)返回以下 NTSTATUS 值之一：

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
<td align="left"><p>此句柄持有的 oplock 处于中断过程中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_OPLOCK_PROTOCOL</strong></p></td>
<td align="left"><p>此句柄未持有 oplock，或 oplock 中断当前未进行。 这是一个错误代码。</p></td>
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
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs 或 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**用于 IRP\_MJ\_文件\_系统\_控制的 FLT\_参数**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FSCTL\_OPLOCK\_中断\_ACK\_NO\_2**](fsctl-oplock-break-ack-no-2.md)

[**FSCTL\_OPLOCK\_中断\_确认**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_OPLOCK\_中断\_通知**](fsctl-oplock-break-notify.md)

[**FSCTL\_请求\_批\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_REQUEST\_FILTER\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_请求\_OPLOCK\_级别\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_请求\_OPLOCK\_级别\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

 

 






