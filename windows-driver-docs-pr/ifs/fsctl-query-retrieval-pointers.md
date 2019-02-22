---
title: FSCTL_QUERY_RETRIEVAL_POINTERS 控制代码
description: FSCTL\_查询\_检索\_指针控制的代码检索虚拟群集 (VCN，文件/流空间内的偏移量) 和逻辑群集号码 (LCN，卷空间内的偏移量) 之间的映射，从最大映射大小 InputBuffer 中指定文件的开头处开始。
ms.assetid: 463a5cb9-d4eb-42d6-9103-956b45a5abfb
keywords:
- FSCTL_QUERY_RETRIEVAL_POINTERS 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: 7c54bbbfdb782e80955ff61c518bf530cec63e1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546868"
---
# <a name="fsctlqueryretrievalpointers-control-code"></a>FSCTL\_查询\_检索\_指针控制的代码


**FSCTL\_查询\_检索\_指针**控制代码检索虚拟群集数字 (VCN，文件/流空间内的偏移量) 之间的映射和逻辑群集数字 (LCN，偏移量的卷空间内），最多开始处的文件中指定映射大小*InputBuffer*。

**FSCTL\_查询\_检索\_指针**类似于[ **FSCTL\_获取\_检索\_指针**](fsctl-get-retrieval-pointers.md). 但是， **FSCTL\_查询\_检索\_指针**仅适用于本地的页面文件或系统配置单元在内核模式下。 分页文件保证能够从 VCN 的一对一映射更直接地对基础物理存储，请参阅 LCN 到卷中。 您必须使用**FSCTL\_查询\_检索\_指针**与页面文件以外的文件，因为它们可能位于如镜像卷的卷上具有的一个多映射到 LCNs VCNs。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**参数**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 对象的指针的页面文件或休眠文件。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 分页文件或休眠文件的文件句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_获取\_检索\_指针与此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
包含一个指向指定地图大小 quadlet 的用户提供的缓冲区。 地图大小是要映射的分类数。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
在输入缓冲区的长度，以字节为单位， *InputBuffer*。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向包含以下类型的元素的数组的页面缓冲的池内存缓冲区的指针：

```cpp
struct {
 LONGLONG  SectorLengthInBytes;
 LONGLONG  StartingLogicalOffsetInBytes;
  } MappingPair;
```

此数组 quadlet 对定义文件的磁盘运行。 值**SectorLengthInBytes**中数组的最后一个元素的成员为零。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
大小 （字节） 通过指向的缓冲区*OutputBuffer*参数。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)并[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)都返回状态\_成功或适当的 NTSTATUS 错误值。

<a name="remarks"></a>备注
-------

**ReFS:  **不支持此代码。

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
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**FSCTL\_GET\_RETRIEVAL\_POINTERS**](fsctl-get-retrieval-pointers.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






