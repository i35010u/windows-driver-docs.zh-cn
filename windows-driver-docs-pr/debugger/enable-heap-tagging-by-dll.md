---
title: 启用按 DLL 的堆标记
description: 启用按 DLL 的堆标记
ms.assetid: d8f8f6f6-7365-4208-834f-3f5ccacdb7b6
keywords:
- 启用堆标记 dll （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f53fa81c682e0bd6d549ab6bb712310aa0afc77
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330795"
---
# <a name="enable-heap-tagging-by-dll"></a>启用按 DLL 的堆标记


## <span id="ddk_enable_heap_tagging_by_dll_dtools"></span><span id="DDK_ENABLE_HEAP_TAGGING_BY_DLL_DTOOLS"></span>


**启用按 DLL 标记堆**标志将唯一的标记分配给堆分配创建的同一个 DLL。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>htd</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x8000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAG_BY_DLL</p></td>
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

[启用堆标记](enable-heap-tagging.md)

 

 





