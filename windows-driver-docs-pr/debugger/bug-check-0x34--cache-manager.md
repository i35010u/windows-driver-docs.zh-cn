---
title: Bug 检查 0x34 CACHE_MANAGER
description: CACHE_MANAGER bug 检查具有 0x00000034 值。 这表示在文件系统缓存管理器中出现问题。
ms.assetid: a943e5ce-0be7-4b30-94e7-3e29ce8aa38c
keywords:
- Bug 检查 0x34 CACHE_MANAGER
- CACHE_MANAGER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CACHE_MANAGER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4625af25462acb16857e6ec375e99f6c4e203982
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463786"
---
# <a name="bug-check-0x34-cachemanager"></a>Bug 检查 0x34：缓存\_管理器


缓存\_MANAGER bug 检查的值为 0x00000034。 这表示在文件系统缓存管理器中出现问题。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="cachemanager-parameters"></a>缓存\_管理器参数


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
<td align="left"><p>指定源代码文件和行号信息。 高 16 位 （"0x"后的前四个十六进制数字） 标识由其标识符编号的源代码文件。 低 16 位标识发生错误检查的文件中的源行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查的一个可能的原因是非分页缓冲的池内存耗尽。 如果完全耗尽的非分页缓冲的池内存，则此错误可以停止系统。 但是，在索引过程中，如果可用的非分页缓冲的池内存量为非常低，需要非分页缓冲的池内存的另一个内核模式驱动程序还可以触发此错误。

<a name="resolution"></a>分辨率
----------

**若要解决非分页缓冲的池内存耗尽问题：** 向计算机添加新的物理内存。 这会增加可用的内核的非分页缓冲的池内存的数量。

 

 




