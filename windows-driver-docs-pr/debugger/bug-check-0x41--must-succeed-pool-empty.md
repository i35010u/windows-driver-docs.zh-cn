---
title: Bug 检查0x41 向 MUST_SUCCEED_POOL_EMPTY
description: MUST_SUCCEED_POOL_EMPTY bug 检查的值为0x00000041。 这表示内核模式线程已经请求了太多的必须成功的池。
keywords:
- Bug 检查0x41 向 MUST_SUCCEED_POOL_EMPTY
- MUST_SUCCEED_POOL_EMPTY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MUST_SUCCEED_POOL_EMPTY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 307aeeb9ab23bc4d1deaacd982066a2cdf1125b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790685"
---
# <a name="bug-check-0x41-must_succeed_pool_empty"></a>Bug 检查0x41 向：必须 \_ 成功的 \_ 池 \_ 为空


必须 \_ 成功的 \_ 池 \_ 空 bug 检查的值为0x00000041。 这表示内核模式线程已经请求了太多的必须成功的池。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="must_succeed_pool_empty-parameters"></a>必须 \_ 成功 \_ 池 \_ 空参数


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
<td align="left"><p>无法满足的请求的大小</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>非分页池使用的页数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>非分页池发出的请求数大于 PAGE_SIZE</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>可用页数</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

不允许任何驱动程序请求必须-成功池。

如果无法填充必须成功的请求，则会发出此 bug 检查。

<a name="resolution"></a>解决方法
----------

替换或重写发出请求的驱动程序。 驱动程序不应请求必需-成功池。 相反，它应要求提供普通池，并适当地处理池暂时为空的情况。

[**Kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令将显示导致错误的驱动程序。

此外，另一个组件可能已耗尽了必须成功的池。 若要确定是否为这种情况，请首先使用 **kb** 命令。 然后，使用 [**！ vm 1**](-vm.md) 显示总池使用率， [**！ poolused 2**](-poolused.md) 显示按标记的非分页池使用情况，并使用 **！ poolused 4** 显示每个标记的页缓冲池使用情况。 与使用最大池的标记关联的组件可能是问题的根源。

 

 




