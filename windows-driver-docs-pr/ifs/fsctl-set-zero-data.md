---
title: FSCTL_SET_ZERO_DATA 控制代码
description: FSCTL\_将\_零\_数据控制代码使用零（0）填充文件的指定范围。
ms.assetid: AEC4DAD4-17EB-412B-881B-E54F6A578637
keywords:
- FSCTL_SET_ZERO_DATA 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: a2b723eeb510e387efb42a8e154cf49b0d483340
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841246"
---
# <a name="fsctl_set_zero_data-control-code"></a>FSCTL\_设置\_零\_数据控制代码


**FSCTL\_将\_零\_数据**控制代码使用零（0）填充文件的指定范围。 如果文件是稀疏文件或压缩文件，则 NTFS 文件系统可能会释放文件中的磁盘空间。 这会将字节范围设置为零（0），而不会扩展文件大小。

若要从驱动程序执行此操作，请使用以下参数调用[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。

**Parameters**

<a href="" id="instance"></a>*实例*  
调用方的不透明实例指针。 此参数是必需的，不能为**NULL**。

<a href="" id="fileobject"></a>*FileObject*  
文件对象指针，指向要将零写入其中的文件。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。

使用**FSCTL\_设置此操作\_零\_数据**。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向文件的指针[ **\_零\_数据\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information)或[**文件\_零\_数据\_\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information_ex)结构，它指定要设置为零的文件范围。

**FileOffset**成员是要设置为零（0）的第一个字节的字节偏移量，而**BeyondFinalZero**成员是最后一个零（0）字节之外的第一个字节的字节偏移量。

文件中的**Flags**成员[ **\_零\_数据\_信息\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information_ex)指定操作的修饰符。 例如，当**标志**设置为**FILE\_零\_数据\_信息\_标志\_保留\_缓存\_数据**，则不会清除与此文件范围对应的缓存内容。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
输入缓冲区的大小（以字节为单位）。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不与此操作一起使用;设置为**NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)返回 **\_SUCCESS**或适当的 NTSTATUS 值的状态。

-   如果没有足够的内存来完成该操作，则会返回 **\_状态\_资源不足**。
-   状态\_当*InputBufferLength*小于文件的大小 **\_零\_数据\_信息**结构或指定的文件是系统元数据文件时，返回 **\_参数无效**。或目录。
-   当**文件\_零\_数据\_\_标志**\_\_的数据从用户模式设置\_时，将返回 **\_拒绝访问的状态**。
-   如果卷当前写保护，则会返回 **\_MEDIA\_写入\_保护的状态**。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**文件\_零\_数据\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information)

[**文件\_零\_数据\_信息\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information_ex)

 

 






