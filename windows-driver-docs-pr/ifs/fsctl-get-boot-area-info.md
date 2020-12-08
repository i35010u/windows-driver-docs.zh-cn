---
title: FSCTL_GET_BOOT_AREA_INFO 控制代码
description: FSCTL \_ 获取 \_ 启动 \_ 区域 \_ 信息控制代码检索卷的启动扇区的位置。
keywords:
- FSCTL_GET_BOOT_AREA_INFO 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: 481bedc7467556a40338d4142ee84be4fb0ba599
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808383"
---
# <a name="fsctl_get_boot_area_info-control-code"></a>FSCTL \_ 获取 \_ 启动 \_ 区域 \_ 信息控制代码


**FSCTL \_ 获取 \_ 启动 \_ 区域 \_ 信息** 控制代码检索卷的启动扇区的位置。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 函数或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 函数。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 **FSCTL \_ 获取 \_ 启动 \_ 区域 \_ 信息** 的卷的文件对象指针将检索启动信息。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 卷的文件句柄， **FSCTL \_ 获取 \_ 启动 \_ 区域 \_ 信息** 将检索启动信息。 此参数是必需的，不能为 **NULL**。

必须使用 SE \_ 管理 \_ 卷 \_ 名访问权限打开此句柄。 有关详细信息，请参阅 [文件安全性和访问权限](/windows/desktop/FileIO/file-security-and-access-rights)。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 **FSCTL 获取此操作的 \_ \_ 启动 \_ 区域 \_ 信息** 。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用。 设置为 **NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不与此操作一起使用。 设置为零。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向 [**启动 \_ 区域 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_boot_area_info) 结构的指针，该结构接收卷的启动扇区的位置。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
输出缓冲区的大小（以字节为单位）。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 返回相应的 NTSTATUS 值，如下所示：

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
<td align="left"><p>操作成功。 OutputBuffer 包含指向 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_boot_area_info" data-raw-source="[&lt;strong&gt;BOOT_AREA_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_boot_area_info)"><strong>BOOT_AREA_INFO</strong></a> 结构的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>参数无效;例如，使用的句柄不是有效的卷句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>OutputBuffer 不够大，无法满足结果。 未将任何信息写入缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>用户没有 SE_MANAGE_VOLUME 的访问权限。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**FSCTL \_可以在 FastFAT 和 exFAT 设备上使用 "获取 \_ 启动 \_ 区域 \_ 信息** " 控制代码。 此功能支持为闪存驱动器等设备使用 BitLocker。

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
<td align="left"><p>Windows Server 2008 R2，Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)

