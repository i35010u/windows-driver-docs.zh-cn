---
title: C28751
description: 警告 C28751 禁止使用 ExAllocatePool 及其变种。
ms.assetid: A2FBEDA8-FA5D-42A5-B298-FF0A32B1662C
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28751
ms.openlocfilehash: f2e329c09f5c018cf8d52e9a8938d7cf426ae7af
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839590"
---
# <a name="c28751"></a>C28751


警告 C28751： ExAllocatePool 及其变体的禁止使用情况

此警告表明，使用的功能已被禁止，并具有更可靠和更安全的替换。

内核内存分配函数 ExAllocatePool 和 ExAllocatePoolWithQuota 不提供标记以帮助稍后进行调试。 您可以使用这些函数的替换内容，这使得调试变得更加容易。

替换

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">API</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="ExAllocatePool"></span><span id="exallocatepool"></span><span id="EXALLOCATEPOOL"></span>ExAllocatePool</p></td>
<td align="left"><p>安全替换： <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)"> <strong>ExAllocatePoolWithTag</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ExAllocatePoolWithQuota"></span><span id="exallocatepoolwithquota"></span><span id="EXALLOCATEPOOLWITHQUOTA"></span>ExAllocatePoolWithQuota</p></td>
<td align="left"><p>安全替换： <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithQuotaTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)"><strong>ExAllocatePoolWithQuotaTag</strong></a>例程</p></td>
</tr>
</tbody>
</table>

 

 

 





