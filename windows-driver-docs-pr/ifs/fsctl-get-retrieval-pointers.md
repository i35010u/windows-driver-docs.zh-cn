---
title: FSCTL_GET_RETRIEVAL_POINTERS 控制代码
description: FSCTL\_获取\_检索\_指针控制代码检索大小不定大小的数据结构，该结构描述特定文件在磁盘上的分配和位置。
ms.assetid: d77790c8-9fe6-4b36-995e-40a7ea54c18a
keywords:
- FSCTL_GET_RETRIEVAL_POINTERS 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_GET_RETRIEVAL_POINTERS
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a9f6bb4e809aea3b53dfefa28261ac67ea20602
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841302"
---
# <a name="fsctl_get_retrieval_pointers-control-code"></a>FSCTL\_获取\_检索\_指针控制代码


**FSCTL\_获取\_检索\_指针**控制代码检索大小不定大小的数据结构，该结构描述特定文件在磁盘上的分配和位置。 此结构描述虚拟群集号（VCN、文件/流空间内的偏移量）与逻辑群集号（LCN，卷空间内的偏移量）之间的映射。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

有关重新分析点和 FSCTL\_获取\_检索\_指针控制代码的详细信息，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 FSCTL\_获取其\_检索\_指针检索映射的备用流、文件或目录的文件对象指针。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 备用流、文件或目录的文件句柄，FSCTL\_获取该文件的\_检索\_指针检索映射。 如果*FileHandle*中的值是整个卷的句柄，则例程将返回错误群集文件的 VCNs 和区的映射。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_获取此操作\_检索\_指针。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向开始\_VCN\_输入\_缓冲区结构的指针，该结构指示用于标记备用流、文件或目录的开头的虚拟群集号（VCN）。 开始\_VCN\_输入\_缓冲区结构的定义如下所示：

```cpp
typedef struct {
  LARGE_INTEGER  ;
} STARTING_VCN_INPUT_BUFFER, *PSTARTING_VCN_INPUT_BUFFER;
```

**成员**

<a href="" id="startingvcn"></a>**StartingVcn**  
FSCTL\_获取\_检索的 VCN，\_指针开始枚举区和关联的虚拟和逻辑群集号。 在第一次调用[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)时，文件系统控制代码为 FSCTL\_获取\_指针\_检索， **StartingVcn**应设置为零。

如果*OutputBuffer*的大小不足以保存文件的 VCNs 和区的整个映射，则调用方必须使用检索\_指针的**NextVcn**成员中返回的值来请求更多的映射数据，\_缓冲区结构作为起始 VCN。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
位于 InputBuffer 的输入缓冲区的长度（以字节为单位） *。*

<a href="" id="outputbuffer"></a>*OutputBuffer*  
一个指针，指向类型检索\_指针的大小不定大小结构\_缓冲区，该缓冲区包含磁盘上与备用流、文件或目录对应的范围的枚举：

```cpp
typedef struct RETRIEVAL_POINTERS_BUFFER {
 ULONG  ExtentCount;
  LARGE_INTEGER  StartingVcn;
 struct {
    LARGE_INTEGER  NextVcn;
    LARGE_INTEGER  Lcn;
  } Extents[1];
} RETRIEVAL_POINTERS_BUFFER, *PRETRIEVAL_POINTERS_BUFFER;
```

**成员**

<a href="" id="extentcount"></a>**ExtentCount**  
**区**数组中的元素计数。

<a href="" id="startingvcn"></a>**StartingVcn**  
正在启动由函数调用返回的 VCN。 这不一定是函数调用请求的 VCN，因为文件系统驱动程序可能会向下舍入到所请求的起始 VCN 所在范围的第一个 VCN。

<a href="" id="extents-"></a>**区**   
区结构的数组。 有关数组中的成员数，请参阅**ExtentCount**。 数组的每个成员都具有下列成员。

<a href="" id="nextvcn"></a>**NextVcn**  
下一个区开始处的 VCN。 此值减去**StartingVcn** （对于第一个**区**数组成员）或数组上一个成员的**NextVcn** （对于所有其他**区**数组成员）是当前范围的长度（以群集为限）。

<a href="" id="lcn"></a>**Lcn**  
当前区在卷上的起始位置的 LCN。 在 NTFS 上，值（LONGLONG）-1 表示已部分分配的压缩单元或稀疏文件的未分配区域。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer*参数指向的缓冲区的大小（以字节为单位）。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)和[**ZWFSCONTROLFILE**](https://msdn.microsoft.com/library/windows/hardware/ff566462)都返回状态\_SUCCESS 或适当的 NTSTATUS 错误值。

如果 VCN/区映射不能容纳在*OutputBuffer*中，则两个例程\_溢出返回状态\_的值，并且调用方必须使用检索\_指针的**NextVcn**成员中返回的值请求更多的映射数据，并在下一次调用[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)时，\_缓冲区结构作为起始 VCN （**StartingVcn**）。

如果**StartingVcn**中指定的值超出了文件的末尾，则返回\_文件\_结束\_的状态。

<a name="remarks"></a>备注
-------

**FSCTL\_获取\_检索\_指针**控制代码可在 FastFAT 和 exFAT 设备上使用。 此功能支持为闪存驱动器等设备使用 BitLocker。

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

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






