---
title: FSCTL_DISMOUNT_VOLUME 控制代码
description: FSCTL\_卸除\_卷控件代码尝试卸除卷而不考虑卷是否在使用中。
ms.assetid: edfff768-3bb3-4b8a-b982-80797ac116fd
keywords:
- FSCTL_DISMOUNT_VOLUME 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_DISMOUNT_VOLUME
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6112d6332da7043822789316854779b26a20bfb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365067"
---
# <a name="fsctldismountvolume-control-code"></a>FSCTL\_卸除\_卷控制代码


**FSCTL\_卸除\_卷**控件代码尝试卸除卷而不考虑卷是否在使用中。

若要执行此操作，调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="instance"></a>*实例*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 调用方的不透明实例指针。 此参数是必需的不能**NULL**。

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 文件指针对象指定要卸除卷。 此参数是必需的不能**NULL**。

<a href="" id="filehandle--in-"></a>*FileHandle \[in\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 要卸除的卷的文件句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
操作的控制代码。 使用**FSCTL\_卸除\_卷**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不使用与此操作。 设置为**NULL**。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
不使用与此操作。 设置为零。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
不使用与此操作。 设置为**NULL**。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength \[in\]*  
不使用与此操作。 设置为零。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功或适当的 NTSTATUS 值。

<a name="remarks"></a>备注
-------

**FSCTL\_卸除\_卷**控制代码将尝试卸除卷而不考虑任何其他进程是否正在使用该卷，这会产生不可预知的结果，这些进程，如果它们不具有在卷上的锁。 有关锁定卷的信息，请参阅[ **FSCTL\_锁\_卷**](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_lock_volume)。

操作系统不检测到未装入的卷。 如果尝试访问未装入的卷，操作系统将依次尝试装入卷。 例如，调用[ **GetLogicalDrives** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-getlogicaldrives)触发要卸载的卷装载的操作系统。

*FileHandle*句柄传递给[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)必须是对卷进行直接访问而打开的句柄。 若要检索卷句柄，请调用[ **ZwCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)与*ObjectAttributes*参数设置为*ObjectName*的以下窗体：  *\\ \\。\\X:* 其中*X*是卷、 软盘驱动器或 CD-ROM 驱动器的驱动器号。 应用程序还必须指定的文件\_共享\_读取和文件\_共享\_写标志中*ShareAccess*参数**ZwCreateFile**.

如果指定的卷是系统卷或包含页面文件，则操作将失败。

如果指定的卷被另一个进程锁定，则操作将失败。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






