---
title: FSCTL_QUERY_RETRIEVAL_POINTERS 控制代码
description: FSCTL \_ 查询 \_ 检索 \_ 指针控制代码检索虚拟群集号之间的映射 (VCN、文件/流空间内的偏移量) 和 () LCN 的逻辑群集号，从文件开头到 InputBuffer 中指定的映射大小开始，从文件的开头开始。
keywords:
- FSCTL_QUERY_RETRIEVAL_POINTERS 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_QUERY_RETRIEVAL_POINTERS
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c55117d5c7fd6d7a4770ab4c86bb7ccf0cab3f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833029"
---
# <a name="fsctl_query_retrieval_pointers-control-code"></a>FSCTL \_ 查询 \_ 检索 \_ 指针控制代码


**FSCTL \_ 查询 \_ 检索 \_ 指针** 控制代码检索虚拟群集号之间的映射 (VCN、文件/流空间内的偏移量) 和 () LCN 的逻辑群集号，从文件开头到 *InputBuffer* 中指定的映射大小开始，从文件的开头开始。

**FSCTL \_查询 \_ 检索 \_ 指针** 类似于 [**FSCTL \_ GET \_ 检索 \_ 指针**](fsctl-get-retrieval-pointers.md)。 但是， **FSCTL \_ 查询 \_ 检索 \_ 指针** 仅适用于本地页面文件或系统配置单元上的内核模式。 页面文件可保证从卷中的 VCN 到 LCN 的一对一映射，该映射直接引用底层的物理存储。 不得将 **FSCTL \_ 查询 \_ 检索 \_ 指针** 与页面文件以外的文件一起使用，因为它们可能驻留在具有 VCNs 到 LCNs 的一对多映射的卷上，如镜像卷。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 页面文件或休眠文件的文件对象指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 页面文件或休眠文件的文件句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 对于此操作，请使用 FSCTL \_ GET \_ 检索 \_ 指针。

<a href="" id="inputbuffer"></a>*InputBuffer*  
用户提供的一个缓冲区，其中包含指向指定地图大小的 quadlet 的指针。 地图大小是要映射的分类数。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
位于 *InputBuffer* 的输入缓冲区的长度（以字节为单位）。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
一个指针，指向包含以下类型的元素数组的分页缓冲池内存缓冲区：

```cpp
struct {
 LONGLONG  SectorLengthInBytes;
 LONGLONG  StartingLogicalOffsetInBytes;
  } MappingPair;
```

此 quadlet 对的数组定义文件的磁盘运行。 数组中最后一个元素的 **SectorLengthInBytes** 成员的值为零。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer* 参数指向的缓冲区的大小（以字节为单位）。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 和 [**ZWFSCONTROLFILE**](/previous-versions/ff566462(v=vs.85)) 都返回状态 \_ SUCCESS 或适当的 NTSTATUS 错误值。

<a name="remarks"></a>备注
-------

* * ReFS： * * 此代码不受支持。

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

[**FSCTL \_ 获取 \_ 检索 \_ 指针**](fsctl-get-retrieval-pointers.md)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

 

