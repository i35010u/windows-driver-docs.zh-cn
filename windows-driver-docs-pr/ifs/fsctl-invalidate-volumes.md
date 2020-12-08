---
title: FSCTL_INVALIDATE_VOLUMES 控制代码
description: FSCTL \_ 使 \_ 卷控制代码无效查找并删除设备上装入的所有卷（由指定的文件对象或句柄表示）。
keywords:
- FSCTL_INVALIDATE_VOLUMES 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_INVALIDATE_VOLUMES
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6af05a13c573c5b8d1ef8e90f06b461169e4dca5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808361"
---
# <a name="fsctl_invalidate_volumes-control-code"></a>FSCTL \_ 使 \_ 卷控制代码无效


**FSCTL \_ 使 \_ 卷** 控制代码无效查找并删除设备上装入的所有卷（由指定的文件对象或句柄表示）。

要执行此操作，微筛选器驱动程序使用以下 [**参数调用**](/previous-versions/ff566462(v=vs.85)) [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)、文件系统、重定向程序和旧式文件系统筛选器驱动程序。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
设备的句柄。 若要获取设备句柄，请调用 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 函数。

<a href="" id="filehandle"></a>*FileHandle*  
设备的句柄。 若要获取设备句柄，请调用 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 函数。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 **FSCTL \_ 使 \_ 卷失效** ，以便执行此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用;设置为 **NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不与此操作一起使用;设置为零。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不与此操作一起使用;设置为 **NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------

如果操作成功，则 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)和 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))返回状态 \_ SUCCESS，否则返回相应的 NTSTATUS 值。

<a name="remarks"></a>备注
-------

FSCTL 会将 \_ \_ 卷发送到文件系统的控件 (即) 设备对象，而不是卷设备对象。 有关控制设备对象的详细信息，请参阅 [创建控制设备对象](./creating-the-control-device-object.md)。

FAT 和 NTFS 文件系统通过响应 IRP \_ MJ \_ PNP/IRP \_ MN \_ 意外 \_ 删除来处理意外删除。

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
<td align="left">Ntifs (包含 Ntifs) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

 

