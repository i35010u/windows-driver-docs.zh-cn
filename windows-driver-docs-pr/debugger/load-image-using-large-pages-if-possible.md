---
title: 在可能的情况下大型页加载映像
description: 在可能的情况下大型页加载映像
keywords:
- '如果可能 (全局标志，则使用大页面加载图像) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ddd8d0720f338f19d1a2ee57a730e1e5e971ce0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838167"
---
# <a name="load-image-using-large-pages-if-possible"></a>在可能的情况下大型页加载映像


## <span id="ddk_load_image_using_large_pages_if_possible_dtools"></span><span id="DDK_LOAD_IMAGE_USING_LARGE_PAGES_IF_POSSIBLE_DTOOLS"></span>


**如果 "如果可能，则使用大页面的负载图像**" 设置指示系统使用大页面 (4 MB) 而不是在将二进制文件映射到进程地址空间时使用的标准小页面 (4) KB。

此设置对于大的可执行文件最有用，因为这样可以显著减少物理内存中的页表项的数目。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>lpg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>（无）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

此设置在技术上不是全局标志，因为其值存储在单独的注册表项中，而不是 GlobalFlag 注册表项的值。 因此，您不能使用十六进制值设置它，当您为图像文件选择此设置时，它会显示在显示的 " **其他设置** " 字段中。

 

 





