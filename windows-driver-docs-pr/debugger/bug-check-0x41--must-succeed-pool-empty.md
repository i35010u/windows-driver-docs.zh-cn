---
title: Bug 检查将 0x41 向 MUST_SUCCEED_POOL_EMPTY
description: MUST_SUCCEED_POOL_EMPTY bug 检查具有 0x00000041 值。 这表示内核模式线程已请求过多 must-succeed 池。
ms.assetid: 10aafcf4-6af0-41b5-803c-578369bdd810
keywords:
- Bug 检查将 0x41 向 MUST_SUCCEED_POOL_EMPTY
- MUST_SUCCEED_POOL_EMPTY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MUST_SUCCEED_POOL_EMPTY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aa914bd46f773dd69b6e7fe3b672ea0b4982de10
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239728"
---
# <a name="bug-check-0x41-mustsucceedpoolempty"></a>Bug 检查 0x41：必须\_SUCCEED\_池\_空


必须\_SUCCEED\_池\_空 bug 检查的值为 0x00000041。 这表示内核模式线程已请求过多 must-succeed 池。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="mustsucceedpoolempty-parameters"></a>必须\_SUCCEED\_池\_空参数


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
<td align="left"><p>无法满足请求的大小</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>使用从非分页缓冲池页数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>来自大于 PAGE_SIZE 非分页缓冲池的请求数</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>可用的页面数</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

没有驱动程序允许请求必须成功池。

如果不能填充 must-succeed 请求，则会发出此 bug 检查。

<a name="resolution"></a>分辨率
----------

替换或重写其发出请求的驱动程序。 驱动程序不应请求必须成功池。 相反，它应寻求正常池，并适当地处理方案的池是暂时为空。

[ **Kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令将显示导致该错误的驱动程序。

此外，就可以第二个组件已耗尽 must-succeed 池。 若要确定是否这种情况，请先使用**kb**命令。 然后，使用[ **！ vm 1** ](-vm.md)以显示总池使用情况[ **！ poolused 2** ](-poolused.md)以显示每个标记非分页缓冲池使用情况，和 **！poolused 4**以显示每个标记页面缓冲池使用率。 与使用大多数池标记关联的组件可能是问题根源。

 

 




