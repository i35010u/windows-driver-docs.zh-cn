---
title: FSCTL_SET_ZERO_DATA 控制代码
description: FSCTL \_ 设置 \_ 零 \_ 数据控制代码用零 (0) 填充文件的指定范围。
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
ms.openlocfilehash: 9a833c2910b3c7427f4c3f7d75ca38d5cc6a5d42
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785229"
---
# <a name="fsctl_set_zero_data-control-code"></a>FSCTL \_ 设置 \_ 零 \_ 数据控制代码


**FSCTL \_ 设置 \_ 零 \_ 数据** 控制代码用零 (0) 填充文件的指定范围。 如果文件是稀疏文件或压缩文件，则 NTFS 文件系统可能会释放文件中的磁盘空间。 这会将字节范围设置为零 (0) ，而无需扩展文件大小。

若要从驱动程序执行此操作，请使用以下参数调用 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。

**Parameters**

<a href="" id="instance"></a>*实例*  
调用方的不透明实例指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="fileobject"></a>*FileObject*  
文件对象指针，指向要将零写入其中的文件。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。

使用 FSCTL 为此操作 **\_ 设置 \_ 零 \_ 数据** 。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向 [**文件 \_ 零 \_ 数据 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information) 或 [**文件 \_ 零 \_ 数据 \_ 信息 \_**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information_ex) 的指针，如结构，它指定要设置为零的文件范围。

**FileOffset** 成员是要设置为零 (0) 的第一个字节的字节偏移量，而 **BeyondFinalZero** 成员是在最后一个零 (0) 字节之外的第一个字节的字节偏移量。

[**文件 \_ 零 \_ 数据 \_ 信息 \_**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information_ex)中的 **Flags** 成员（EX）指定操作的修饰符。 例如，如果 " **标志** " 设置为 "文件零"，则 **\_ \_ 数据 \_ 信息 \_ 标志将 \_ 保留 \_ 缓存的 \_ 数据**，则不会清除与此文件范围对应的缓存内容。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
输入缓冲区的大小（以字节为单位）。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不与此操作一起使用;设置为 **NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 返回 **状态 \_ SUCCESS** 或适当的 NTSTATUS 值。

-   **状态 \_如果 \_** 没有足够的内存来完成该操作，则会返回资源不足。
-   **状态 \_当 \_** *InputBufferLength* 小于 **文件 \_ 零 \_ 数据 \_ 信息** 结构的大小，或者指定的文件是系统元数据文件或目录时，将返回无效参数。
-   **状态 \_当 \_** 从用户模式设置 **文件 \_ 零 \_ 数据 \_ 信息 \_ 标志 \_ 保留 \_ 缓存 \_ 数据** 时，将返回 "拒绝访问"。
-   **状态 \_如果 \_ \_** 卷当前写保护，则返回受媒体写入保护。

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
<td align="left">Ntifs (包含 Ntifs) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**文件 \_ 零 \_ 数据 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information)

[**文件 \_ 零 \_ 数据 \_ 信息， \_ 例如**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information_ex)

 

