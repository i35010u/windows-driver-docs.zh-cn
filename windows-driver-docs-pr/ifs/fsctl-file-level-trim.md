---
title: FSCTL_FILE_LEVEL_TRIM 控制代码
description: FSCTL\_文件\_级别\_剪裁控件的代码提供了用于剪裁与文件中的数据范围的方法。
ms.assetid: AD8A7A15-8B53-41DA-A6E4-BD1825C8CB45
keywords:
- FSCTL_FILE_LEVEL_TRIM 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_FILE_LEVEL_TRIM
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1d56c4643f47d9629020aba86dc41794d152eab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365043"
---
# <a name="fsctlfileleveltrim-control-code"></a>FSCTL\_文件\_级别\_剪裁控制代码


**FSCTL\_文件\_级别\_剪裁**控件的代码提供了用于剪裁与文件中的数据范围的方法。 文件剪裁范围将转换为基础的存储设备，使其能够优化其资源的组织提高访问性能。 **FSCTL\_文件\_级别\_剪裁**请求可让要保持在固定大小分配状态时，与虚拟磁盘上释放的数据范围相对应的物理存储的虚拟磁盘文件。

若要执行此操作，调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="instance--in-"></a>*实例\[中\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 调用方的不透明实例指针。 此参数是必需的不能**NULL**。

<a href="" id="fileobject--in-"></a>*FileObject \[in\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 文件指针对象指定要卸除卷。 此参数是必需的不能**NULL**。

<a href="" id="filehandle--in-"></a>*FileHandle \[in\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 要卸除的卷的文件句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
操作的控制代码。 使用**FSCTL\_删除\_覆盖**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区，必须包含**FSCTL\_文件\_级别\_剪裁**结构。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
一个指向[**文件\_级别\_剪裁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim)结构，其中包含一组文件的剪裁区域。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
指向一个可选[**文件\_级别\_剪裁\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim)接收剪裁操作结果的结构。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[出\]*  
大小 （字节），指向的缓冲区*OutputBuffer*参数。 此值必须至少**sizeof**([**文件\_级别\_剪裁\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim)) 如果**文件\_级别\_剪裁\_输出**中包含*OutputBuffer*。 否则，这是设置为 0。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功或可能是下列值之一。

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
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>压缩或加密要剪裁的文件、 输入或输出缓冲区长度是无效的或者，不剪裁的范围指定的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOURCES</strong></p></td>
<td align="left"><p>内部资源分配失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_LOCK_CONFLICT</strong></p></td>
<td align="left"><p>剪裁范围是以前锁定的字节范围的一部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>文件所在的位置的卷未装载。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_PURGE_FAILED</strong></p></td>
<td align="left"><p>缓存清除剪裁范围失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_NO_RANGES_PROCESSED</strong></p></td>
<td align="left"><p>已处理剪裁范围数组中的无范围。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在某些存储设备上执行 trim 可以显著提高其未来的写入性能。 剪裁还在精简预配的存储系统返回的资源添加到分配池。 当虚拟磁盘上删除文件时，不会更改虚拟磁盘文件本身的大小。 释放虚拟磁盘上的数据范围也不剪裁上的物理存储空间虚拟磁盘文件所在的位置。 虚拟磁盘设备可以通知文件系统虚拟磁盘文件的某些数据范围，可以在物理存储设备上使用裁边**FSCTL\_文件\_级别\_剪裁**请求。 文件系统然后将向物理存储发出剪裁请求。 **FSCTL\_文件\_级别\_剪裁**还可以通过管理数据库或内存交换文件的服务应用程序发出请求。

**FSCTL\_文件\_级别\_剪裁**控制代码将尝试剪裁文件从存储设备的所选的字节范围。 字节范围都包含在**范围**数组[**文件\_级别\_剪裁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim)结构。 包含在**范围**数组是一个或多个[**文件\_级别\_剪裁\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim_range)结构。

范围数组中包括重叠的范围不一定是错误条件。 这是依赖于基础存储如何处理范围处理。

为文件系统缓存中的页面中清除已修整的范围。 为了匹配的缓存页大小，剪裁范围的长度调整到的倍数**页上\_大小**。 此外，如果未在页面边界处开始剪裁范围偏移量，它是与下一步的页边界对齐。 这些限制，其偏移量不是对齐的页面或长度不是一个页面时减少剪裁范围长度大小倍数。 剪裁范围长度可能会降低到 0，如果原始长度小于两个页面和偏移量不对齐的页。

如果指定剪裁范围或页调整超出结尾的文件尾 (EOF)，则忽略范围。 但是，一个范围偏移量的对齐之前 EOF 但具有过去的 EOF 的长度扩展将调整到页面大小倍数&lt;= EOF。

压缩或加密的文件不支持文件级剪裁 (文件的工具**特性\_标志\_压缩\_掩码**或**特性\_标志\_加密**属性集)。

文件 trim 之外的任何事务执行。 不能回滚剪裁操作。

使用稀疏文件 (文件的工具**特性\_标志\_SPARSE**属性设置)，忽略的剪裁区域中的文件的未分配部分。

当中包括*OutputBuffer*，则**NumRangesProcessed**的成员[**文件\_级别\_剪裁\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim_output)将指示已成功处理的剪裁区域的数量。 如果剪裁的范围，在处理过程中出现错误**NumRangesProcessed**将指定的结束时间的剩余未处理范围的起始索引**NumRanges**的成员[**文件\_级别\_剪裁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim) -1。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows 8 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FILE\_LEVEL\_TRIM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim)

[**FILE\_LEVEL\_TRIM\_OUTPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim_output)

[**FILE\_LEVEL\_TRIM\_RANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim_range)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






