---
title: 启用按 DLL 的堆标记
description: 启用按 DLL 的堆标记
keywords:
- '按 DLL (全局标志启用堆标记) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e466ae99d874aef1f283bf295f0a7cb884850e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841151"
---
# <a name="enable-heap-tagging-by-dll"></a>启用按 DLL 的堆标记


## <span id="ddk_enable_heap_tagging_by_dll_dtools"></span><span id="DDK_ENABLE_HEAP_TAGGING_BY_DLL_DTOOLS"></span>


**启用堆标记按 DLL** 标志为同一 DLL 创建的堆分配分配唯一标记。

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
<td align="left"><p>系统范围的注册表项、内核标志、映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

可以通过将 [**！堆**](-heap.md) 调试程序扩展与-t 参数一起使用来显示标记。

### <a name="span-idsee_alsospanspan-idsee_alsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[启用堆标记](enable-heap-tagging.md)

 

 





