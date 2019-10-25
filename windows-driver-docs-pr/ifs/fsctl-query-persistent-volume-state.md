---
title: FSCTL_QUERY_PERSISTENT_VOLUME_STATE 控制代码
description: FSCTL\_查询\_永久性\_卷\_状态控制代码检索文件系统卷的持久设置。
ms.assetid: e54a03bb-9329-4095-bb81-857b46fee31c
keywords:
- FSCTL_QUERY_PERSISTENT_VOLUME_STATE 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_QUERY_PERSISTENT_VOLUME_STATE
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 484e45c52465c5cf908ecd6ea0ae23adb88380e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841270"
---
# <a name="fsctl_query_persistent_volume_state-control-code"></a>FSCTL\_查询\_永久性\_卷\_状态控制代码


**FSCTL\_查询\_永久性\_卷\_状态**控制代码检索文件系统卷的持久设置。 持久设置在计算机重新启动之间保留在文件系统卷上。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件系统卷的文件对象指针。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 文件系统卷的文件句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用**FSCTL\_查询\_此操作的持续\_卷\_状态**。

<a href="" id="inputbuffer"></a>*InputBuffer*  
一个指针，指向分配给调用方的[**文件\_FS\_永久性\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)结构。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*参数指向的缓冲区的大小（以字节为单位）。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向分配给调用方的[**文件\_FS 的指针\_永久性\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)结构，该结构接收文件系统卷的持久设置。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer*参数指向的缓冲区的大小（以字节为单位）。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZWFSCONTROLFILE**](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_SUCCESS 或适当的 NTSTATUS 值，如以下之一：

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
<td align="left"><p><strong>STATUS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>调用方在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)"><strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>的<strong>version</strong>成员中指定了不正确的版本号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>文件系统卷不是打开的用户卷，或调用方在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)"><strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>的<strong>FlagMask</strong>成员中指定了无效的标志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>InputBuffer</em>参数指向的缓冲区不够大（即，缓冲区小于<strong>sizeof</strong>（FILE_FS_PERSISTENT_VOLUME_INFORMATION））。 在这种情况下，不返回持久性设置数据。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>调用方无法访问文件系统卷。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>文件系统卷已卸除。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_TOO_LATE</strong></p></td>
<td align="left"><p>文件系统卷已关闭。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_MEDIA_WRITE_PROTECTED</strong></p></td>
<td align="left"><p>文件系统卷为只读。</p></td>
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
<td align="left"><p>版本</p></td>
<td align="left"><p>可从 Windows 7 开始使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**文件\_FS\_永久性\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






