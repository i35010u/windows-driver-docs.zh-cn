---
title: FSCTL_SET_EXTERNAL_BACKING 控制代码
description: FSCTL\_设置\_外部\_支持控件代码设置的文件，如 Windows 映像格式 (WIM) 文件或压缩的文件，由外部备份提供程序的备份源。
ms.assetid: 5CB9FD4D-AF29-4438-B0B5-49871102968A
keywords:
- FSCTL_SET_EXTERNAL_BACKING 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: ac3fa1240ceee4ed55cc212cc929e5aba22acc7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524176"
---
# <a name="fsctlsetexternalbacking-control-code"></a>FSCTL\_设置\_外部\_支持控件代码


**FSCTL\_设置\_外部\_备份**控制代码设置的文件，如 Windows 映像格式 (WIM) 文件或压缩的文件，由外部备份提供程序的备份源。 从外部备份文件的内容可能来源以外的其他文件所在的位置的卷上的卷上。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**参数**

<a href="" id="instance--in-"></a>*实例\[中\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 调用方不透明实例指针。 此参数是必需的不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[in\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 为其设置备份文件的文件指针对象。 此参数是必需的不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[in\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 为其设置备份的文件句柄。 此参数是必需的不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
操作的控制代码。 使用**FSCTL\_设置\_外部\_备份**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区，其中包含[ **WOF\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632452)结构后跟提供程序数据。 WIM 提供支持文件， **WOF\_外部\_信息**后跟[ **WIM\_提供程序\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632448)结构。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
中提供的数据的大小*InputBuffer*。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
无。 设置为 NULL。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength \[in\]*  
设置为 0。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功如果操作成功。 否则，返回相应的 NTSTATUS 值。

<a name="remarks"></a>备注
-------

输入的缓冲区的 WIM 提供程序添加的数据源的支持提供程序时，将包含[ **WOF\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632452)结构跟[**WIM\_提供程序\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632448)结构。 *InputBufferLength*在这种情况下将为**sizeof**(**WOF\_外部\_信息**) + **sizeof**(**WIM\_提供程序\_外部\_信息**)。

单独压缩的文件提供了很好地压缩不会修改，包括可执行文件的数据。 如果这些打开以进行写入该文件将以透明方式解压缩。 若要指定一个单独压缩的文件、 输入的缓冲区将包含[ **WOF\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632452)结构跟[**文件\_提供程序\_外部\_信息\_V1** ](https://msdn.microsoft.com/library/windows/hardware/mt426732)结构。 *InputBufferLength*在这种情况下将为**sizeof**(**WOF\_外部\_信息**) + **sizeof**(**文件\_提供程序\_外部\_信息\_V1**)。 可从 Windows 10 开始单个压缩的文件。

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
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_DELETE\_EXTERNAL\_BACKING**](fsctl-delete-external-backing.md)

[**FSCTL\_GET\_EXTERNAL\_BACKING**](fsctl-get-external-backing.md)

[**WIM\_PROVIDER\_EXTERNAL\_INFO**](https://msdn.microsoft.com/library/windows/hardware/dn632448)

[**WOF\_EXTERNAL\_INFO**](https://msdn.microsoft.com/library/windows/hardware/dn632452)

 

 






