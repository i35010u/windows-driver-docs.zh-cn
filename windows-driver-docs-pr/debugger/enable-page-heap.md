---
title: 启用页堆
description: 启用页堆
ms.assetid: b889b7b7-721c-4ecf-bf59-c1ccc0bc735d
keywords:
- 启用页堆 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1ffe23db6ad6ab653ddab9a9d2b2c12e998dd18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363551"
---
# <a name="enable-page-heap"></a>启用页堆


## <span id="ddk_enable_page_heap_dtools"></span><span id="DDK_ENABLE_PAGE_HEAP_DTOOLS"></span>


**启用页堆**标志打开页堆验证，它监视动态堆内存操作，包括分配和可用的操作，并验证程序检测到堆错误时，会导致调试器中断。

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
<td align="left"><p>整个系统的注册表项、 内核标志和图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

此选项，当设置为图像文件的整页堆验证和设置系统注册表中或为一个内核标记时的标准页堆验证。

-   *完整的页堆验证*(对于 **/i**) 将在每次分配结束的位置的区域的保留虚拟内存。

-   *标准页堆验证*(对于 **/r**或 **/k**) 会随机模式放在末尾的分配和释放堆块时检查这些模式。

设置此标志的图像文件与键入相同**gflags/p /enable** *ImageFile* **/full**图像文件在命令行。

 

 





