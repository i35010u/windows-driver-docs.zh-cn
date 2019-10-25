---
title: FSCTL_MARK_VOLUME_DIRTY 控制代码
description: FSCTL\_将\_批量\_脏控制代码标记为已更新，这将在下一次系统重新启动期间触发 Autochk 在卷上运行。
ms.assetid: 9062b212-fc8a-4467-b32f-047fc3702445
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
ms.openlocfilehash: d7e7788529834de6336cf49c88f095f958913efd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841285"
---
# <a name="fsctl_mark_volume_dirty-control-code"></a>FSCTL\_标记\_卷\_脏控制代码


**FSCTL\_将\_批量\_脏**控制代码标记为已更新，这将在下一次系统重新启动期间触发 Autochk 在卷上运行。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="instance"></a>*实例*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 指向启动 FSCTL 请求的微筛选器驱动程序实例的不透明实例指针。

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 一个文件指针对象，用于指定要标记为已更新的卷。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 要标记为已更新的卷的句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用**FSCTL\_标记\_卷\_** 为此操作更新。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用。 设置为**NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不与此操作一起使用。 设置为0。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不与此操作一起使用。 设置为**NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不与此操作一起使用。 设置为0。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)例程返回\_SUCCESS 或适当的 NTSTATUS 值的状态。

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
<td align="left"><p>调用方不具有 SE_MANAGE_VOLUME 访问权限。</p></td>
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

**ReFS：  **此代码不受支持。

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
<td align="left">Ntifs （包括 FltKernel 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FSCTL\_\_卷\_更新**](fsctl-is-volume-dirty.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






