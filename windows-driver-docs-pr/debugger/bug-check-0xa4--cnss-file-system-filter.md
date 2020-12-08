---
title: Bug 检查 0xA4 CNSS_FILE_SYSTEM_FILTER
description: CNSS_FILE_SYSTEM_FILTER bug 检查的值为0x000000A4。 此 bug 检查指示在 CNSS 文件系统筛选器中出现问题。
keywords:
- Bug 检查 0xA4 CNSS_FILE_SYSTEM_FILTER
- CNSS_FILE_SYSTEM_FILTER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CNSS_FILE_SYSTEM_FILTER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 29872068f061d7ebebdda27c5c54d95bf827cb26
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784161"
---
# <a name="bug-check-0xa4-cnss_file_system_filter"></a>Bug 检查0xA4： CNSS \_ 文件 \_ 系统 \_ 筛选器


CNSS \_ 文件 \_ 系统 \_ 筛选器 bug 检查的值为0x000000A4。 此 bug 检查指示在 CNSS 文件系统筛选器中出现问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="cnss_file_system_filter-parameters"></a>CNSS \_ 文件 \_ 系统 \_ 筛选器参数


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

\_ \_ \_ 由于非分页池内存已满，因此可能会发生 CNSS 文件系统筛选器 bug 检查。 如果非分页池内存完全满，此错误可能会导致系统停止。 但是，在索引过程中，如果可用的非分页池内存量非常低，则另一个需要非分页池内存的内核模式驱动程序也会触发此错误。

<a name="resolution"></a>解决方法
----------

**解决非分页池内存消耗问题：** 向计算机添加新的物理内存。 此内存 sincrease 可供内核使用的非分页池内存的数量。

 

 




