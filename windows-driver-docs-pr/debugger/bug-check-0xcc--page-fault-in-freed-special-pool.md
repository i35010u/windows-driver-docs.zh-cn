---
title: Bug 检查 0xCC PAGE_FAULT_IN_FREED_SPECIAL_POOL
description: PAGE_FAULT_IN_FREED_SPECIAL_POOL bug 检查具有 0x000000CC 值。 这表明系统已引用先前释放的内存。
ms.assetid: 77823c38-76eb-49ca-aaf4-3cf5994a0525
keywords:
- Bug 检查 0xCC PAGE_FAULT_IN_FREED_SPECIAL_POOL
- PAGE_FAULT_IN_FREED_SPECIAL_POOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PAGE_FAULT_IN_FREED_SPECIAL_POOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e9ec4361b127f068b7be532282a25c182929d145
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518902"
---
# <a name="bug-check-0xcc-pagefaultinfreedspecialpool"></a>Bug 检查 0xCC：页\_容错\_IN\_FREED\_特殊\_池


页面\_容错\_IN\_FREED\_特殊\_池 bug 检查的值为 0x000000CC。 这表明系统已引用先前释放的内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="pagefaultinfreedspecialpool-parameters"></a>页\_容错\_IN\_FREED\_特殊\_池参数


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

驱动程序验证工具特殊池选项具有捕获访问内存，这是早期释放的系统。 这通常表示的系统驱动程序同步问题。

有关特殊的池的信息，请查阅 Windows 驱动程序工具包的驱动程序验证程序部分。

<a name="remarks"></a>备注
-------

这不会受到**试用-除**处理程序-通过探测来仅进行保护。

 

 




