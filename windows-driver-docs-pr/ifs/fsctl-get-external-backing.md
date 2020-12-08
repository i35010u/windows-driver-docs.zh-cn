---
title: FSCTL_GET_EXTERNAL_BACKING 控制代码
description: FSCTL \_ 获取 \_ 外部 \_ 后备控制代码从外部支持提供商处获取文件的后备信息。
keywords:
- FSCTL_GET_EXTERNAL_BACKING 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_GET_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08c8cd89c7cc10378c2b89cc2c1ca3a0fd0f0f16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808381"
---
# <a name="fsctl_get_external_backing-control-code"></a>FSCTL \_ 获取 \_ 外部 \_ 后备控制代码


**FSCTL \_ 获取 \_ 外部 \_ 后备** 控制代码从外部支持提供商处获取文件的后备信息。 支持提供程序包括 Windows 映像格式 (WIM) 提供程序或单独的压缩文件提供程序。 外部支持的文件的内容可能驻留在卷上，而不是包含查询的文件的卷上。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**Parameters**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[ in\]*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 要查询其备份信息的文件的文件指针对象。 此参数是必需的，不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[\]*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 要查询其备份信息的文件的句柄。 此参数是必需的，不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[\]*  
操作的控制代码。 使用 **FSCTL 获取此操作的 \_ \_ 外部 \_ 支持** 。

<a href="" id="inputbuffer--in-"></a>*InputBuffer \[\]*  
无。 设置为 **NULL**。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[\]*  
设置为0。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[\]*  
指向输出缓冲区的指针，该缓冲区的大小必须足够大，以便接收 [**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info) 结构后跟提供程序数据。 对于支持 WIM 的文件， **WOF \_ 外部 \_ 信息** 后跟 [**wim \_ 提供程序 \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info) 结构。 对于单独压缩的文件， **WOF \_ 外部 \_ 信息** 后跟 [**文件 \_ 提供程序 \_ 外部 \_ 信息 \_ V1**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_provider_external_info_v1) 结构。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[\]*  
*OutputBuffer* 所指向的缓冲区的大小（以字节为单位）。

<a href="" id="lengthreturned"></a>*LengthReturned*  
指定成功完成后写入到 *OutputBuffer* 中的字节数。

<a name="status-block"></a>状态块
------------

如果操作成功，则 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))返回状态 \_ SUCCESS。 否则，相应的函数可能会返回以下 NTSTATUS 值之一。

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
<td align="left"><p><strong>STATUS_OBJECT_NOT_EXTERNALLY_BACKED</strong></p></td>
<td align="left"><p>文件未从外部获得支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>后备服务不存在或未启动。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

当要更新的数据源的后备提供程序是 WIM 文件时，输出缓冲区将包含 [**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info) 结构，后跟 [**WIM \_ 提供程序 \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info) 结构。 *OutputBufferLength* 必须至少为 **sizeof** (WOF \_ 外部 \_ 信息) + **sizeof** (WIM \_ 提供程序 \_ 外部 \_ 信息) 。 当后备提供程序是单独的压缩文件时，输出缓冲区将包含 **WOF \_ 外部 \_ 信息** 结构，后跟 [**文件 \_ 提供程序 \_ 外部 \_ 信息 \_ V1**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_provider_external_info_v1) 结构。

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
<td align="left"><p>从 Windows 8.1 更新开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs (包含 Ntifs 或 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

[**FSCTL \_ 设置 \_ 外部 \_ 支持**](fsctl-set-external-backing.md)

[**WIM \_ 提供程序 \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info)

[**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)

 

