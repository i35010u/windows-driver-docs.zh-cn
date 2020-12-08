---
title: Bug 检查 0x127 PAGE_NOT_ZERO
description: PAGE_NOT_ZERO bug 检查的值为0x00000127。
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
ms.openlocfilehash: 2444a847a9e989d8ef146619fa83e55c945e9224
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832531"
---
# <a name="bug-check-0x127-page_not_zero"></a>Bug 检查0x127：页 \_ 不 \_ 为零


\_不 \_ 为零 bug 检查的页的值为0x00000127。 此 bug 检查指示应该用零填充的页不应为零。 此 bug 检查可能是由于硬件错误或操作系统的特权组件在释放它之后修改了某个页面导致的。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="page_not_zero-parameters"></a>页 \_ 不是 \_ 零参数


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
<td align="left"><p>映射损坏页的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>物理页码</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>零 (保留) </p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>零 (保留) </p></td>
</tr>
</tbody>
</table>

 

 

 




