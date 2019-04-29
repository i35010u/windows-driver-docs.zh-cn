---
title: C28751
description: 警告 C28751 已禁止的 ExAllocatePool 及其变体的使用情况。
ms.assetid: A2FBEDA8-FA5D-42A5-B298-FF0A32B1662C
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28751
ms.openlocfilehash: f72ee8b8372436e8269846b58131c201af51b6e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374761"
---
# <a name="c28751"></a>C28751


警告 C28751:已禁止的 ExAllocatePool 及其变体的用法

此警告意味着，正在使用的函数已禁止，并具有更为可靠和安全替换。

内核内存分配函数 ExAllocatePool 和 ExAllocatePoolWithQuota 不提供标记，以帮助更高版本调试。 有您可以使用，这使调试更加容易这些函数的替代项。

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
<td align="left"><p>可靠的替代：<a href="https://msdn.microsoft.com/library/windows/hardware/ff544520" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544520)"><strong>ExAllocatePoolWithTag</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ExAllocatePoolWithQuota"></span><span id="exallocatepoolwithquota"></span><span id="EXALLOCATEPOOLWITHQUOTA"></span>ExAllocatePoolWithQuota</p></td>
<td align="left"><p>可靠的替代：<a href="https://msdn.microsoft.com/library/windows/hardware/ff544513" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithQuotaTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544513)"><strong>ExAllocatePoolWithQuotaTag</strong></a> routine</p></td>
</tr>
</tbody>
</table>

 

 

 





