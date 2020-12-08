---
title: 启用页堆
description: 启用页堆
keywords:
- " (全局标志启用页堆) "
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82d0f85a31830aa3fb81e03faae49d3302351164
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813281"
---
# <a name="enable-page-heap"></a>启用页堆


## <span id="ddk_enable_page_heap_dtools"></span><span id="DDK_ENABLE_PAGE_HEAP_DTOOLS"></span>


**启用页堆标志启用** 页堆验证，这会监视动态堆内存操作（包括分配和免费操作），并在验证程序检测到堆错误时导致调试器中断。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>hpa</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x02000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_HEAP_PAGE_ALLOCS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围的注册表项、内核标志、映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

当设置为映像文件时，此选项将启用完整的页堆验证，并在系统注册表中或作为内核标志时启用标准页堆验证。

-   对于 **/i**) ，*整页堆验证* (在每次分配结束时放置保留虚拟内存的区域。

-   **/R** 或 **/k** 的 *标准页堆验证* () 在分配末尾放置随机模式，并在释放堆块时检查模式。

为映像文件设置此标志与在命令行中为映像文件键入 **gflags/p/Enable** *ImageFile* **/full** 相同。

 

 





