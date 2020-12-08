---
title: FSCTL_GET_RETRIEVAL_POINTERS 控制代码
description: FSCTL \_ GET \_ 检索 \_ 指针控制代码检索大小不定大小的数据结构，该结构描述特定文件在磁盘上的分配和位置。
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
ms.openlocfilehash: 1da245f35eebeaf82532bd8798521b01a7212232
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808375"
---
# <a name="fsctl_get_retrieval_pointers-control-code"></a>FSCTL \_ GET \_ 检索 \_ 指针控制代码


**FSCTL \_ GET \_ 检索 \_ 指针** 控制代码检索大小不定大小的数据结构，该结构描述特定文件在磁盘上的分配和位置。 此结构描述了虚拟群集号之间的映射 (VCN、文件/流空间内的偏移量) 和 (LCN 的逻辑群集号，) 中的偏移量。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

有关重新分析点和 FSCTL \_ GET \_ 检索 \_ 指针控制代码的详细信息，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 FSCTL \_ GET \_ 检索指针为其检索映射的备用流、文件或目录的文件对象指针 \_ 。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 FSCTL \_ GET \_ 检索 \_ 指针检索映射的备用流、文件或目录的文件句柄。 如果 *FileHandle* 中的值是整个卷的句柄，则例程将返回错误群集文件的 VCNs 和区的映射。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 对于此操作，请使用 FSCTL \_ GET \_ 检索 \_ 指针。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向起始 \_ vcn \_ 输入 \_ 缓冲区结构的指针，该结构指示虚拟群集号 (VCN) ，用于标记备用流、文件或目录的开头。 按如下所示 \_ 定义起始 VCN \_ 输入 \_ 缓冲区结构：

```cpp
typedef struct {
  LARGE_INTEGER  ;
} STARTING_VCN_INPUT_BUFFER, *PSTARTING_VCN_INPUT_BUFFER;
```

**成员**

<a href="" id="startingvcn"></a>**StartingVcn**  
VCN，FSCTL \_ GET \_ 检索 \_ 指针开始枚举区和关联的虚拟和逻辑群集号。 在第一次调用 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 时，对于文件系统控制代码 FSCTL \_ GET \_ 检索 \_ 指针， **StartingVcn** 应设置为零。

如果 *OutputBuffer* 的大小不足以保存文件的 VCNs 和区的整个映射，则调用方必须使用检索指针缓冲区结构的 **NextVcn** 成员中返回的值 \_ \_ 作为起始 VCN 来请求更多的映射数据。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
位于 InputBuffer 的输入缓冲区的长度（以字节为单位） *。*

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向类型检索指针缓冲区的大小不定大小结构的 \_ 指针 \_ ，该指针包含磁盘上与备用流、文件或目录对应的范围的枚举：

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
**区** 数组中的元素计数。

<a href="" id="startingvcn"></a>**StartingVcn**  
正在启动由函数调用返回的 VCN。 这不一定是函数调用请求的 VCN，因为文件系统驱动程序可能会向下舍入到所请求的起始 VCN 所在范围的第一个 VCN。

<a href="" id="extents-"></a>**无关**   
区结构的数组。 有关数组中的成员数，请参阅 **ExtentCount**。 数组的每个成员都具有下列成员。

<a href="" id="nextvcn"></a>**NextVcn**  
下一个区开始处的 VCN。 此值减去第一个 **区** 数组成员的 **StartingVcn** (，) 或数组上一个成员的 **NextVcn** (适用于所有其他 **区** 数组成员) 是当前范围的长度（以分类为分类）。

<a href="" id="lcn"></a>**Lcn**  
当前区在卷上的起始位置的 LCN。 在 NTFS 上，LONGLONG)  (的值指示已部分分配的压缩单元或稀疏文件的未分配区域。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer* 参数指向的缓冲区的大小（以字节为单位）。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 和 [**ZWFSCONTROLFILE**](/previous-versions/ff566462(v=vs.85)) 都返回状态 \_ SUCCESS 或适当的 NTSTATUS 错误值。

如果 VCN/区映射不能容纳在 *OutputBuffer* 中，则两个例程将返回状态 \_ 缓冲区 \_ 溢出的值，并且调用方必须使用检索指针缓冲区结构的 **NextVcn** 成员中返回的值 \_ \_)  (来 **StartingVcn** [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))请求更多的映射数据。

如果 **StartingVcn** 中指定的值超出了文件的末尾， \_ \_ \_ 则返回文件的状态结尾。

<a name="remarks"></a>备注
-------

可以在 FastFAT 和 exFAT 设备上使用 **FSCTL \_ GET \_ 检索 \_ 指针** 控制代码。 此功能支持为闪存驱动器等设备使用 BitLocker。

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

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

 

