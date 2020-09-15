---
title: C28751
description: 警告 C28751 禁止使用 ExAllocatePool 及其变种。
ms.assetid: A2FBEDA8-FA5D-42A5-B298-FF0A32B1662C
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28751
ms.openlocfilehash: 918c61f90962127839543ec5a934442d452cdc6c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104146"
---
# <a name="c28751"></a>C28751


警告 C28751： ExAllocatePool 及其变体的禁止使用情况

此警告表明，使用的功能已被禁止，并具有更可靠和更安全的替换。

内核内存分配函数 ExAllocatePool 和 ExAllocatePoolWithQuota 不提供标记以帮助稍后进行调试。 您可以使用这些函数的替换内容，这使得调试变得更加容易。

替代功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">API</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="ExAllocatePool"></span><span id="exallocatepool"></span><span id="EXALLOCATEPOOL"></span>ExAllocatePool</p></td>
<td align="left"><p>安全替换： <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)"> <strong>ExAllocatePoolWithTag</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ExAllocatePoolWithQuota"></span><span id="exallocatepoolwithquota"></span><span id="EXALLOCATEPOOLWITHQUOTA"></span>ExAllocatePoolWithQuota</p></td>
<td align="left"><p>安全替换： <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithQuotaTag&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)"><strong>ExAllocatePoolWithQuotaTag</strong></a> 例程</p></td>
</tr>
</tbody>
</table>

 

