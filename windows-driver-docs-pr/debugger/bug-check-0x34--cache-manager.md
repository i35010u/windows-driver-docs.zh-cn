---
title: Bug 检查0x34 赋 CACHE_MANAGER
description: CACHE_MANAGER bug 检查的值为0x00000034。 这表示文件系统的缓存管理器出现问题。
keywords:
- Bug 检查0x34 赋 CACHE_MANAGER
- CACHE_MANAGER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CACHE_MANAGER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 09a45d4dca3e9919cb6d76aa04ce94896dd15bbc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786483"
---
# <a name="bug-check-0x34-cache_manager"></a>Bug 检查0x34 赋：缓存 \_ 管理器


缓存 \_ 管理器 bug 检查的值为0x00000034。 这表示文件系统的缓存管理器出现问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="cache_manager-parameters"></a>缓存 \_ 管理器参数


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
<td align="left"><p>指定源文件和行号信息。 高16位 ("0x" 后的前四个十六进制数字 ) 按其标识符号识别源文件。 低16位标识文件中发生错误检查的源行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此错误检查的一个可能原因是消耗了未分页的池内存。 如果非分页池内存完全耗尽，此错误可能会停止系统。 但是，在索引过程中，如果可用的非分页池内存量非常低，则另一个需要非分页池内存的内核模式驱动程序也会触发此错误。

<a name="resolution"></a>解决方法
----------

**解决非分页池内存消耗问题：** 向计算机添加新的物理内存。 这会增加可用于内核的非分页缓冲池内存量。

 

 




