---
title: FSCTL_QUERY_RETRIEVAL_POINTERS 控制代码
description: FSCTL\_查询\_检索\_指针控制代码检索虚拟群集号之间的映射（VCN、文件/流空间内的偏移量）和逻辑群集号（LCN，介于卷空间内的偏移量），从文件的开头到 InputBuffer 中指定的映射大小。
ms.assetid: 463a5cb9-d4eb-42d6-9103-956b45a5abfb
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
ms.openlocfilehash: 517be772ac656d4a185dfbedd9a7ff7968045e60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841266"
---
# <a name="fsctl_query_retrieval_pointers-control-code"></a>FSCTL\_查询\_检索\_指针控制代码


**FSCTL\_查询\_检索\_指针**控制代码检索虚拟群集号之间的映射（VCN、文件/流空间内的偏移量）和逻辑群集号（LCN，卷空间内的偏移量）。从文件开头到*InputBuffer*中指定的地图大小开始。

**FSCTL\_查询\_检索\_指针**类似于[**FSCTL\_获取\_检索\_指针**](fsctl-get-retrieval-pointers.md)。 但是， **FSCTL\_查询\_检索\_指针**仅适用于本地页面文件或系统配置单元上的内核模式。 页面文件可保证从卷中的 VCN 到 LCN 的一对一映射，该映射直接引用底层的物理存储。 不能使用**FSCTL\_查询\_检索\_** 包含除页面文件以外的文件的指针，因为它们可能驻留在具有 VCNs 到 LCNs 的一对多映射的卷上。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 页面文件或休眠文件的文件对象指针。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 页面文件或休眠文件的文件句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_获取用于此操作的\_检索\_指针。

<a href="" id="inputbuffer"></a>*InputBuffer*  
用户提供的一个缓冲区，其中包含指向指定地图大小的 quadlet 的指针。 地图大小是要映射的分类数。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
位于*InputBuffer*的输入缓冲区的长度（以字节为单位）。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
一个指针，指向包含以下类型的元素数组的分页缓冲池内存缓冲区：

```cpp
struct {
 LONGLONG  SectorLengthInBytes;
 LONGLONG  StartingLogicalOffsetInBytes;
  } MappingPair;
```

此 quadlet 对的数组定义文件的磁盘运行。 数组中最后一个元素的**SectorLengthInBytes**成员的值为零。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer*参数指向的缓冲区的大小（以字节为单位）。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)和[**ZWFSCONTROLFILE**](https://msdn.microsoft.com/library/windows/hardware/ff566462)都返回状态\_SUCCESS 或适当的 NTSTATUS 错误值。

<a name="remarks"></a>备注
-------

**ReFS：  **此代码不受支持。

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

[**FSCTL\_获取\_指针\_检索**](fsctl-get-retrieval-pointers.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






