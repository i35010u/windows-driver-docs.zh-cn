---
title: Bug 检查 0x189 BAD_OBJECT_HEADER
description: BAD_OBJECT_HEADER bug 检查的值为0x00000189。 这表示 OBJECT_HEADER 已损坏。
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
ms.openlocfilehash: d547f6bc0f14ef01850d803c0812817377a54183
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840463"
---
# <a name="bug-check-0x189-bad_object_header"></a>Bug 检查0x189：错误的 \_ 对象 \_ 标头


错误的 \_ 对象 \_ 标头 bug 检查的值为0x00000189。 这表明对象 \_ 标头已损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="bad_object_header-parameters"></a>错误的 \_ 对象 \_ 头参数


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
<td align="left">指向不良 OBJECT_HEADER 的指针</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">指向基于 OBJECT_HEADER 中的 Typeindex> 生成的 OBJECT_TYPE 的指针</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left"><p>损坏的类型。</p>
0x0：类型索引已损坏0x1：对象安全描述符无效</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">预留</td>
</tr>
</tbody>
</table>

 

 

 




