---
title: Bug 检查 0xCD PAGE_FAULT_BEYOND_END_OF_ALLOCATION
description: PAGE_FAULT_BEYOND_END_OF_ALLOCATION bug 检查的值为0x000000CD。 这表示系统访问的内存超出了某个驱动程序的池分配的结尾。
keywords:
- Bug 检查 0xCD PAGE_FAULT_BEYOND_END_OF_ALLOCATION
- PAGE_FAULT_BEYOND_END_OF_ALLOCATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PAGE_FAULT_BEYOND_END_OF_ALLOCATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 39870f5a2c53433400462f322148ae760fb2024f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825217"
---
# <a name="bug-check-0xcd-page_fault_beyond_end_of_allocation"></a>Bug 检查0xCD：在 \_ \_ \_ \_ \_ 分配结束后出现页错误


\_ \_ 超出 \_ \_ 分配错误检查结束的页错误 \_ 具有值0x000000CD。 这表示系统访问的内存超出了某个驱动程序的池分配的结尾。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="page_fault_beyond_end_of_allocation-parameters"></a>\_ \_ 超出 \_ \_ 分配参数结尾的 \_ 页面错误


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>引用的内存地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0：</strong> 读取</p>
<p><strong>1：</strong> 写入</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>引用内存的地址（如果已知）</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

如果能够识别出导致错误的驱动程序，则其名称将打印在蓝屏上，并存储在内存中的 (PUNICODE\_STRING) KiBugCheckDriver  位置。

<a name="cause"></a>原因
-----

驱动程序从特殊池分配了 *n* 个字节的内存。 然后，系统从该池中引用了超过 *n* 个字节。 这通常表示系统驱动程序同步问题。

有关特殊池的信息，请参阅 Windows 驱动程序工具包的驱动程序验证程序部分。

<a name="remarks"></a>备注
-------

这不能通过 **try-except** 处理程序来保护--它只能通过探测进行保护。

 

 




