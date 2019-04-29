---
title: IRP_MJ_SET_INFORMATION
description: IRP\_MJ\_SET\_INFORMATION
ms.assetid: cc1b539c-8d39-4f4d-93b1-ce9fcdb8c555
keywords:
- IRP_MJ_SET_INFORMATION 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_SET_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 258147f46d4cabda6bc7efea8ae2d965aec4ab74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324409"
---
# <a name="irpmjsetinformation"></a>IRP\_MJ\_SET\_INFORMATION


## <a name="when-sent"></a>发送时间


IRP\_MJ\_设置\_信息请求发送的 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序。 它可以发送，例如，在用户模式应用程序具有如调用 Microsoft Win32 函数时**SetEndOfFile**或当调用内核模式组件[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096).

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取和解码以确定是否表示用户文件或目录打开的文件对象。 如果是这样，文件系统驱动程序应处理相应请求和完成 IRP。

可以在文件和目录上设置以下类型的信息：

FileBasicInformation

FileDispositionInformation

FileLinkInformation （对于允许周期，才能在目录层次结构中创建的文件系统）

FilePositionInformation

FileRenameInformation

可以仅在文件上设置以下类型的信息：

FileAllocationInformation

FileEndOfFileInformation

FileLinkInformation （适用于文件系统，如 NTFS，不允许循环，以便在目录层次结构中创建的）

FileValidDataLengthInformation

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序必须在堆栈上传递此 IRP 到下一步低驱动程序。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理集文件的信息请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
指向包含要设置的文件或目录信息的输入缓冲区的指针。 此信息存储在一个以下结构：

[**文件\_分配\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540232)

[**文件\_BASIC\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545762)

[**文件\_处置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545765)

[**文件\_最终\_OF\_文件\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545780)

[**文件\_链接\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540324)

[**文件\_位置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545848)

[**文件\_重命名\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540344)

[**文件\_VALID\_数据\_长度\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545873)

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*指针，指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)有关接收最终的完成状态和信息的结构请求的操作。 有关详细信息，请参阅的说明*IoStatusBlock*参数[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;的文件对象*与关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_设置\_信息和不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction* IRP 指定\_MJ\_设置\_信息。

<a href="" id="irpsp--parameters-setfile-advanceonly"></a>*IrpSp-&gt;Parameters.SetFile.AdvanceOnly*的标志的文件结束操作。 这将确定使用**EndOfFile**成员[**文件\_最终\_OF\_文件\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545780)结构何时**FileInformationClass** == **FileEndOfFileInformation**。 如果 **，则返回 TRUE**，该文件的新有效的数据长度将设置从**EndOfFile**才会增加当前有效的数据长度。 如果**FALSE**，新的文件大小设置从**EndOfFile**。

<a href="" id="irpsp--parameters-setfile-clustercount"></a>*IrpSp-&gt;Parameters.SetFile.ClusterCount*保留供系统使用。

<a href="" id="irpsp--parameters-setfile-deletehandle"></a>*IrpSp-&gt;Parameters.SetFile.DeleteHandle*保留供系统使用。

<a href="" id="irpsp--parameters-setfile-fileinformationclass"></a>*IrpSp-&gt;Parameters.SetFile.FileInformationClass*指定要为文件设置的信息类型。 下列情况之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileAllocationInformation</strong></p></td>
<td align="left"><p>设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff540232" data-raw-source="[&lt;strong&gt;FILE_ALLOCATION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540232)"> <strong>FILE_ALLOCATION_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff545762" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545762)"> <strong>FILE_BASIC_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileDispositionInformation</strong></p></td>
<td align="left"><p>设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff545765" data-raw-source="[&lt;strong&gt;FILE_DISPOSITION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545765)"> <strong>FILE_DISPOSITION_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileEndOfFileInformation</strong></p></td>
<td align="left"><p>设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff545780" data-raw-source="[&lt;strong&gt;FILE_END_OF_FILE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545780)"> <strong>FILE_END_OF_FILE_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileLinkInformation</strong></p></td>
<td align="left"><p>设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff540324" data-raw-source="[&lt;strong&gt;FILE_LINK_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540324)"> <strong>FILE_LINK_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff545848" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545848)"> <strong>FILE_POSITION_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileRenameInformation</strong></p></td>
<td align="left"><p>设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff540344" data-raw-source="[&lt;strong&gt;FILE_RENAME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540344)"> <strong>FILE_RENAME_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileValidDataLengthInformation</strong></p></td>
<td align="left"><p>设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff545873" data-raw-source="[&lt;strong&gt;FILE_VALID_DATA_LENGTH_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545873)"> <strong>FILE_VALID_DATA_LENGTH_INFORMATION</strong> </a>文件。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-setfile-fileobject"></a>*IrpSp-&gt;Parameters.SetFile.FileObject*重命名或链接的操作。 如果*Irp-&gt;AssociatedIrp.SystemBuffer-&gt;FileName*包含完全限定的文件名，或者，如果*Irp-&gt;AssociatedIrp.SystemBuffer-&gt;RootDirectory*为非**NULL**，此成员是操作的目标的文件的父目录的文件对象指针。 否则它是**NULL**。

<a href="" id="irpsp--parameters-setfile-length"></a>*IrpSp-&gt;Parameters.SetFile.Length*指向的缓冲区的长度，以字节为单位， *Irp-&gt;AssociatedIrp.SystemBuffer*。

<a href="" id="irpsp--parameters-setfile-replaceifexists"></a>*IrpSp-&gt;Parameters.SetFile.ReplaceIfExists*设置为**TRUE**指定，如果已存在具有相同名称的文件，则应替换与给定文件。 设置为**FALSE**如果已存在具有给定名称的文件重命名操作应失败。

<a name="remarks"></a>备注
-------

**AdvanceOnly**成员设置为**TRUE**缓存管理器以通知文件系统，从而提升在磁盘上的新有效的数据长度中的当前有效的数据长度**EndOfFile**. 如果**AdvanceOnly**是**FALSE**，新的文件大小**EndOfFile**正在设置成员，这可以是大于或小于当前文件大小。

## <a name="see-also"></a>请参阅


[**文件\_分配\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540232)

[**文件\_BASIC\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545762)

[**文件\_处置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545765)

[**文件\_最终\_OF\_文件\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545780)

[**文件\_链接\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540324)

[**文件\_位置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545848)

[**文件\_重命名\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540344)

[**文件\_VALID\_数据\_长度\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545873)

[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_查询\_信息**](irp-mj-query-information.md)

[**ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)

 

 






