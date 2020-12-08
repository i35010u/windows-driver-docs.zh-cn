---
title: FSCTL_SET_EXTERNAL_BACKING 控制代码
description: FSCTL \_ 设置 \_ 外部 \_ 后备控制代码通过外部后备提供程序设置文件的支持源，例如 Windows 映像格式 (WIM) 文件或压缩文件。
keywords:
- FSCTL_SET_EXTERNAL_BACKING 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_SET_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 662e1786689ae4e1aa2156270346b1560c19841d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801769"
---
# <a name="fsctl_set_external_backing-control-code"></a>FSCTL \_ 设置 \_ 外部 \_ 后备控制代码


**FSCTL \_ 设置 \_ 外部 \_ 后备** 控制代码通过外部后备提供程序设置文件的支持源，例如 Windows 映像格式 (WIM) 文件或压缩文件。 外部支持的文件的内容可能来源于文件所在卷以外的卷。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**Parameters**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[ in\]*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 为其设置了备份的文件的文件指针对象。 此参数是必需的，不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[\]*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 为其设置了备份的文件的句柄。 此参数是必需的，不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[\]*  
操作的控制代码。 使用 **FSCTL 设置此操作的 \_ \_ 外部 \_ 后备** 。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区的指针，其中包含 [**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info) 结构，后面跟提供程序数据。 对于支持 WIM 的文件， **WOF \_ 外部 \_ 信息** 后跟 [**wim \_ 提供程序 \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info) 结构。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[\]*  
*InputBuffer* 中提供的数据的大小。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[\]*  
无。 设置为 NULL。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength \[\]*  
设置为0。

<a name="status-block"></a>状态块
------------

如果操作成功，则 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))返回状态 \_ SUCCESS。 否则，将返回相应的 NTSTATUS 值。

<a name="remarks"></a>备注
-------

当添加的数据源的后备提供程序是 WIM 提供程序时，输入缓冲区将包含 [**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info) 结构，后跟 [**WIM \_ 提供程序 \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info) 结构。 在这种情况下， *InputBufferLength* 将为 **sizeof** (**WOF \_ 外部 \_ 信息**) + **sizeof** (**WIM \_ 提供程序 \_ 外部 \_ 信息**) 。

单独压缩的文件为不会修改的数据（包括可执行文件）提供了良好的压缩功能。 如果打开这些文件进行写入，将以透明方式解压缩文件。 若要指定单独的压缩文件，输入缓冲区将包含 [**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info) 结构，后跟 [**文件 \_ 提供程序 \_ 外部 \_ 信息 \_ V1**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_provider_external_info_v1) 结构。 在这种情况下， *InputBufferLength* 将为 **sizeof** (**WOF \_ 外部 \_ 信息**) + **sizeof** (**文件 \_ 提供程序 \_ 外部 \_ 信息 \_ V1**) 。 从 Windows 10 开始可以使用各个压缩文件。

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

[**FSCTL \_ 删除 \_ 外部 \_ 支持**](fsctl-delete-external-backing.md)

[**FSCTL \_ 获取 \_ 外部 \_ 支持**](fsctl-get-external-backing.md)

[**WIM \_ 提供程序 \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info)

[**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)

 

