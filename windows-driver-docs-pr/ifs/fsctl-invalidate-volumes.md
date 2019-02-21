---
title: FSCTL_INVALIDATE_VOLUMES 控制代码
description: FSCTL\_INVALIDATE\_卷控制代码查找并删除装载到指定的文件对象或句柄所表示的设备上的所有卷。
ms.assetid: 26B7EBA2-F3A9-4E5A-961C-C1857AA4FF33
keywords:
- FSCTL_INVALIDATE_VOLUMES 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: 6ffb8ee3a4b4ba5d60aa66d23f1e33701df0bd41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524040"
---
# <a name="fsctlinvalidatevolumes-control-code"></a>FSCTL\_INVALIDATE\_卷控制代码


**FSCTL\_INVALIDATE\_卷**控制代码查找并删除装载到指定的文件对象或句柄所表示的设备上的所有卷。

若要执行此操作，微筛选器驱动程序调用[ **FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)，和文件系统、 重定向程序，以及传统文件系统筛选器驱动程序调用[ **ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)，使用以下参数。

**参数**

<a href="" id="fileobject"></a>*FileObject*  
设备的句柄。 若要获取设备句柄，请调用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)函数。

<a href="" id="filehandle"></a>*FileHandle*  
设备的句柄。 若要获取设备句柄，请调用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)函数。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用**FSCTL\_INVALIDATE\_卷**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不用于此操作;设置为**NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不用于此操作;设置为零。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不用于此操作;设置为**NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不用于此操作;设置为零。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)并[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回状态\_如果操作成功的成功或适当的 NTSTATUS 值。

<a name="remarks"></a>备注
-------

FSCTL\_INVALIDATE\_卷发送到文件系统的控件 （名为） 的设备对象，而不是卷设备对象。 控制设备对象的详细信息，请参阅[创建控件设备对象](https://msdn.microsoft.com/library/windows/hardware/ff540060)。

FAT 和 NTFS 文件系统处理意外删除回应 IRP\_MJ\_PNP/IRP\_MN\_惊讶\_删除。

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
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






