---
title: FSCTL_OPLOCK_BREAK_NOTIFY 控制代码
description: FSCTL \_ oplock \_ 中断 \_ 通知控制代码允许调用应用程序等待机会锁的完成， (OPLOCK) 中断。
ms.assetid: 80fe4e5f-fb6f-4c11-8574-97d7f0e7cc6b
keywords:
- FSCTL_OPLOCK_BREAK_NOTIFY 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: b5d59b958e16b3680625449d63efbfbfc0d5e9dc
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063404"
---
# <a name="fsctl_oplock_break_notify-control-code"></a>FSCTL \_ OPLOCK \_ 中断 \_ 通知控制代码


**FSCTL \_ oplock \_ 中断 \_ 通知**控制代码允许调用应用程序等待机会锁的完成， (OPLOCK) 中断。

此操作仅适用于打开调用方句柄时已启动的 oplock 中断。 如果 OPLOCKED，则必须已使用文件完成打开句柄 \_ \_ \_ 。 如果当前持有 oplock 并且 oplock 中断尚未开始，则此操作无意义。

若要处理此控制代码，微筛选器将使用以下参数调用 [**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) 。 文件系统或旧筛选器驱动程序调用 [**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)。

有关机会锁定和 **FSCTL \_ OPLOCK \_ 中断 \_ 通知** 控制代码的详细信息，请参阅 Microsoft Windows SDK 文档。

**参数**

<a href="" id="oplock"></a>*机会*  
文件的不透明 oplock 对象指针。

<a href="" id="callbackdata"></a>*CallbackData*  
仅[**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) 。 为 IRP MJ [** \_ \_ **](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) \_ \_ 文件 \_ 系统 \_ 控制 FSCTL 请求 (FLT 回调数据) 结构的回叫数据。 操作的 *FsControlCode* 参数必须是 FSCTL \_ OPLOCK \_ 中断 \_ 通知。

<a href="" id="irp"></a>*Irp*  
仅[**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl) 。 Irp \_ MJ \_ 文件 \_ 系统 \_ 控件 FSCTL 请求。 操作的 *FsControlCode* 参数必须是 FSCTL \_ OPLOCK \_ 中断 \_ 通知。

<a href="" id="opencount"></a>*OpenCount*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------

[**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) \_ \_ 如果 oplock 中断正在进行，则 FltOplockFsctrl 将返回 FLT PREOP，并将在 oplock 中断完成时完成 IRP。  (在这种情况下，IRP 最终最终可能会在状态为 "成功" 或 "已取消" 状态时完成 \_ \_ 。 ) 否则， **FltOplockFsctrl** 返回 FLT \_ PREOP \_ complete。

对于此操作， [**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)返回以下 NTSTATUS 值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>此句柄未持有 oplock，或持有 oplock，并且 oplock 中断尚未开始。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_OPLOCK_PROTOCOL</strong></p></td>
<td align="left"><p>IRP 在 FSCTL_OPLOCK_BREAK_NOTIFY 操作完成前被取消。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_PENDING</strong></p></td>
<td align="left"><p>Oplock 中断正在进行。 完成 oplock 中断后，将完成 IRP。 IRP 最终可以通过 STATUS_SUCCESS 或 STATUS_CANCELLED 完成。 这是一个成功代码。</p></td>
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
<td align="left">Ntifs (包含 Ntifs 或 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**\_IRP \_ MJ \_ 文件 \_ 系统 \_ 控件的 FLT 参数**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FSCTL \_ OPBATCH \_ ACK \_ CLOSE \_ 挂起**](fsctl-opbatch-ack-close-pending.md)

[**FSCTL \_ OPLOCK \_ 中断 \_ ACK \_ NO \_ 2**](fsctl-oplock-break-ack-no-2.md)

[**FSCTL \_ OPLOCK \_ 中断 \_ 确认**](fsctl-oplock-break-acknowledge.md)

[**FSCTL \_ 请求 \_ 批处理 \_ OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL \_ 请求 \_ 筛选器 \_ OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL \_ 请求 \_ OPLOCK \_ LEVEL \_ 1**](fsctl-request-oplock-level-1.md)

[**FSCTL \_ 请求 \_ OPLOCK \_ LEVEL \_ 2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md)

 

