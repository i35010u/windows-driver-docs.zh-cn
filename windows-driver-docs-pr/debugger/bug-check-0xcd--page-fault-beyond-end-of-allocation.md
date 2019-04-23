---
title: Bug 检查 0xcd 填充 PAGE_FAULT_BEYOND_END_OF_ALLOCATION
description: PAGE_FAULT_BEYOND_END_OF_ALLOCATION bug 检查具有 0x000000CD 值。 这表示系统访问超出末尾的某些驱动程序的池分配的内存。
ms.assetid: ce506f92-94a9-4ef5-974b-32013410468a
keywords:
- Bug 检查 0xcd 填充 PAGE_FAULT_BEYOND_END_OF_ALLOCATION
- PAGE_FAULT_BEYOND_END_OF_ALLOCATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PAGE_FAULT_BEYOND_END_OF_ALLOCATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 893035d0996e242808cceda57c62d813257c375a
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903897"
---
# <a name="bug-check-0xcd-pagefaultbeyondendofallocation"></a>Bug 检查 0xCD：页\_容错\_超出\_最终\_OF\_分配


页面\_容错\_超出\_最终\_OF\_分配错误检查的值为 0x000000CD。 这表示系统访问超出末尾的某些驱动程序的池分配的内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="pagefaultbeyondendofallocation-parameters"></a>页\_容错\_超出\_最终\_OF\_分配参数


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
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>写入</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>（如果已知） 引用内存的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。

<a name="cause"></a>原因
-----

驱动程序分配*n*特殊池中的内存字节数。 随后，系统引用多个*n*来自该池的字节数。 这通常表示的系统驱动程序同步问题。

有关特殊的池的信息，请查阅 Windows 驱动程序工具包的驱动程序验证程序部分。

<a name="remarks"></a>备注
-------

这不会受到**试用-除**处理程序-通过探测来仅进行保护。

 

 




