---
title: C28147
description: 警告 C28147 使用默认的池标记 (kdD 或 mdW) 对此函数的调用会从而池标记的初衷背道而驰。
ms.assetid: 4838b006-349e-45d1-8ac3-42cbf0d880b7
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28147
ms.openlocfilehash: f836334872c5157def7396b87055149c3db3f198
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364107"
---
# <a name="c28147"></a>C28147


警告 C28147:使用默认的池标记 (kdD 或 mdW) 对此函数的调用的初衷背道而驰标记池

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>这可能引起 ExAllocatePool 直接使用，或标记可能从该宏复制。 在任何情况下，应使用唯一的标记使用 ExAllocatePoolWithTag （等）。</p></td>
</tr>
</tbody>
</table>

 

该驱动程序指定默认的池标记。 系统按池标记跟踪池使用，因为使用的唯一池标记这些驱动程序可以标识和区分其池使用。

**ExAllocatePool**并**ExAllocatePoolWithQuota**已过时，并应替换为[ **ExAllocatePoolWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)和[ **ExAllocatePoolWithQuotaTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithquotatag)，其可让您指定的唯一池标记。

 

 





