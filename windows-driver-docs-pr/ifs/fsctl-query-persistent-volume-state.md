---
title: FSCTL_QUERY_PERSISTENT_VOLUME_STATE 控制代码
description: FSCTL \_ 查询 \_ 永久性 \_ 卷 \_ 状态控制代码检索文件系统卷的持久设置。
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
ms.openlocfilehash: 32ce85bba91207a228d9661d7cb7109680aa4bd3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104200"
---
# <a name="fsctl_query_persistent_volume_state-control-code"></a>FSCTL \_ 查询 \_ 永久性 \_ 卷 \_ 状态控制代码


**FSCTL \_ 查询 \_ 永久性 \_ 卷 \_ 状态**控制代码检索文件系统卷的持久设置。 持久设置在计算机重新启动之间保留在文件系统卷上。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**参数**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件系统卷的文件对象指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 文件系统卷的文件句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 将 **FSCTL \_ 查询 \_ 永久 \_ 卷 \_ 状态** 用于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
一个指针，指向分配给调用方的 [**文件 \_ FS \_ 永久性 \_ 卷 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information) 结构。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*参数指向的缓冲区的大小（以字节为单位）。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
一个指针，指向为文件系统卷接收持久设置的调用方分配的 [**文件 \_ FS \_ 永久性 \_ 卷 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information) 结构。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer*参数指向的缓冲区的大小（以字节为单位）。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 返回状态 \_ "成功" 或相应的 NTSTATUS 值，如下所示：

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
<td align="left"><p><strong>STATUS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>调用方在<a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)"><strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>的<strong>版本</strong>成员中指定了不正确的版本号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>文件系统卷不是打开的用户卷，或调用方在<a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)"><strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>的<strong>FlagMask</strong>成员中指定了无效的标志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>InputBuffer</em>参数指向的缓冲区不够大 (也就是说，缓冲区小于<strong>sizeof</strong> (FILE_FS_PERSISTENT_VOLUME_INFORMATION) # A3。 在这种情况下，不返回持久性设置数据。 这是一个错误代码。</p></td>
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
<td align="left">Ntifs (包含 Ntifs) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**文件 \_ FS \_ 永久性 \_ 卷 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

