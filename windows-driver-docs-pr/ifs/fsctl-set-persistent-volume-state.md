---
title: FSCTL_SET_PERSISTENT_VOLUME_STATE 控制代码
description: FSCTL \_ SET \_ 永久性 \_ 卷 \_ 状态控制代码设置文件系统卷的持久设置。 持久设置在计算机重新启动之间保留在文件系统卷上。
ms.assetid: 1670f3e9-c2f4-4696-a76e-bcf1bad5dc43
keywords:
- FSCTL_SET_PERSISTENT_VOLUME_STATE 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_SET_PERSISTENT_VOLUME_STATE
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1c93ad796d999428af0ebd5447025637fe2cd24
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105428"
---
# <a name="fsctl_set_persistent_volume_state-control-code"></a>FSCTL \_ 设置 \_ 永久性 \_ 卷 \_ 状态控制代码


**FSCTL \_ SET \_ 永久性 \_ 卷 \_ 状态**控制代码设置文件系统卷的持久设置。 持久设置在计算机重新启动之间保留在文件系统卷上。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**参数**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件系统卷的文件对象指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 文件系统卷的文件句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL 为此操作 ** \_ 设置 \_ 永久 \_ 卷 \_ 状态** 。

<a href="" id="inputbuffer"></a>*InputBuffer*  
一个指针，指向分配给调用方的 [**文件 \_ FS \_ 永久性 \_ 卷 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information) 结构，该结构包含文件系统卷的持久设置。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*参数指向的缓冲区的大小（以字节为单位）。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不与此操作一起使用;设置为 **NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不与此操作一起使用;设置为零。

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
<td align="left"><p>请求的注册表设置不是每个卷，或调用方在<a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)"><strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>的<strong>版本</strong>成员中指定了不正确的版本号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>文件系统卷不是打开的用户卷，或调用方在<a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)"><strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>的<strong>FlagMask</strong>成员中指定了无效的标志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>InputBuffer</em>参数指向的缓冲区不够大，无法保存持久的设置数据。 在这种情况下，不设置持久性设置数据。 这是一个错误代码。</p></td>
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

## <a name="see-also"></a>请参阅


[**文件 \_ FS \_ 永久性 \_ 卷 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

