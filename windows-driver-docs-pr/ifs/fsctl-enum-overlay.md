---
title: FSCTL_ENUM_OVERLAY 控制代码
description: FSCTL\_枚举\_叠加控制代码枚举指定卷的后备提供程序中的所有数据源。
ms.assetid: 146A7D77-034F-4C06-99B8-8EBA6E7F0A40
keywords:
- FSCTL_ENUM_OVERLAY 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_ENUM_OVERLAY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc2652b99b14e4eb494a9bc5c461e6dbe4fcd8c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841315"
---
# <a name="fsctl_enum_overlay-control-code"></a>FSCTL\_枚举\_叠加控制代码


**FSCTL\_枚举\_叠加**控制代码枚举指定卷的后备提供程序中的所有数据源。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为**NULL**。

<a href="" id="fileobject--in-"></a>*FileObject \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件指针对象，指定要卸除的卷。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle--in-"></a> *\]中的 FileHandle \[*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 要卸除的卷的文件句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode--in-"></a> *\]中的 FsControlCode \[*  
操作的控制代码。 使用**FSCTL\_删除**此操作的\_重叠。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区的指针，该指针必须包含[**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)结构。

<a href="" id="inputbufferlength--in-"></a> *\]中的 InputBufferLength \[*  
设置为**sizeof**（WOF\_外部\_信息）。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
指向输出缓冲区的指针，该缓冲区将接收一个或多个[**WIM\_提供程序\_覆盖**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_update_overlay_input)用于支持卷的数据源\_条目结构。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[out\]*  
*OutputBuffer*所指向的缓冲区大小（以字节为单位）。

<a href="" id="lengthreturned--out-"></a>*LengthReturned \[out\]*  
指定成功完成后写入到*OutputBuffer*中的字节数。

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
<td align="left"><p><em>OutputBuffer</em>指向的和由<em>OutputBufferLength</em>指定的输出缓冲区的长度太小。</p></td>
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

枚举 WIM 提供程序的数据源时，输出缓冲区将包含[**wim\_提供程序的数组\_覆盖\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_update_overlay_input)结构。 输出缓冲区的大小必须足够大才能包含所有覆盖项，否则，调用将返回状态\_缓冲区\_\_太小。

其他支持提供商将定义自己的特定枚举结构。

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


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_添加\_叠加**](fsctl-add-overlay.md)

[**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)

 

 






