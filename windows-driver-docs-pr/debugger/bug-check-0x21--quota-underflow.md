---
title: Bug 检查 0x21 QUOTA_UNDERFLOW
description: QUOTA_UNDERFLOW bug 检查具有 0x00000021 值。 这表示已错误配额费用处理通过返回到某一特定块的配额不是以前的收费。
ms.assetid: 41b1c93b-77e0-4baa-8eed-7a956e45d144
keywords:
- Bug 检查 0x21 QUOTA_UNDERFLOW
- QUOTA_UNDERFLOW
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- QUOTA_UNDERFLOW
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 45b0427b81d0321e1fbb8a7c7ece763dd733ba39
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519595"
---
# <a name="bug-check-0x21-quotaunderflow"></a>Bug 检查 0x21：配额\_下溢


配额\_下溢错误检查的值为 0x00000021。 这表示已错误配额费用处理通过返回到某一特定块的配额不是以前的收费。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="quotaunderflow-parameters"></a>配额\_下溢参数


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
<td align="left"><p>1</p></td>
<td align="left"><p>最初的收费，如果可用过程。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>配额类型。 有关所有可能的配额类型值的列表，请参阅 Ps.h Windows Driver Kit (WDK) 中的标头文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>配额以返回初始的计费的量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>不返回的配额剩余量。</p></td>
</tr>
</tbody>
</table>

 

 

 




