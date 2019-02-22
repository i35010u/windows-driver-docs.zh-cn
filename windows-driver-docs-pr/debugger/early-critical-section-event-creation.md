---
title: 早期的关键部分事件创建
description: 早期的关键部分事件创建
ms.assetid: a9453e6d-7566-4226-a950-d32d6192f8ac
keywords:
- 早期的关键部分事件创建 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6d9cfcae920046584bf2decab62f48649ed7a77
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544717"
---
# <a name="early-critical-section-event-creation"></a>早期的关键部分事件创建


## <span id="ddk_early_critical_section_event_creation_dtools"></span><span id="DDK_EARLY_CRITICAL_SECTION_EVENT_CREATION_DTOOLS"></span>


**早期的关键部分事件创建**标志创建事件句柄初始化时关键部分，而不是等待，直到需要该事件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>cse</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x10000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_CRITSEC_EVENT_CREATION</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>整个系统的注册表项、 内核标志和图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

当 Windows 无法创建事件时，它生成在初始化过程中的异常，并进入和离开关键节的调用不会失败。

由于此标志使用大量的非分页缓冲的池内存，则仅在有足够的内存的非常可靠系统上使用它。

 

 





