---
title: FSCTL_FILE_LEVEL_TRIM 控制代码
description: FSCTL\_文件\_级别\_剪裁控制代码提供了一种在文件中使用剪裁数据范围的方法。
ms.assetid: AD8A7A15-8B53-41DA-A6E4-BD1825C8CB45
keywords:
- FSCTL_FILE_LEVEL_TRIM 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: 86ddb803ece874a8a1b4c386510214329106523e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841319"
---
# <a name="fsctl_file_level_trim-control-code"></a>FSCTL\_文件\_级别\_剪裁控制代码


**FSCTL\_文件\_级别\_剪裁**控制代码提供了一种在文件中使用剪裁数据范围的方法。 文件剪裁范围会转换为底层存储设备，使其能够优化其资源组织以提高访问性能。 **FSCTL\_文件\_级别\_TRIM**请求允许虚拟磁盘文件保持固定大小，同时剪裁物理存储与虚拟磁盘上释放的数据区域相对应。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为**NULL**。

<a href="" id="fileobject--in-"></a>*FileObject \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件指针对象，指定要卸除的卷。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle--in-"></a> *\]中的 FileHandle \[*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 要卸除的卷的文件句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode--in-"></a> *\]中的 FsControlCode \[*  
操作的控制代码。 使用**FSCTL\_删除**此操作的\_重叠。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区的指针，该指针必须包含**FSCTL\_文件\_级别\_剪裁**结构。

<a href="" id="inputbufferlength--in-"></a> *\]中的 InputBufferLength \[*  
指向[**文件\_级别的指针\_剪裁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)结构，其中包含文件的剪裁范围数组。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
指向可选[**文件\_级别的指针\_剪裁\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)结构，该结构接收剪裁操作的结果。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[out\]*  
*OutputBuffer*参数指向的缓冲区的大小（以字节为单位）。 如果*OutputBuffer*中包含**文件\_级别\_剪裁\_输出**，此值必须至少为**sizeof**（[**文件\_级别\_剪裁\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)）。 否则，此设置为0。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回状态\_SUCCESS 或可能是以下值之一。

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
<td align="left"><p>要剪裁的文件已压缩或加密，输入或输出缓冲区长度无效，或者未指定剪裁范围。</p></td>
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
<td align="left"><p>文件所在的卷未装入。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_PURGE_FAILED</strong></p></td>
<td align="left"><p>清除范围的缓存清除失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_NO_RANGES_PROCESSED</strong></p></td>
<td align="left"><p>未处理剪裁范围数组中的任何范围。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在某些存储设备上执行修剪可显著提高其未来的写入性能。 Trim 还会将资源返回到已精简预配的存储系统中的分配池。 在虚拟磁盘上删除文件时，虚拟磁盘文件本身的大小不会更改。 虚拟磁盘上释放的数据范围不会在虚拟磁盘文件所在的物理存储上进行修剪。 虚拟磁盘设备可以通知文件系统虚拟磁盘文件中的某些数据范围可以在具有**FSCTL\_文件\_级别\_剪裁**请求的物理存储设备上剪裁。 然后，文件系统将向物理存储发出剪裁请求。 **FSCTL\_文件\_级别\_剪裁**请求也可能由管理数据库或内存交换文件的服务应用程序发出。

**FSCTL\_文件\_级别\_剪裁**控制代码将尝试从存储设备中剪裁文件的所选字节范围。 字节范围包含在[**文件\_级别\_剪裁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)结构中的**范围**数组中。 **范围**数组包含一个或多个[**文件\_级别\_剪裁\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim_range)结构。

在范围数组中包括重叠范围并不一定是错误条件。 这取决于基础存储处理区处理的方式。

剪裁范围将作为页面从文件系统缓存中清除。 为了匹配缓存页面大小，会将剪裁范围的长度向下调整到**页面\_大小**的倍数。 此外，如果剪裁范围偏移量不是以页面边界开始，则与下一页边界对齐。 使用这些约束时，如果偏移量不是页面对齐或长度不是页面大小，则剪裁范围长度将减少。 如果原始长度小于两页并且偏移量不是页面对齐，则剪裁范围长度可能会减小到0。

如果指定了剪裁范围或在文件尾（EOF）之后调整了页面，则将忽略范围。 但是，在 EOF 之前对齐但长度超过 EOF 的范围偏移量将调整为多 &lt;= EOF 的页大小。

压缩文件或加密文件不支持文件级别剪裁（\_带有特性的文件 **\_压缩\_掩码**或**特性\_标记\_加密**的属性集）。

文件修剪是在任何事务的外部执行的。 无法回滚剪裁操作。

对于稀疏文件（具有**特性\_标志的文件\_稀疏**特性集），将忽略该文件的未分配部分中的剪裁范围。

当包含在*OutputBuffer*中时， [ **\_剪裁\_输出的文件\_级别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim_output)的**NumRangesProcessed**成员将指示成功处理的剪裁范围数。 如果在处理剪裁范围期间发生错误，则**NumRangesProcessed**将指定剩余未处理范围的起始索引，以在[**文件\_级别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)的**NumRanges**成员结尾，以\_trim-1 结束。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 8 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs 或 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**文件\_级别\_剪裁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)

[**文件\_级别\_剪裁\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim_output)

[ **\_剪裁\_范围的文件\_级别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim_range)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






