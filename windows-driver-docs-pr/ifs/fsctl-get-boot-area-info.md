---
title: FSCTL_GET_BOOT_AREA_INFO 控制代码
description: FSCTL\_获取\_BOOT\_区域\_信息控制代码会检索卷的引导扇区的位置。
ms.assetid: 0e842609-65f9-4a61-ab7f-f525650dfd14
keywords:
- FSCTL_GET_BOOT_AREA_INFO 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_GET_BOOT_AREA_INFO
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65a58b4a2a751609de947995ad3996d84ed73eee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365039"
---
# <a name="fsctlgetbootareainfo-control-code"></a>FSCTL\_获取\_BOOT\_区域\_信息控制代码


**FSCTL\_获取\_引导\_区域\_信息**控制代码检索卷的引导扇区的位置。

若要执行此操作，调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)函数或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)以下函数参数。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 为其卷的文件对象指针**FSCTL\_获取\_引导\_区域\_信息**将检索启动信息。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 为其卷的文件句柄**FSCTL\_获取\_引导\_区域\_信息**将检索启动信息。 此参数是必需的不能**NULL**。

必须使用 SE 打开此句柄\_管理\_卷\_名称访问权限。 有关详细信息，请参阅[文件安全和访问权限](https://docs.microsoft.com/windows/desktop/FileIO/file-security-and-access-rights)。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
该操作控制代码。 使用**FSCTL\_获取\_引导\_区域\_信息**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不使用与此操作。 设置为**NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不使用与此操作。 设置为零。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
一个指向[ **BOOT\_区域\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_boot_area_info)结构，它接收的卷的引导扇区的位置。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
输出缓冲区，以字节为单位的大小。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回适当的 NTSTATUS 值如以下之一：

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
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>操作成功。 OutputBuffer 包含一个指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_boot_area_info" data-raw-source="[&lt;strong&gt;BOOT_AREA_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_boot_area_info)"> <strong>BOOT_AREA_INFO</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>参数不是有效，则为例如，使用的句柄不是有效的批量句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>OutputBuffer 不足够大的结果。 已向缓冲区不写入任何信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>用户没有 SE_MANAGE_VOLUME 访问。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**FSCTL\_获取\_BOOT\_区域\_信息**可 FastFAT 和 exFAT 的设备上使用的控制代码。 此功能支持的设备，例如闪存驱动器使用 BitLocker。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows Server 2008 R2, Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)

 

 






