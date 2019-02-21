---
title: 禁用堆上免费 coalesce
description: 禁用堆上免费 coalesce
ms.assetid: 64a68fa2-9270-4b2d-9edc-d54370191dcb
keywords:
- 禁用堆 coalesce 上免费 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef5b8fd7ff3da4569029b3cbcbd46474ce3a6666
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520534"
---
# <a name="disable-heap-coalesce-on-free"></a>禁用堆上免费 coalesce


## <span id="ddk_disable_heap_coalesce_on_free_dtools"></span><span id="DDK_DISABLE_HEAP_COALESCE_ON_FREE_DTOOLS"></span>


**禁用堆上免费 coalesce**标志时，保留的堆内存的相邻块单独则释放。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>dhc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x00200000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_HEAP_DISABLE_COALESCING</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>整个系统的注册表项、 内核标志和图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

默认情况下，Windows 将新释放相邻块 （"将合并"） 合并到单个块。 合并块需要时间，但减少了可能会强制分配更多内存时找不到连续内存堆的碎片。

此标志用于保持与旧的应用程序兼容性。

 

 





