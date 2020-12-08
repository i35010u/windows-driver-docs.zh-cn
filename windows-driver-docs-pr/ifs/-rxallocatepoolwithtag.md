---
title: '\_RxAllocatePoolWithTag 函数'
description: '\_RxAllocatePoolWithTag 从池中分配内存，在块开头有一个四字节标记，可用于帮助捕获内存 trashing 的实例。'
keywords:
- _RxAllocatePoolWithTag 功能可安装的文件系统驱动程序
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
ms.openlocfilehash: 261cef9bd47ac574e7915c881c60229cdf62d854
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789947"
---
# <a name="_rxallocatepoolwithtag-function"></a>\_RxAllocatePoolWithTag 函数


**\_ RxAllocatePoolWithTag** 从池中分配内存，在块开头有一个四字节标记，可用于帮助捕获内存 trashing 的实例。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID* _RxAllocatePoolWithTag(
   ULONG Type,
   ULONG Size,
   ULONG Tag,
   PSZ   FileName,
   ULONG LineNumber
);
```

<a name="parameters"></a>参数
----------

*类别*   
要分配的池的类型。 此参数可以是池类型的下列枚举值之一 \_ ：

<a href="" id="nonpagedpool"></a>**非分页池**  
可从任何 IRQL 访问的不可分页系统内存。 **非分页池** 内存是稀有资源，驱动程序只应在必要时才分配。 系统 \_ 在页面大小的倍数内只能分配大于 **非分页池** 页面大小的缓冲区 \_ 。 对于超出页面 \_ 大小但不是页面大小的缓冲区请求，会 \_ 浪费不可分页内存。

<a href="" id="pagedpool"></a>**PagedPool**  
只能以 IRQL 调度级别进行分配和访问的可分页系统内存 &lt; \_ 。

*规格*   
要分配的内存块的大小（以字节为单位）。

*符*   
用于标记已分配缓冲区的四字节标记。 有关如何使用标记的说明，请参阅 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)。 标记中每个字符的 ASCII 值必须介于0到127之间。

*名字*   
指向发生内存分配的源文件名的指针。 当前未使用此参数。

*LineNumber*   
源文件中发生内存分配的行号。 当前未使用此参数。

<a name="return-value"></a>返回值
------------

如果可用池中没有足够的内存来满足该请求， **RxAllocatePoolWithTag** 将返回 **NULL** 。 否则，例程将返回指向分配的内存的指针。

<a name="remarks"></a>备注
-------

建议调用 **RxAllocatePoolWithTag** 宏，而不是直接使用此例程。 在零售版上，此宏定义为调用 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)。 在选中的生成上，此宏定义为调用 **\_ RxAllocatePoolWithTag**。

**\_ RxAllocatePoolWithTag** 例程将调用 **ExAllocatePoolWithTagPriority** ，并将请求的优先级 (重要性设置为 "LowPoolPriority") 。 系统可能会在资源不足的情况下，请求 LowPoolPriority。 使用此例程时，驱动程序应准备好从分配故障中恢复。

当系统从页面大小的池内存或更大的内存分配缓冲区时 \_ ，将在页面边界上对齐缓冲区。 小于页面 \_ 大小的内存请求无需在页面边界上对齐，但始终适合单个页面，并在8字节边界上对齐。 如果任何成功分配请求的块大于页面大小 \_ 的倍数，并且不是页面大小的倍数，则会 \_ 在上次分配的页面上浪费所有未使用的字节。

系统将池标记与分配的内存关联起来。 诸如 WinDbg 这样的编程工具可以显示与每个已分配缓冲区关联的池标记。 *标记* 的值通常以相反顺序显示。 例如，如果调用方将 "Fred" 作为 *标记* 传递，则当内存转储或跟踪调试器中的内存使用率时，它将显示为 "derF"。

使用 **\_ RxAllocatePoolWithTag** 分配的内存应通过调用 [**\_ RxFreePool**](-rxfreepool.md)来释放。

**\_ RxAllocatePoolWithTag** 的调用方必须以 IRQL &lt; = 调度 \_ 级别执行。 在调度级别执行的调用方 \_ 必须为该 *类型* 参数指定 **非分页池** 值。 在 IRQL = APC 级别执行的调用方 &lt; \_ 可以 \_ 为 *类型* 参数指定任何池类型值。

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
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntrxdef (包含 Ntrxdef) </td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>请参阅备注部分。</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

[**\_RxCheckMemoryBlock**](-rxcheckmemoryblock.md)

[**\_RxFreePool**](-rxfreepool.md)

 

