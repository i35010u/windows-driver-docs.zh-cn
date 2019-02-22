---
title: Bug 检查 0x127 PAGE_NOT_ZERO
description: PAGE_NOT_ZERO bug 检查具有 0x00000127 值。
ms.assetid: b6485307-191d-401a-8f2e-7f4a54a630f9
keywords:
- Bug 检查 0x127 PAGE_NOT_ZERO
- PAGE_NOT_ZERO
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PAGE_NOT_ZERO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 88b64d23bc6bfc6259f95441de2bef9823b960f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548123"
---
# <a name="bug-check-0x127-pagenotzero"></a>Bug 检查 0x127:PAGE\_NOT\_ZERO


页面\_不\_零错误检查的值为 0x00000127。 此 bug 检查指示应已填充了零页面不是。 检查此错误可能是由于硬件错误或者特权的组件释放后修改页。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="pagenotzero-parameters"></a>页\_不\_零个参数


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
<td align="left"><p>映射已损坏的页面的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>物理页号</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>零 （保留）</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>零 （保留）</p></td>
</tr>
</tbody>
</table>

 

 

 




