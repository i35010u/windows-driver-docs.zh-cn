---
title: '\_RxAllocatePoolWithTag 函数'
description: '\_RxAllocatePoolWithTag 从具有四个字节标记可用于帮助捕获实例的内存移入垃圾桶块的开始处的池分配内存。'
ms.assetid: 5e999d06-ebcf-433a-a714-f340a1c74be1
keywords:
- _RxAllocatePoolWithTag 函数可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- _RxAllocatePoolWithTag
api_location:
- ntrxdef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1b804bf7f2fd8cd580827f6a54df0bef192a20c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524211"
---
# <a name="rxallocatepoolwithtag-function"></a>\_RxAllocatePoolWithTag 函数


**\_RxAllocatePoolWithTag**从具有四个字节标记可用于帮助捕获实例的内存移入垃圾桶块的开始处的池分配内存。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID* _RxAllocatePoolWithTag(
   ULONG Type,
   ULONG Size,
   ULONG Tag,
   PSZ   FileName,
   ULONG LineNumber
);
```

<a name="parameters"></a>参数
----------

*类型*   
要分配的池的类型。 此参数可以是以下池的枚举值之一\_类型：

<a href="" id="nonpagedpool"></a>**NonPagedPool**  
可以从任何 IRQL 访问分页系统内存。 **非分页池**内存是稀缺资源和驱动程序应将其仅在必要时进行分配。 系统仅可以分配大于页的缓冲区\_大小从**非分页池**页的倍数\_大小。 请求的缓冲区大小超过页\_大小，但不是页面\_大小多，浪费不可分页的内存。

<a href="" id="pagedpool"></a>**PagedPool**  
可分页系统内存，仅可以分配和访问在 IRQL&lt;调度\_级别。

*大小*   
内存块，以字节为单位，并将其分配的大小。

*标记*   
要用于标记为已分配的缓冲区的四个字节标记。 有关如何使用标记的说明，请参阅[ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)。 在标记中的每个字符的 ASCII 值必须介于 0 和 127 之间。

*FileName*   
指向源文件名发生内存分配的指针。 当前未使用此参数。

*LineNumber*   
发生内存分配的源文件中的行号。 当前未使用此参数。

<a name="return-value"></a>返回值
------------

**RxAllocatePoolWithTag**将返回**NULL**如果可用的池来满足请求中没有足够的内存。 否则，该例程返回一个指向已分配的内存。

<a name="remarks"></a>备注
-------

建议**RxAllocatePoolWithTag**宏调用而不是直接使用此例程。 在零售版本中，定义此宏调用[ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)。 在 checked 版本中，定义此宏调用 **\_RxAllocatePoolWithTag**。

 **\_RxAllocatePoolWithTag**例程调用**ExAllocatePoolWithTagPriority**优先级 （请求的重要性） 设置为 LowPoolPriority。 在资源上运行较低时，系统可能会失败 LowPoolPriority 的请求。 驱动程序应准备好使用此例程时从发生分配失败中恢复。

当系统分配从页池内存中的缓冲区\_大小或更高版本，它将对齐页边界上的缓冲区。 小于页内存请求\_大小不一定是页边界上对齐，但始终适合单个页面，和一个 8 字节边界上对齐。 请求的块大小超过页任何成功分配\_大小不是页面的倍数\_大小浪费了上一次分配页上所有未使用的字节数。

系统将池标记已分配的内存与相关联。 编程的工具，如的 WinDbg 中，可以显示与每个分配的缓冲区关联的池标记。 值*标记*通常按相反的顺序显示。 例如，如果调用方传递 Fred 作为*标记*，它将显示为 derF，如果内存转储，或者跟踪在调试器中的内存使用情况。

使用分配的内存 **\_RxAllocatePoolWithTag**应释放通过调用[  **\_RxFreePool**](-rxfreepool.md)。

调用方 **\_RxAllocatePoolWithTag**必须执行在 IRQL &lt;= 调度\_级别。 调用方执行调度\_级别必须指定**非分页池**值*类型*参数。 调用方执行在 IRQL &lt;= APC\_级别可以指定任何池\_类型值*类型*参数。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntrxdef.h （包括 Ntrxdef.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>请参阅备注部分。</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)

[**\_RxCheckMemoryBlock**](-rxcheckmemoryblock.md)

[**\_RxFreePool**](-rxfreepool.md)

 

 






