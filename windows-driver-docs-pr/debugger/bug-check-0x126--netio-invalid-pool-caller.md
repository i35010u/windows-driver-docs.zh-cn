---
title: Bug 检查 0x126 NETIO_INVALID_POOL_CALLER
description: NETIO_INVALID_POOL_CALLER bug 检查的值为0x00000126。 这表示对 netio 托管内存池进行了无效的池请求，例如，FSB 和 MDL。
keywords:
- Bug 检查 0x126 NETIO_INVALID_POOL_CALLER
- NETIO_INVALID_POOL_CALLER
ms.date: 01/30/2019
topic_type:
- apiref
api_name:
- NETIO_INVALID_POOL_CALLER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 546402fe9016d61fa330ac0ab07a9f94c1346939
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816427"
---
# <a name="bug-check-0x126-netio_invalid_pool_caller"></a>Bug 检查0x126： NETIO \_ 无效的 \_ 池 \_ 调用方


NETIO \_ 无效的 \_ 池 \_ 调用方 bug 检查的值为0x00000126。 这表示对 netio 托管内存池进行了无效的池请求，例如，FSB 和 MDL。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="netio_invalid_pool_caller-parameters"></a>NETIO \_ 无效的 \_ 池 \_ 调用方参数


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
<td align="left"><p>错误检查的子类型。</p>
<p>0x1：池无效。 池处于无效状态。</p>
参数 2-指向内存块或 MDL 的指针。
参数 3-指向页的指针。
参数 4-指向 CPU 池的指针。
<p>0x2： MDL 无效。 MDL 处于无效状态。</p>
参数 2-指向 MDL 的指针。
参数 3-指向 CPU 池的指针。
参数 4-指向池标头的指针。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数1</td>
</tr>
</tbody>
</table>

 

 

 




