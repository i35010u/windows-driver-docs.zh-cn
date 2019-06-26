---
title: FSCTL_OPLOCK_BREAK_NOTIFY 控制代码
description: FSCTL\_OPLOCK\_中断\_通知控件代码允许调用应用程序要等待的机会锁 (oplock) 中断的完成。
ms.assetid: 80fe4e5f-fb6f-4c11-8574-97d7f0e7cc6b
keywords:
- FSCTL_OPLOCK_BREAK_NOTIFY 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_OPLOCK_BREAK_NOTIFY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ad590a04fa6835f28978fda9ed933593b20fd81
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380097"
---
# <a name="fsctloplockbreaknotify-control-code"></a>FSCTL\_OPLOCK\_中断\_通知控件代码


**FSCTL\_OPLOCK\_中断\_通知**控制代码允许调用应用程序要等待的机会锁 (oplock) 中断的完成。

此操作是仅适用于已启动时打开调用方的句柄 oplock。 打开句柄必须具有已与文件一起\_完成\_如果\_OPLOCKED。 如果当前持有 oplock，并且需要破坏 oplock 尚未启动，此操作是毫无意义。

若要处理此控制代码，微筛选器调用[ **FltOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)使用以下参数。 文件系统或旧筛选器驱动程序调用[ **FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)。

有关详细信息，有关伺机锁定和大约**FSCTL\_OPLOCK\_中断\_通知**控制代码，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
该文件的不透明 oplock 对象指针。

<a href="" id="callbackdata"></a>*CallbackData*  
[**FltOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)仅。 回调数据 ([**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 的 IRP 结构\_MJ\_文件\_系统\_控件 FSCTL请求。 *FsControlCode*操作的参数必须为 FSCTL\_OPLOCK\_中断\_通知。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)仅。 IRP 的 IRP\_MJ\_文件\_系统\_控件 FSCTL 请求。 *FsControlCode*操作的参数必须为 FSCTL\_OPLOCK\_中断\_通知。

<a href="" id="opencount"></a>*OpenCount*  
不用于此操作;设置为零。

<a name="status-block"></a>状态块
------------

[**FltOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)返回 FLT\_PREOP\_如果需要破坏 oplock 正在进行，并且需要破坏 oplock 完成时将完成 IRP 的待决。 (在这种情况下，IRP 最终可以使用任一状态完成\_成功或状态\_已取消。)否则为**FltOplockFsctrl**返回 FLT\_PREOP\_完成。

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
<td align="left"><p>通过此句柄，持有没有机会锁的时间或持有 oplock，并且需要破坏 oplock 尚未启动。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_OPLOCK_PROTOCOL</strong></p></td>
<td align="left"><p>IRP FSCTL_OPLOCK_BREAK_NOTIFY 操作已完成之前取消。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_PENDING</strong></p></td>
<td align="left"><p>需要破坏 oplock 正在研发中。 需要破坏 oplock 完成时，将完成 IRP。 IRP 最终可以使用 STATUS_SUCCESS 或 STATUS_CANCELLED 完成。 这是一个成功代码。</p></td>
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

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FLT\_IRP 的参数\_MJ\_文件\_系统\_控件**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FSCTL\_OPBATCH\_ACK\_CLOSE\_PENDING**](fsctl-opbatch-ack-close-pending.md)

[**FSCTL\_OPLOCK\_BREAK\_ACK\_NO\_2**](fsctl-oplock-break-ack-no-2.md)

[**FSCTL\_OPLOCK\_BREAK\_ACKNOWLEDGE**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_REQUEST\_BATCH\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_REQUEST\_FILTER\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_REQUEST\_OPLOCK\_LEVEL\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_REQUEST\_OPLOCK\_LEVEL\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

 

 






