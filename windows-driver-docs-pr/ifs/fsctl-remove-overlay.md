---
title: FSCTL_REMOVE_OVERLAY 控制代码
description: FSCTL\_删除\_叠加控制代码从卷中删除后备源。
ms.assetid: 9AB1DD06-AFB3-45AF-8139-14B60076D63A
keywords:
- FSCTL_REMOVE_OVERLAY 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_REMOVE_OVERLAY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfec7a0997564edd8681bef5888414ff24da464d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841265"
---
# <a name="fsctl_remove_overlay-control-code"></a>FSCTL\_删除\_叠加控制代码


**FSCTL\_删除\_叠加**控制代码从卷中删除后备源。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 从中删除覆盖的卷的文件指针对象。 此参数是必需的，不能为 NULL。

<a href="" id="filehandle--in-"></a> *\]中的 FileHandle \[*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 要为其删除覆盖的卷的句柄。 此参数是必需的，不能为 NULL。

<a href="" id="fscontrolcode--in-"></a> *\]中的 FsControlCode \[*  
操作的控制代码。 使用**FSCTL\_删除**此操作的\_重叠。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区的指针，该指针必须包含[**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)结构。 如果需要，其他提供程序特定的数据将立即包含在**WOF\_外部\_信息**之后。 如果提供程序是 WIM 文件，则[**wim\_提供程序\_删除\_覆盖\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_remove_overlay_input)结构在**WOF\_外部\_信息**后包括。

<a href="" id="inputbufferlength--in-"></a> *\]中的 InputBufferLength \[*  
设置为**sizeof**（[**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)）加上任何其他提供程序输入数据的大小。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
不使用。 设置为 NULL。

<a href="" id="outputbufferlength--in-"></a> *\]中的 OutputBufferLength \[*  
设置为0。

<a name="status-block"></a>状态块
------------

如果操作成功，则[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回状态\_成功。 否则，相应的函数可能会返回以下 NTSTATUS 值之一。

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
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>请求者没有管理权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>OutputBuffer</em>（由<em>OutputBufferLength</em>指定）指向的输出缓冲区的长度太小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>请求的卷不可访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>后备服务不存在或未启动。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果要删除的后备源是 Windows 映像格式（WIM）文件，则输入缓冲区将包含[**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)结构后跟[**WIM\_提供程序\_删除\_覆盖\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_remove_overlay_input)构造. 在这种情况下， *InputBufferLength*将为**sizeof**（WOF\_外部\_信息） + **SIZEOF**（**WIM\_提供程序\_删除\_覆盖\_输入**）。 **Wim\_提供程序\_删除\_覆盖\_输入**的**DataSourceId**值必须为之前添加到[**FSCTL\_添加\_覆盖**](fsctl-add-overlay.md)请求中的 WIM 文件。

其他支持提供商将定义自己的特定输入参数结构。

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
<td align="left">Ntifs （包括 Ntifs 或 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FSCTL\_挂起\_覆盖**](fsctl-suspend-overlay.md)

[**FSCTL\_更新\_覆盖**](fsctl-update-overlay.md)

[**FSCTL\_获取\_外部\_后备**](fsctl-get-external-backing.md)

[**FSCTL\_设置\_外部\_后备**](fsctl-set-external-backing.md)

 

 






