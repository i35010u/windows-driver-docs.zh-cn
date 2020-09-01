---
title: FSCTL_DISMOUNT_VOLUME 控制代码
description: '\_ \_ 无论卷是否正在使用中，FSCTL 卸载卷控制代码都将尝试卸除卷。'
ms.assetid: edfff768-3bb3-4b8a-b982-80797ac116fd
keywords:
- FSCTL_DISMOUNT_VOLUME 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: f0742fe14b42b5ca3bd21e19b34e5e17785a3491
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066178"
---
# <a name="fsctl_dismount_volume-control-code"></a>FSCTL \_ 卸除 \_ 音量控制代码


无论卷是否正在使用中， **FSCTL \_ 卸载 \_ 卷** 控制代码都将尝试卸除卷。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**参数**

<a href="" id="instance"></a>*实例*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件指针对象，指定要卸除的卷。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle--in-"></a>*FileHandle \[\]*  
仅[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 要卸除的卷的文件句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[\]*  
操作的控制代码。 将 **FSCTL \_ 卸除 \_ 卷** 用于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用。 设置为 **NULL**。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[\]*  
不与此操作一起使用。 设置为零。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[\]*  
不与此操作一起使用。 设置为 **NULL**。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength \[\]*  
不与此操作一起使用。 设置为零。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 返回状态 \_ SUCCESS 或适当的 NTSTATUS 值。

<a name="remarks"></a>备注
-------

不管是否有任何其他进程正在使用该卷， **FSCTL \_ 卸载 \_ 卷** 控制代码都将尝试卸载该卷，如果这些进程未在卷上持有锁，则可能会产生不可预知的结果。 有关锁定卷的信息，请参阅 [**FSCTL \_ LOCK \_ volume**](/windows/desktop/api/winioctl/ni-winioctl-fsctl_lock_volume)。

操作系统不检测未装入的卷。 如果尝试访问未装入的卷，则操作系统将尝试装入该卷。 例如，对 [**GetLogicalDrives**](/windows/desktop/api/fileapi/nf-fileapi-getlogicaldrives) 的调用会触发操作系统来装入未装入的卷。

传递给[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))的*FileHandle*句柄必须是为直接访问而打开的卷的句柄。 若要检索卷句柄，请调用[**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile) ，并将*ObjectAttributes*参数设置为以下形式的*ObjectName* ： * \\ \\ 。 \\X：* 其中*x*是卷、软盘驱动器或 cd-rom 驱动器的驱动器号。 应用程序还必须 \_ \_ \_ \_ 在**ZwCreateFile**的*ShareAccess*参数中指定文件共享读取和文件共享写入标志。

如果指定的卷是系统卷或包含页面文件，则操作将失败。

如果指定的卷被另一个进程锁定，则该操作将失败。

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
<td align="left">Ntifs</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltCreateFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

 

