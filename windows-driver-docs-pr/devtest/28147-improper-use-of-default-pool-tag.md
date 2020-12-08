---
title: C28147
description: 警告 C28147 使用默认池标记 ( "kdD" 或 "mdW" ) 对此函数的调用不能实现池标记目的。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28147
ms.openlocfilehash: 81f8df7cfab2a30c040d89db78c6bfb94bdcbc91
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793183"
---
# <a name="c28147"></a>C28147


警告 C28147： ) 对此函数的调用使用默认的池标记 ( "kdD" 或 "mdW"，因而无法实现池标记目的

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>这可能是由于使用 ExAllocatePool 直接引起的，或者可能已从该宏复制了标记。 在任何情况下，都应将 ExAllocatePoolWithTag (等 ) 用于唯一标记。</p></td>
</tr>
</tbody>
</table>

 

驱动程序正在指定默认的池标记。 由于系统跟踪池标记使用的池，因此只有那些使用唯一池标记的驱动程序才能识别和区分其池使用。

**ExAllocatePool** 和 **ExAllocatePoolWithQuota** 已过时，应替换为 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 和 [**ExAllocatePoolWithQuotaTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)，以便指定唯一的池标记。

 

