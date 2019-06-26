---
title: FSCTL_GET_RETRIEVAL_POINTERS 控制代码
description: FSCTL\_获取\_检索\_指针控制的代码检索特定文件的磁盘描述的分配和位置的大小不定的数据结构。
ms.assetid: d77790c8-9fe6-4b36-995e-40a7ea54c18a
keywords:
- FSCTL_GET_RETRIEVAL_POINTERS 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: b500a5ba4094de7de16dd26f8b90a5df9e764122
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365023"
---
# <a name="fsctlgetretrievalpointers-control-code"></a>FSCTL\_获取\_检索\_指针控制的代码


**FSCTL\_获取\_检索\_指针**控制代码会检索特定文件的磁盘描述的分配和位置的大小不定的数据结构。 结构描述虚拟群集 (VCN，文件/流空间内的偏移量) 和逻辑群集号码 (LCN，卷空间内的偏移量) 之间的映射。

若要执行此操作，调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

有关重新分析点和 FSCTL\_获取\_检索\_指针控制的代码，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 对象的指针的备用流、 文件或目录的 FSCTL\_获取\_检索\_指针检索映射。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 备用流、 文件或目录的 FSCTL 的文件句柄\_获取\_检索\_指针检索映射。 如果中的值*FileHandle*是整个卷，VCNs 和不正确的群集文件的扩展盘区的地图，例程返回的句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_获取\_检索\_指针对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
正在启动一个指向\_VCN\_输入\_缓冲区结构，它指示表示备用流、 文件或目录的开头的虚拟群集数 (VCN)。 正在启动\_VCN\_输入\_缓冲区结构定义，如下所示：

```cpp
typedef struct {
  LARGE_INTEGER  ;
} STARTING_VCN_INPUT_BUFFER, *PSTARTING_VCN_INPUT_BUFFER;
```

**成员**

<a href="" id="startingvcn"></a>**StartingVcn**  
在哪些 FSCTL VCN\_获取\_检索\_指针开始枚举扩展盘区和关联的虚拟和逻辑群集数字。 在首次调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)文件系统的控制代码，为 FSCTL\_获取\_检索\_指针**StartingVcn**应设置为零。

如果*OutputBuffer*是不足够大以保存 VCNs 和扩展盘区的文件的整个代码图，调用方必须详细地图数据使用请求中返回的值**NextVcn** 中检索的成员\_指针\_作为起始 VCN 缓冲区结构。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
在输入缓冲区的长度，以字节为单位， *InputBuffer。*

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向类型检索的大小不定结构的指针\_指针\_缓冲区，其中包含对应于备用流、 文件或目录的磁盘上的盘区的枚举：

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
中的元素计数**区**数组。

<a href="" id="startingvcn"></a>**StartingVcn**  
启动 VCN 函数调用返回。 这不一定是函数调用请求 VCN 向下舍入的文件系统驱动程序可能会在其中找到所请求的起始 VCN 的范围内第一个 VCN 到。

<a href="" id="extents-"></a>**扩展盘区**   
扩展盘区结构的数组。 数组中的成员数，请参阅**ExtentCount**。 数组的每个成员具有以下成员。

<a href="" id="nextvcn"></a>**NextVcn**  
下一步的范围开始处 VCN。 此值减去任一**StartingVcn** (第一个**区**数组成员) 或**NextVcn**的数组的上一个成员 (对于所有其他**扩展盘区**数组成员) 的当前范围内长度，在群集中，为。

<a href="" id="lcn"></a>**Lcn**  
在卷的当前范围内开始处 LCN。 在 NTFS 中，值 (LONGLONG)-1 指示部分分配一个压缩单元或稀疏文件的未分配的区域。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
大小 （字节），指向的缓冲区*OutputBuffer*参数。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)并[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)都返回状态\_成功或适当的 NTSTATUS 错误值。

如果 VCN / 扩展盘区映射不符合要求*OutputBuffer*，这两个例程将返回状态的值\_缓冲区\_溢出和调用方必须请求使用中返回的值的多个地图数据**NextVcn**检索的成员\_指针\_缓冲区结构作为起始 VCN (**StartingVcn**) 中的后续调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)。

如果在指定的值**StartingVcn**超出文件状态的结尾\_最终\_OF\_返回文件。

<a name="remarks"></a>备注
-------

**FSCTL\_获取\_检索\_指针**可 FastFAT 和 exFAT 的设备上使用的控制代码。 此功能支持的设备，例如闪存驱动器使用 BitLocker。

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

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






