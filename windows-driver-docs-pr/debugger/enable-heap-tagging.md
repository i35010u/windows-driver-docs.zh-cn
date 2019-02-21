---
title: 启用堆标记
description: 启用堆标记
ms.assetid: be877811-075c-4019-81dd-73a134d5fb81
keywords:
- 启用堆标记 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bcb37128088c2461d316de5d8cc5a8e91dfebf9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524979"
---
# <a name="enable-heap-tagging"></a>启用堆标记


## <span id="ddk_enable_heap_tagging_dtools"></span><span id="DDK_ENABLE_HEAP_TAGGING_DTOOLS"></span>


**启用堆标记**标志将唯一的标记分配给堆分配。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>加热</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x800</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAGGING</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>整个系统的注册表项、 内核标志和图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

可以通过使用显示标记[ **！ 堆**](-heap.md)调试器扩展与-t 参数。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[启用堆按 DLL 标记](enable-heap-tagging-by-dll.md)

 

 





