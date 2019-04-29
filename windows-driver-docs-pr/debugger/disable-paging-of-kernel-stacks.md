---
title: 禁用内核堆栈分页
description: 禁用内核堆栈分页
ms.assetid: 3bf0ae20-4569-41de-9d7c-dd6a2790dac6
keywords:
- 禁用分页的内核堆栈 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d02e9a57d9950e8012149d4c080f9ca175879735
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324573"
---
# <a name="disable-paging-of-kernel-stacks"></a>禁用内核堆栈分页


## <span id="ddk_disable_paging_of_kernel_stacks_dtools"></span><span id="DDK_DISABLE_PAGING_OF_KERNEL_STACKS_DTOOLS"></span>


**禁用分页的内核堆栈**的标记阻止对非活动状态的线程的内核模式堆栈的分页。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>dps</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x80000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_DISABLE_PAGE_KERNEL_STACKS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>整个系统的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

通常情况下，不能分页的内核模式堆栈;它被保证可驻留在内存中。 但是，Windows 偶尔页面处于非活动状态的线程的内核堆栈。 此标志会阻止这些情况的发生。

仅当其堆栈处于物理内存时，内核调试程序可以提供有关线程的信息。 此标志是特别重要调试死锁时和在其他情况下，当必须跟踪每个线程。

 

 





