---
title: FSCTL_INVALIDATE_VOLUMES 控制代码
description: FSCTL\_使\_的卷控制代码能够查找并删除设备上装入的所有卷（由指定的文件对象或句柄表示）。
ms.assetid: 26B7EBA2-F3A9-4E5A-961C-C1857AA4FF33
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
ms.openlocfilehash: df174ddb9ebd9b9e81f0be46285b10d4aab1c0ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841298"
---
# <a name="fsctl_invalidate_volumes-control-code"></a>FSCTL\_使\_的卷控制代码无效


**FSCTL\_使\_的卷**控制代码能够查找并删除设备上装入的所有卷（由指定的文件对象或句柄表示）。

要执行此操作，微筛选器驱动程序使用以下[**参数调用**](https://msdn.microsoft.com/library/windows/hardware/ff566462) [**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)、文件系统、重定向程序和旧式文件系统筛选器驱动程序。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
设备的句柄。 若要获取设备句柄，请调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数。

<a href="" id="filehandle"></a>*FileHandle*  
设备的句柄。 若要获取设备句柄，请调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用**FSCTL\_使此操作\_卷无效**。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用;设置为**NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不与此操作一起使用;设置为零。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不与此操作一起使用;设置为**NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------

如果操作成功，则[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)和[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回状态\_成功，或者为适当的 NTSTATUS 值。

<a name="remarks"></a>备注
-------

FSCTL\_会使\_的卷发送到文件系统的控件（即命名）设备对象，而不是发送到卷设备对象。 有关控制设备对象的详细信息，请参阅[创建控制设备对象](https://docs.microsoft.com/windows-hardware/drivers/ifs/creating-the-control-device-object)。

FAT 和 NTFS 文件系统通过响应 IRP\_MJ\_PNP/IRP\_MN\_意外\_删除来处理意外删除。

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
<td align="left">Ntifs （包括 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






