---
title: FSCTL_SET_EXTERNAL_BACKING 控制代码
description: FSCTL\_将\_外部\_后备控制代码设置为外部后备提供程序设置文件的支持源，例如 Windows 映像格式（WIM）文件或压缩文件。
ms.assetid: 5CB9FD4D-AF29-4438-B0B5-49871102968A
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
ms.openlocfilehash: 703bc6cada1475c12ee16965770d381b24f51c5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841252"
---
# <a name="fsctl_set_external_backing-control-code"></a>FSCTL\_设置\_外部\_后备控制代码


**FSCTL\_将\_外部\_后备**控制代码设置为外部后备提供程序设置文件的支持源，例如 Windows 映像格式（WIM）文件或压缩文件。 外部支持的文件的内容可能来源于文件所在卷以外的卷。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 为其设置了备份的文件的文件指针对象。 此参数是必需的，不能为 NULL。

<a href="" id="filehandle--in-"></a> *\]中的 FileHandle \[*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 为其设置了备份的文件的句柄。 此参数是必需的，不能为 NULL。

<a href="" id="fscontrolcode--in-"></a> *\]中的 FsControlCode \[*  
操作的控制代码。 使用**FSCTL\_设置\_外部\_** 为此操作提供支持。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区的指针，其中包含[**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)结构后跟提供程序数据。 对于支持 WIM 的文件， **WOF\_外部\_信息**后跟[**WIM\_提供程序\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info)结构。

<a href="" id="inputbufferlength--in-"></a> *\]中的 InputBufferLength \[*  
*InputBuffer*中提供的数据的大小。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
无。 设置为 NULL。

<a href="" id="outputbufferlength--in-"></a> *\]中的 OutputBufferLength \[*  
设置为0。

<a name="status-block"></a>状态块
------------

如果操作成功，则[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回状态\_成功。 否则，将返回相应的 NTSTATUS 值。

<a name="remarks"></a>备注
-------

当添加的数据源的后备提供程序是 WIM 提供程序时，输入缓冲区将包含[**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)结构，后面跟有[**WIM\_提供程序\_外部\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info)结构。 在这种情况下， *InputBufferLength*将为**sizeof**（**WOF\_外部\_信息**） + **SIZEOF**（**WIM\_提供程序\_外部\_信息**）。

单独压缩的文件为不会修改的数据（包括可执行文件）提供了良好的压缩功能。 如果打开这些文件进行写入，将以透明方式解压缩文件。 若要指定单独的压缩文件，输入缓冲区将包含[**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)结构，后跟一个[**文件\_提供程序\_外部\_INFO\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_provider_external_info_v1)结构。 在这种情况下， *InputBufferLength*将为**sizeof**（**WOF\_外部\_信息**） + **SIZEOF**（**文件\_提供程序\_外部\_INFO\_V1**）。 从 Windows 10 开始可以使用各个压缩文件。

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

[**FSCTL\_删除\_外部\_后备**](fsctl-delete-external-backing.md)

[**FSCTL\_获取\_外部\_后备**](fsctl-get-external-backing.md)

[**WIM\_提供程序\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info)

[**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)

 

 






