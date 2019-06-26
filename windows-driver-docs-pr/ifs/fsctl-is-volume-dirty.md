---
title: FSCTL_IS_VOLUME_DIRTY 控制代码
description: FSCTL\_IS\_卷\_脏控制代码确定指定的卷是否为脏对象。
ms.assetid: 77263957-cf7f-4db1-81b7-c58438202518
keywords:
- FSCTL_IS_VOLUME_DIRTY 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: bbdf6b3988fceac7c1f0477e4aab30add8df74c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380147"
---
# <a name="fsctlisvolumedirty-control-code"></a>FSCTL\_IS\_卷\_脏控制代码


**FSCTL\_IS\_卷\_繁琐**控制代码确定指定的卷是否为脏对象。

如果卷信息文件已损坏，NTFS 将返回状态\_文件\_损坏\_错误。

若要执行此操作，微筛选器驱动程序调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)与以下参数和文件系统中，重定向程序和旧的文件系统筛选驱动程序调用[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 该卷的文件对象指针。 此参数必须表示打开已装载的文件系统卷的一个用户卷。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 该卷的句柄。 此参数必须是已装载的文件系统卷的卷打开某个用户的句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_IS\_卷\_繁琐对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不用于此操作;设置为**NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不用于此操作;设置为零。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向接收指示卷是否为当前脏标志的 ULONG 位掩码的调用方分配的、 32 位对齐缓冲区的指针。 可以设置一个或多个以下表中的标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>VOLUME_IS_DIRTY</p></td>
<td align="left"><p>卷有问题。</p></td>
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
大小 （字节），所指向的缓冲区*OutputBuffer*参数。 此大小必须至少为 sizeof(ULONG)。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功如果操作成功。 否则，相应的函数可能返回以下 NTSTATUS 值之一：

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
<td align="left"><p>文件系统在遇到池分配失败。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>缓冲区的<em>OutputBuffer</em>参数指向的是<strong>NULL</strong>，或<em>FileHandle</em>或者<em>文件对象</em>参数不表示打开用户卷。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_USER_BUFFER</strong></p></td>
<td align="left"><p>缓冲区的<em>OutputBuffer</em>参数指向不是足够大以保存重新分析点数据，或<em>FileHandle</em>或<em>的文件对象</em>参数不表示卷的打开的用户。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>不装载卷。 这是一个错误代码。</p></td>
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

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






