---
title: 在可能的情况下大型页加载映像
description: 在可能的情况下大型页加载映像
ms.assetid: 7f75b5bd-cc25-4f09-9d60-55b86969d16b
keywords:
- 加载图像如有可能使用大型页 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bccbe3e8f6ac111c0e2a0309391fe604f0391fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383334"
---
# <a name="load-image-using-large-pages-if-possible"></a>在可能的情况下大型页加载映像


## <span id="ddk_load_image_using_large_pages_if_possible_dtools"></span><span id="DDK_LOAD_IMAGE_USING_LARGE_PAGES_IF_POSSIBLE_DTOOLS"></span>


**尽可能使用大型页映像加载**设置而不是标准的小型页面 (4 KB) 映射到进程地址空间的二进制文件时都指示系统在使用大型页 (4 MB)。

此设置是对于大型的可执行文件，最有帮助，因为它大大减少了在物理内存中的页表条目数。

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
<td align="left"><p>图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

此设置不是从技术上讲全局标志，因为其值存储在一个单独的注册表项不是作为 GlobalFlag 注册表项的值。 因此，不能使用十六进制值，设置它并选择图像文件的此设置时，出现在**其他设置**显示的字段。

 

 





