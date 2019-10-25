---
title: FSCTL_IS_VOLUME_DIRTY 控制代码
description: FSCTL\_\_卷\_脏控制代码确定指定的卷是否已更新。
ms.assetid: 77263957-cf7f-4db1-81b7-c58438202518
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
ms.openlocfilehash: aa38c11230bff83b14a02ac7c03411ac26e54cb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841295"
---
# <a name="fsctl_is_volume_dirty-control-code"></a>FSCTL\_\_卷\_脏控制代码


**FSCTL\_\_卷\_脏**控制代码确定指定的卷是否已更新。

如果卷信息文件已损坏，NTFS 将返回状态\_文件\_损坏\_错误。

要执行此操作，微筛选器驱动程序将调用[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)与以下参数、文件系统、重定向程序和旧文件系统筛选器驱动程序调用[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) ，并提供以下参数。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 卷的文件对象指针。 此参数必须表示打开的文件系统卷的用户卷。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 卷的句柄。 此参数必须是打开已装入文件系统卷的用户卷的句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_为此操作\_卷\_更新。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用;设置为**NULL**。

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
<th align="left">Value</th>
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
<td align="left"><p>当前未使用此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>所有其他值</p></td>
<td align="left"><p>保留供将来使用。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer*参数指向的缓冲区的大小（以字节为单位）。 此大小必须至少为 sizeof （ULONG）。

<a name="status-block"></a>状态块
------------

如果操作成功，则[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回状态\_成功。 否则，相应的函数可能会返回以下某个 NTSTATUS 值：

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
<td align="left">Ntifs （包括 Ntifs 或 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**用于 IRP\_MJ\_文件\_系统\_控制的 FLT\_参数**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






