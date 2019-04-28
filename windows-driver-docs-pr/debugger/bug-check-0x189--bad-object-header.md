---
title: Bug 检查 0x189 BAD_OBJECT_HEADER
description: BAD_OBJECT_HEADER bug 检查具有 0x00000189 值。 这表示 OBJECT_HEADER 已损坏。
ms.assetid: 1B4F586A-2DFB-421A-863B-CC706FB4795B
keywords:
- Bug 检查 0x189 BAD_OBJECT_HEADER
- BAD_OBJECT_HEADER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BAD_OBJECT_HEADER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6005dfa0260b04b7d27bbcb893afd405efe9a84a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352505"
---
# <a name="bug-check-0x189-badobjectheader"></a>Bug 检查 0x189：错误\_对象\_标头


缺点\_对象\_标头错误检查的值为 0x00000189。 这表示对象\_标头已损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="badobjectheader-parameters"></a>错误\_对象\_标头参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left">指向错误 OBJECT_HEADER</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">指向生成的对象类型基于在 OBJECT_HEADER TypeIndex</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left"><p>损坏的类型。</p>
0x0:类型索引为损坏 0x1:对象安全描述符无效</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">保留</td>
</tr>
</tbody>
</table>

 

 

 




