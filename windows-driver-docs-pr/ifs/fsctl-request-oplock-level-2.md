---
title: FSCTL_REQUEST_OPLOCK_LEVEL_2 控制代码
description: FSCTL\_请求\_OPLOCK\_级别\_2 控制代码请求对文件进行第2级机会锁定（OPLOCK）。
ms.assetid: 418fbbc7-5dca-4c73-8ea0-d4b4e0a2efff
keywords:
- FSCTL_REQUEST_OPLOCK_LEVEL_2 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_REQUEST_OPLOCK_LEVEL_2
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14c57d7a940a40a391d9ea71a968b256b6b81b2c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841257"
---
# <a name="fsctl_request_oplock_level_2-control-code"></a>FSCTL\_请求\_OPLOCK\_级别\_2 控制代码


**FSCTL\_请求\_OPLOCK\_级别\_2**控制代码请求对文件进行第2级机会锁定（OPLOCK）。

若要处理此控制代码，微筛选器将使用以下参数调用[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) 。 文件系统或旧筛选器驱动程序调用[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)。

有关机会锁定的详细信息，以及关于**FSCTL\_请求\_OPLOCK\_级别\_2**控制代码的详细信息，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="oplock"></a>*机会*  
文件的不透明 oplock 对象指针。

<a href="" id="callbackdata"></a>*CallbackData*  
仅[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) 。 IRP\_MJ\_文件\_SYSTEM\_控制 FSCTL 请求的回调数据（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构。 操作的*FsControlCode*参数必须是 FSCTL\_请求\_OPLOCK\_级别\_2。

<a href="" id="irp"></a>*Irp*  
仅[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl) 。 Irp\_MJ\_文件\_系统\_控制 FSCTL 请求。 操作的*FsControlCode*参数必须是 FSCTL\_请求\_OPLOCK\_级别\_2。

<a href="" id="opencount"></a>*OpenCount*  
指定文件的锁定状态。 如果文件上存在字节范围锁，则将此参数设置为非零 ULONG 值，否则设置为零。

<a name="status-block"></a>状态块
------------

如果已授予 oplock， [**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)将为此操作返回 FLT\_\_PREOP。 否则，它将返回 FLT\_PREOP\_完成。

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
<td align="left"><p><strong>STATUS_PENDING</strong></p></td>
<td align="left"><p>已授予 oplock。 这是一个成功代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_CANCELLED</strong></p></td>
<td align="left"><p>IRP 在 FSCTL_REQUEST_OPLOCK_LEVEL_2 操作完成前被取消。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_OPLOCK_NOT_GRANTED</strong></p></td>
<td align="left"><p>无法授予 oplock。 这是一个错误代码。</p></td>
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

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**用于 IRP\_MJ\_文件\_系统\_控制的 FLT\_参数**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FSCTL\_OPBATCH\_ACK\_关闭\_挂起**](fsctl-opbatch-ack-close-pending.md)

[**FSCTL\_OPLOCK\_中断\_ACK\_NO\_2**](fsctl-oplock-break-ack-no-2.md)

[**FSCTL\_OPLOCK\_中断\_确认**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_OPLOCK\_中断\_通知**](fsctl-oplock-break-notify.md)

[**FSCTL\_请求\_批\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_REQUEST\_FILTER\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_请求\_OPLOCK\_级别\_1**](fsctl-request-oplock-level-1.md)

[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

 

 






