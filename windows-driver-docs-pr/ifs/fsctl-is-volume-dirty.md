---
title: FSCTL_IS_VOLUME_DIRTY 控制代码
description: FSCTL \_ 是 \_ 批量 \_ 脏控制代码确定指定的卷是否已更新。
keywords:
- FSCTL_IS_VOLUME_DIRTY 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_IS_VOLUME_DIRTY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c47f86791f9842be9637fc40f4d11ce1725ade5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808347"
---
# <a name="fsctl_is_volume_dirty-control-code"></a>FSCTL \_ 是 \_ 批量 \_ 脏控制代码


**FSCTL \_ 是 \_ 批量 \_ 脏** 控制代码确定指定的卷是否已更新。

如果卷信息文件已损坏，NTFS 将返回 "状态 \_ 文件 \_ 已损坏" \_ 错误。

要执行此操作，微筛选器驱动程序将调用 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 与以下参数、文件系统、重定向程序和旧文件系统筛选器驱动程序调用 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) ，并提供以下参数。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 卷的文件对象指针。 此参数必须表示打开的文件系统卷的用户卷。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 卷的句柄。 此参数必须是打开已装入文件系统卷的用户卷的句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL \_ \_ \_ 对此操作进行了大量更新。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用;设置为 **NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不与此操作一起使用;设置为零。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向分配给调用方的32位对齐缓冲区的指针，该缓冲区接收用于指示当前卷是否已更新的 ULONG 标志位掩码。 可以设置下表中的一个或多个标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>VOLUME_IS_DIRTY</p></td>
<td align="left"><p>卷已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>VOLUME_UPGRADE_SCHEDULED</p></td>
<td align="left"><p>目前不会使用此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>所有其他值</p></td>
<td align="left"><p>留待将来使用。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer* 参数指向的缓冲区的大小（以字节为单位）。 此大小必须至少为 sizeof (ULONG) 。

<a name="status-block"></a>状态块
------------

如果操作成功，则 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))返回状态 \_ SUCCESS。 否则，相应的函数可能会返回以下某个 NTSTATUS 值：

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
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOURCES</strong></p></td>
<td align="left"><p>文件系统遇到池分配错误。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p><em>OutputBuffer</em>参数指向的缓冲区为<strong>NULL</strong>，或者<em>FileHandle</em>或<em>FileObject</em>参数不表示用户卷打开。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_USER_BUFFER</strong></p></td>
<td align="left"><p><em>OutputBuffer</em>参数指向的缓冲区不够大，无法保存重新分析点数据，或<em>FileHandle</em>或<em>FileObject</em>参数不表示已打开用户卷。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>卷未装入。 这是一个错误代码。</p></td>
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

[**\_IRP \_ MJ \_ 文件 \_ 系统 \_ 控件的 FLT 参数**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

 

