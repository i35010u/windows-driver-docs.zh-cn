---
title: FSCTL_MARK_VOLUME_DIRTY 控制代码
description: FSCTL \_ 标记 \_ 批量 \_ 脏控制代码将指定的卷标记为脏卷，这会触发在下一次系统重新启动期间在卷上运行 Autochk.exe。
keywords:
- FSCTL_MARK_VOLUME_DIRTY 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_MARK_VOLUME_DIRTY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a59824cca67676f24f9d79539df64d7f309398f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808341"
---
# <a name="fsctl_mark_volume_dirty-control-code"></a>FSCTL \_ 标记 \_ 卷 \_ 脏控制代码


**FSCTL \_ 标记 \_ 批量 \_ 脏** 控制代码将指定的卷标记为脏卷，这会触发在下一次系统重新启动期间在卷上运行 Autochk.exe。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**Parameters**

<a href="" id="instance"></a>*实例*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 指向启动 FSCTL 请求的微筛选器驱动程序实例的不透明实例指针。

<a href="" id="fileobject"></a>*FileObject*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 一个文件指针对象，用于指定要标记为已更新的卷。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 要标记为已更新的卷的句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 在此操作中使用 **FSCTL \_ 标记 \_ 批量 \_ 更新** 。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用。 设置为 **NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不与此操作一起使用。 设置为0。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不与此操作一起使用。 设置为 **NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不与此操作一起使用。 设置为0。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或 [**ZWFSCONTROLFILE**](/previous-versions/ff566462(v=vs.85))例程返回状态 \_ 成功或适当的 NTSTATUS 值。

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
<td align="left"><p><em>FileObject</em>或<em>FileHandle</em>不表示有效的卷句柄，或者其他参数无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>调用方没有 SE_MANAGE_VOLUME 的访问权限。</p></td>
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

 

<a name="remarks"></a>备注
-------

* * ReFS： * * 此代码不受支持。

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
<td align="left">Ntifs (包含 FltKernel 或 Ntifs) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FSCTL \_ 的 \_ 卷已 \_ 更新**](fsctl-is-volume-dirty.md)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

 

