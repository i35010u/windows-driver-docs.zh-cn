---
title: FSCTL_OFFLOAD_WRITE 控制代码
description: FSCTL\_卸载\_编写控件代码中支持卸载写入基元的存储系统启动的数据块的卸载写入。
ms.assetid: A40C6D4C-D31D-423E-B7B0-51151EEDD30F
keywords:
- FSCTL_OFFLOAD_WRITE 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_OFFLOAD_WRITE
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f53c1cdc57d5402d1955865efede22d4039a548
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380119"
---
# <a name="fsctloffloadwrite-control-code"></a>FSCTL\_卸载\_编写控件的代码


**FSCTL\_卸载\_编写**控件代码中支持卸载写入基元的存储系统启动的数据块的卸载写入。

若要执行此操作，微筛选器驱动程序调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)与以下参数和文件系统中，重定向程序和旧的文件系统筛选驱动程序调用[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="instance--in-"></a>*实例\[中\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 调用方不透明实例指针。 此参数是必需的不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[in\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 文件指针对象指定要写入的文件。 此参数是必需的不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[in\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 要写入的文件的文件句柄。 此参数是必需的不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
操作的控制代码。 使用**FSCTL\_卸载\_编写**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
一个指向[ **FSCTL\_卸载\_编写\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_input)结构，其中包含的大小和要读取的数据块的偏移量。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
大小 （字节） 通过指向的缓冲区*InputBuffer*。 此值是**sizeof**(FSCTL\_卸载\_编写\_输入)。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
一个指向[ **FSCTL\_卸载\_编写\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_input)结构，其中包含的大小和要读取的数据块的偏移量。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[出\]*  
大小 （字节） 通过指向的缓冲区*OutputBuffer*参数。 此值必须至少**sizeof**(FSCTL\_卸载\_读取\_输出)。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功如果操作成功。 否则，相应的函数可能返回以下 NTSTATUS 值之一。

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
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>指定的句柄不是有效的文件句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>文件大小小于 PAGE_SIZE。</p>
<p>-或-</p>
<p><em>InputBufferLength</em> &lt; <strong>sizeof</strong>(FSCTL_OFFLOAD_WRITE_INPUT)。</p>
<p>-或-</p>
<p>一个或多个的这些成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_input)"> <strong>FSCTL_OFFLOAD_WRITE_INPUT</strong> </a>不正确：</p>
<strong>FileOffset</strong>不是卷的逻辑扇区大小的倍数。
<strong>CopyLength</strong>不是卷的逻辑扇区大小的倍数。
<strong>TransferOffset</strong>不是卷的逻辑扇区大小的倍数。
<strong>大小</strong>的大小<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_input)"> <strong>FSCTL_OFFLOAD_WRITE_INPUT</strong> </a>结构。
<strong>FileOffset</strong> &gt;文件的有效的数据长度 (VDL)。
<strong>FileOffset</strong> + <strong>CopyLength</strong> &gt; <strong>MAXULONGLONG</strong>。</td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>卸载读取此卷上不支持操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_OFFLOAD_WRITE_FILE_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>不支持请求的文件类型。 卸载操作不支持对这些文件类型：</p>
<ul>
<li>事务处理的文件 (TxF)</li>
<li>非用户文件</li>
<li>压缩文件</li>
<li>稀疏文件</li>
<li>加密的文件</li>
<li>NTFS 元数据文件</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_TOO_LATE</strong></p></td>
<td align="left"><p>写入操作试图为卷后已被卸载。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_FILE_DELETED</strong></p></td>
<td align="left"><p>此文件的数据流是无效的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_CLOSED</strong></p></td>
<td align="left"><p>关闭文件句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_HANDLE</strong></p></td>
<td align="left"><p>指定的文件句柄无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_LOCK_CONFLICT</strong></p></td>
<td align="left"><p>由于当前文件锁定状态，不能授予读取或写入访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_END_OF_FILE</strong></p></td>
<td align="left"><p><strong>FileOffset</strong>的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_input)"> <strong>FSCTL_OFFLOAD_WRITE_INPUT</strong> </a>开始后端的文件 (EOF)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_DISMOUNTED_VOLUME</strong></p></td>
<td align="left"><p>卸载写不能已卸除卷上。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_MEDIA_WRITE_PROTECTED</strong></p></td>
<td align="left"><p>该卷为只读。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOUCES</strong></p></td>
<td align="left"><p>没有足够的资源，可完成该请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>InputBufferLength</em>太小<em>InputBuffer</em>包含<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_input)"> <strong>FSCTL_OFFLOAD_WRITE_INPUT</strong> </a>结构。</p>
<p>-或-</p>
<p><em>OutputBufferLength</em>太小<em>OutputBuffer</em>接收<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_output" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_OUTPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_output)"> <strong>FSCTL_OFFLOAD_WRITE_OUTPUT</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

普通文件仅可读取的卸载。 请参阅的说明**状态\_卸载\_编写\_文件\_不\_支持**有关不支持的文件类型的列表。

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
<td align="left"><p>从 Windows 8 开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_OFFLOAD\_WRITE\_INPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_input)

[**FSCTL\_卸载\_编写\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_output)

 

 






