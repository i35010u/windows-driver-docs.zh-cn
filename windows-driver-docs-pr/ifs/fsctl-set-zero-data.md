---
title: FSCTL_SET_ZERO_DATA 控制代码
description: FSCTL\_设置\_零\_数据控件代码填充零 (0) 的文件的指定的范围。
ms.assetid: AEC4DAD4-17EB-412B-881B-E54F6A578637
keywords:
- FSCTL_SET_ZERO_DATA 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_SET_ZERO_DATA
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ddcebb0ad5041c287882cd92fbefa332f2c8088
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366223"
---
# <a name="fsctlsetzerodata-control-code"></a>FSCTL\_设置\_零\_数据控制代码


**FSCTL\_设置\_零\_数据**控制代码填充零 (0) 的文件的指定的范围。 如果该文件是稀疏的还是压缩，NTFS 文件系统可能会释放文件中的磁盘空间。 这设置为零 (0) 无需扩展的文件大小的字节范围。

若要从驱动程序执行此操作，调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)使用以下参数。

**Parameters**

<a href="" id="instance"></a>*实例*  
调用方的不透明实例指针。 此参数是必需的不能**NULL**。

<a href="" id="fileobject"></a>*FileObject*  
指向在其中写入零文件的文件对象指针。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。

使用**FSCTL\_设置\_零\_数据**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
一个指向[**文件\_零\_数据\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_zero_data_information)或[**文件\_零\_数据\_信息\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_zero_data_information_ex)结构，它指定要设置为零的文件的范围。

**FileOffset**成员是要将设置为零 (0) 的第一个字节的字节偏移量和**BeyondFinalZero**成员是字节超出最后一个的第一个字节的零 (0) 的字节偏移量。

**标志**中的成员[**文件\_零\_数据\_信息\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_zero_data_information_ex)指定的修饰符操作。 例如，当**标志**设置为**文件\_零\_数据\_信息\_标志\_保留\_缓存\_数据**，对应于此范围的文件缓存的内容不会被清除。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
输入缓冲区，以字节为单位的大小。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不用于此操作;设置为**NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不用于此操作;设置为零。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)返回**状态\_成功**或适当的 NTSTATUS 值。

-   **状态\_不足\_资源**时内存不足，无法完成该操作返回。
-   **状态\_无效\_参数**时，将返回*InputBufferLength*比的大小小**文件\_零\_数据\_信息**结构或指定的文件是系统元数据文件或目录。
-   **状态\_访问\_DENIED**时，将返回**文件\_零\_数据\_信息\_标志\_保留\_CACHED\_数据**从用户模式设置。
-   **状态\_媒体\_编写\_受保护**返回如果卷当前受写保护。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FILE\_ZERO\_DATA\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_zero_data_information)

[**FILE\_ZERO\_DATA\_INFORMATION\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_zero_data_information_ex)

 

 






