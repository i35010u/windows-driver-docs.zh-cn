---
title: C28147
description: 警告 C28147 如果对此函数的调用使用默认的池标记（"kdD" 或 "mdW"），则将无法实现池标记目的。
ms.assetid: 4838b006-349e-45d1-8ac3-42cbf0d880b7
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28147
ms.openlocfilehash: 6a7ae7e4e2ad5234ff93b40e23618609dcea0ea6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840313"
---
# <a name="c28147"></a>C28147


警告 C28147：对此函数的调用使用默认的池标记（"kdD" 或 "mdW"）违背了池标记目的

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>附加信息</strong></p></td>
<td align="left"><p>这可能是由于使用 ExAllocatePool 直接引起的，或者可能已从该宏复制了标记。 在任何情况下，应将 ExAllocatePoolWithTag （等）与唯一标记一起使用。</p></td>
</tr>
</tbody>
</table>

 

驱动程序正在指定默认的池标记。 由于系统跟踪池标记使用的池，因此只有那些使用唯一池标记的驱动程序才能识别和区分其池使用。

**ExAllocatePool**和**ExAllocatePoolWithQuota**已过时，应替换为[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)和[**ExAllocatePoolWithQuotaTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)，以便指定唯一的池标记。

 

 





