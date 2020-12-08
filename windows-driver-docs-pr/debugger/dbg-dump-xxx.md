---
title: DBG \_ 转储 \_ XXX
description: DBG \_ 转储 \_ XXX
ms.date: 12/07/2017
keywords:
- DBG_DUMP_XXX Windows 调试
topic_type:
- apiref
api_name:
- DBG_DUMP_XXX
api_location:
- wdbgexts.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: d3ffdf568451e6469f10106f30a8b573ac777605
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783505"
---
# <a name="dbg_dump_xxx"></a>DBG \_ 转储 \_ XXX


## <span id="ddk_dbg_dump_xxx_dbx"></span><span id="DDK_DBG_DUMP_XXX_DBX"></span>


\_ \_ 符号转储参数结构的 **OPTIONS** 成员使用 DBG 转储 *XXX* 位标志 \_ \_ 来控制 [**IG \_ 转储 \_ 符号 \_ 信息**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param)[**Ioctl**](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作的行为。

可以存在以下标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DBG_DUMP_NO_INDENT</p></td>
<td align="left"><p>成员不会在输出中缩进。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_NO_OFFSET</p></td>
<td align="left"><p>不打印偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_VERBOSE</p></td>
<td align="left"><p>详细输出。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_CALL_FOR_EACH</p></td>
<td align="left"><p>为每个成员调用回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_LIST</p></td>
<td align="left"><p>符号是链接列表中的项，IG_DUMP_SYMBOL_INFO <strong>Ioctl</strong> 操作将循环访问此列表。 指向列表中下一项的成员的说明由 SYM_DUMP_PARAM 结构的 <strong>linkList</strong> 成员指定。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_NO_PRINT</p></td>
<td align="left"><p>不会打印任何内容 (仅调用回调函数并) 执行数据复制。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_GET_SIZE_ONLY</p></td>
<td align="left"><p><strong>Ioctl</strong>操作仅返回符号的大小;它不会打印成员信息或调用回调函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_COMPACT_OUT</p></td>
<td align="left"><p>不会在每个成员后打印换行符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_ARRAY</p></td>
<td align="left"><p>符号为数组。 数组中元素的数目由 SYM_DUMP_PARAM 结构的成员 <strong>listLink &gt; 大小</strong> 指定。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_ADDRESS_OF_FIELD</p></td>
<td align="left"><p><strong>Addr</strong>的值实际上是 SYM_DUMP_PARAM 结构的成员<strong>listLink- &gt; fName</strong>的地址，而不是符号的开头。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_ADDRESS_AT_END</p></td>
<td align="left"><p><strong>Addr</strong>的值实际上是符号末尾的地址，而不是符号的开头。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_COPY_TYPE_DATA</p></td>
<td align="left"><p>符号的值将复制到成员 <strong>pBuffer</strong>中。 它只能用于基元类型，例如 ULONG 或 PVOID--不能用于结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_READ_PHYSICAL</p></td>
<td align="left"><p>将直接从目标的物理内存中读取符号的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FUNCTION_FORMAT</p></td>
<td align="left"><p>在设置具有函数类型的符号的格式时，将使用函数格式，例如 <code>function(arg1, arg2, ...)</code></p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_BLOCK_RECURSE</p></td>
<td align="left"><p>通过嵌套结构递归;但不要关注指针。</p></td>
</tr>
</tbody>
</table>

 

此外，宏 DBG 转储的结果 \_ \_ \_ (*级别*) 可添加到位集，以指定要递归的结构的深度。 *级别* 可以是0到15之间的数字。

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
<td align="left"> (包含 Wdbgexts、Wdbgexts 或 Dbgeng 的 Wdbgexts) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**IG \_ 转储 \_ 符号 \_ 信息**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param)

[**Ioctl**](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)

 

