---
title: FSCTL_OFFLOAD_READ 控制代码
description: FSCTL\_卸载\_读取控件代码启动一个卸载读取有关支持卸载的存储系统中的数据块，请阅读基元。
ms.assetid: D9A22A8F-9B7E-4BF7-8FBD-267BE4C8DC59
keywords:
- FSCTL_OFFLOAD_READ 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_OFFLOAD_READ
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0a233425428aa634d23743dd825e95e4165a77e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391781"
---
# <a name="fsctloffloadread-control-code"></a>FSCTL\_卸载\_读取控制代码


**FSCTL\_卸载\_读取**控件代码启动一个卸载读取有关支持卸载的存储系统中的数据块，请阅读基元。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="instance--in-"></a>*实例\[中\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 调用方不透明实例指针。 此参数是必需的不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[in\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 文件指针对象指定要读取的文件。 此参数是必需的不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[in\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 要读取的文件的文件句柄。 此参数是必需的不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
操作的控制代码。 使用**FSCTL\_卸载\_读取**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
一个指向[ **FSCTL\_卸载\_读取\_输入**](https://msdn.microsoft.com/library/windows/hardware/hh451104)结构，其中包含的大小和要读取的数据块的偏移量。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
大小 （字节） 通过指向的缓冲区*InputBuffer*。 此值是**sizeof**(FSCTL\_卸载\_读取\_输入)。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
一个指向[ **FSCTL\_卸载\_读取\_输出**](https://msdn.microsoft.com/library/windows/hardware/hh451109)结构，它接收的卸载会读取操作。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[出\]*  
大小 （字节） 通过指向的缓冲区*OutputBuffer*参数。 此值必须至少**sizeof**(FSCTL\_卸载\_读取\_输出)。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功如果操作成功。 否则，相应的函数可能返回以下 NTSTATUS 值之一。

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
<p><em>InputBufferLength</em> &lt; <strong>sizeof</strong>(FSCTL_OFFLOAD_READ_INPUT)。</p>
<p>-或-</p>
<p>一个或多个的这些成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451104" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_INPUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451104)"> <strong>FSCTL_OFFLOAD_READ_INPUT</strong> </a>不正确：</p>
<strong>FileOffset</strong>不是卷的逻辑扇区大小的倍数。
<strong>CopyLength</strong>不是卷的逻辑扇区大小的倍数。
<strong>大小</strong>的大小<a href="https://msdn.microsoft.com/library/windows/hardware/hh451104" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_INPUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451104)"> <strong>FSCTL_OFFLOAD_READ_INPUT</strong> </a>结构。
<strong>FileOffset</strong> + <strong>CopyLength</strong> &gt; <strong>MAXULONGLONG</strong>。</td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>文件系统卷已卸除。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>卸载读取此卷上不支持操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_OFFLOAD_READ_FILE_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>不支持请求的文件类型。 卸载操作不支持对这些文件类型：</p>
<ul>
<li>事务处理的文件 (TxF)</li>
<li>非用户文件</li>
<li>压缩文件</li>
<li>加密的文件</li>
<li>稀疏文件</li>
<li>NTFS 元数据文件</li>
</ul></td>
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
<td align="left"><p>由于当前没有足够的读取访问的文件锁定状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_END_OF_FILE</strong></p></td>
<td align="left"><p><strong>FileOffset</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451104" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_INPUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451104)"> <strong>FSCTL_OFFLOAD_READ_INPUT</strong> </a>开始后端的文件 (EOF)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_DISMOUNTED_VOLUME</strong></p></td>
<td align="left"><p>已卸载卷上不能读取卸载。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOUCES</strong></p></td>
<td align="left"><p>没有足够的资源，可完成该请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>OutputBufferLength</em>太小<em>OutputBuffer</em>接收<a href="https://msdn.microsoft.com/library/windows/hardware/hh451109" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_OUTPUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451109)"> <strong>FSCTL_OFFLOAD_READ_OUTPUT</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

普通文件仅可读取的卸载。 请参阅的说明**状态\_卸载\_读取\_文件\_不\_支持**有关不支持的文件类型的列表。

很可能读取启动超出有效数据长度 (VDL)，且仅限于 EOF。

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


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_OFFLOAD\_READ\_INPUT**](https://msdn.microsoft.com/library/windows/hardware/hh451104)

[**FSCTL\_卸载\_读取\_输出**](https://msdn.microsoft.com/library/windows/hardware/hh451109)

 

 






